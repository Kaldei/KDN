---
title: AWS Cheat Sheet DVA-C02
summary: A cheat sheet to study the Developer Associate certification.
description: A cheat sheet to study the Developer Associate certification.
tags:
  - aws
---

# DVA Specific

---

### Deployment (Publishing Strategies)

|Requirement|Service|
|-----------|-------|
|Least impact on user accessing prod|Blue-Green Deployment|
|Least impact on user accessing prod and lower cost|Canary Release (small percentage test)|
|Deployment that test on a small percentage and then deploy for all users|Canary (e.g. Canary10Percent5Minutes -> 5 min)|
|Deployment that deploy the same amount of users periodically|Linear (e.g. Linear10PercentEvery10Minutes -> 50 min)|
|||
|ECS Rolling Update and keep same capacity during rolling|Min 100%, Max 150%|
|Deploy a **configuration change** with the ability to roll-back|AWS AppConfig|
|||
|Instantly effortlessly switch traffic to a new tested Lambda|Set `AutoPublishAlias` property|
|Deploy new version of a Lambda but keep the ability to return to older version|Use function alias with different versions|
|||
|Use AWS Fault Injection Simulator only on a specified region|Use resource filter of a target component in the template|

---

### Troubleshooting and Optimization

|Requirement|Service|
|-----------|-------|
|ThrottlingExeption|Use exponential back off (retry 1s > 2s > 4s > 8s > 16s > ...)|
|5xx errors and throttling|Implement retries|
|4xx errors|Do not implement retries|
|Troubleshoot when getting HTTP 503 slow down response on S3 PUT or DELETE|Probably due to objects having millions of versions, so S3 automatically throttles. Use Amazon S3 Inventory to create a report|
|Signed AWS HTTP API request|SigV4 (header `Authorization` or `X-Amz-...`)|

# Application Integration

---

### SQS

|Requirement|Service|
|-----------|-------|
|SQS need to manage message that are > 256KB|SQS extended Library for Java|
|Configure messages to be processed only after 5 minutes of being published in the queue|Use `DelaySeconds` parameter|
|Messages are processed more than once|Increase Visibility Timeout (default: 30s, min: 0s, max: 12h)|
|Consumers are polling the SQS Queue too often and are getting empty result|Enable Long Polling|
|Some messages are not processed correctly|Add SQS Dead Letter Queue|
|Multiple consumers need to receive same message form SQS|SNS with SQS Fan Out Pattern|

---

### SNS

|Requirement|Service|
|-----------|-------|
|Send SNS message to certain subscribers and not others|SNS Message Filtering|

# Compute

---

### Beanstalk

|Requirement|Service|
|-----------|-------|
|Ignoring application HTTP errors in Beanstalk|Enhanced health monitoring|
|||
|Beanstalk deployment mode for development and test purpose|Single Instance (no ASG)|
|Beanstalk deployment mode for production purpose|High Availability (ASG)|
|||
|Beanstalk update deployment all at the same time (fast but downtime)|All at once|
|Beanstalk update deployment by batches called buckets (no additional cost but run at below capacity)|Rolling|
|Beanstalk update deployment by batches but not running below capacity (small additional cost)|Rolling with additional batches|
|Beanstalk update deployment using a temporary ASG to confirm new version works (higher cost)|Immutable|
|||
|Specify how the application will be deployed to the underlying instances|File `appspec.yml`|

* Beanstalk is free, but we pay for the infrastructure deployed by Beanstalk.
* We can choose between 2 Tier:
  * Web Server Tier: Architecture with an ELB in front of an Auto Scaling Group of EC2 web servers.
  * Worker Tier: Architecture with an SQS Queue in front of an Auto Scaling Group of EC2 workers.
* Beanstalk can store at most 1000 application versions. They can be removed with a Lifecycle Policy (based on time or space).
* Beanstalk source bundle (extension) have to respect the following rules: 
  * Folder named `.ebextension` (\<500MB).
  * Files in YAML or JSON with `.config` extension.

---

### Lambda

|Requirement|Service|
|-----------|-------|
|Stop a Lambda function that recursively call itself|Set function concurrent execution to 0|
|Improve performance of a Lambda that is CPU, network or memory bound|Increase memory|

* Lambda@Edge functions can only be created in `us-east-1`.

---

### SAM

|Requirement|Service|
|-----------|-------|
|Define serverless resources in a YAML template|AWS Serverless Application Model (SAM)|
|Test a Lambda in a SAM locally|Run `cdk synth` and `sam local start-lambda` commands|

# Containers

---

### ECS

|Requirement|Service|
|-----------|-------|
|Place tasks on the EC2 with the least available CPU or Memory (cost-effective)|Binpack Placement Strategy|
|Place task randomly on available EC2s|Random Placement Strategy|
|Spread tasks based on a specified parameter (instance ID, AZ, ...)|Spread Placement Strategy|
|Constraint to place tasks on different EC2|Constraint `distinctInstance`|
|||
|Allow tasks to access AWS resources|Create an IAM role at the task level and enable `ECS_ENABLE_TASK_IAM_ROLE` in `/etc/ecs/ecs.config`|

* The Load Balancer can only be added during the creation of a service (it can't be modified or removed).

# Database

---

### DynamoDB

|Requirement|Service|
|-----------|-------|
|Use one Partition Key in a query|Query|
|Use the Partition Key and the Sort Key in a query|GetItem|
|Use multiple Partition Keys in a single query|BatchGetItem|
|||
|Capture and store (for 24h) time ordered item modifications on a DynamoDB table|DynamoDB Streams|

# Developer Tools

---

### Code Suite

|Requirement|Service|
|-----------|-------|
|Fully managed VCS, can contain file > 5GB|AWS CodeCommit|
|Service that can compile and test code|AWS CodeBuild|
|Help to troubleshoot issue in code|Amazon CloudGuru|

---

### X-Ray

|Requirement|Service|
|-----------|-------|
|Trace Lambda invoked by non-instrumented service|Enable Active Tracing in AWS Lambda config|
|Filter X-Ray traces (logs) on a specific value (e.g. a user)|Use Annotations (key-value pair that can be used with filters)|
|||
|Enable X-Ray logs on BeanStalk|Add the `.ebextensions/xray-daemon.config`|
|Enable X-Ray on EC2|Run X-Ray Daemon|
|Change X-Ray Daemon listening port|Use `--bind` flag|
|||
|X-Ray Default Sampling Rule|1 request/second & 5% of any additional request per host|

# Security and Compliance

---

### IAM

|Requirement|Service|
|-----------|-------|
|Tool to analyze access control policies to resources like S3|IAM Access Analyzer|
|Report on IAM users and the status of their credentials|IAM Credentials|

# Manager & Governance

---

### AWS CLI

|Requirement|Service|
|-----------|-------|
|AWS CLI credential precedence usage|CLI options > Environment variables > Files in `~/.aws` >  Resource Instance profile (EC2, ECS, Lambda)|

---

### CloudFormation

|Requirement|Service|
|-----------|-------|
|Create a CloudFormation stack in multiple AWS accounts in multiple Regions|CloudFormation StackSets|
|Detect changes made to a stack resource outside of CloudFormation|CloudFormation Drift|
|Analyze upcoming changes on a stack update without executing it|ChangeSets|

---

### CloudWatch

|Requirement|Service|
|-----------|-------|
|Not all data is delivered|IteratorAge (age of the last records processed by functions)|
|Monitor EC2 memory usage (RAM is not included in EC2 metrics)|Use Unified CloudWatch Agent (custom metric)|
|||
|Collect metrics for EC2 every 5 minutes|Basic Monitoring|
|Collect metrics for EC2 every 1 minute|Detailed Monitoring|
|High Resolution Custom Metrics can be collected at minimum|Every 1 second|
|Regular alarms can be triggered|Any multiple of 60 seconds|
|High Resolution alarms can be triggered|Every 10 or 30 seconds|
|||
|Detect unusual activity on all AWS Regions|CloudTrail Insights|
|Test a CloudWatch Alarm|Use the `set-alarm-state` CLI command|

* CloudWatch Metric Filters do not retroactively filter data. CloudWatch only publish metrics after the Filter has been created.

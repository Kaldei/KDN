---
title: AWS Cheat Sheet SOA-C02
summary: A cheat sheet to study the SysOps Administrator Associate certification.
description: A cheat sheet to study the SysOps Administrator Associate certification.
tags:
  - aws
---

# SOA Specific

---

### Monitoring, Logging, and Remediation

|Requirement|Service|
|-----------|-------|
|Create a CloudWatch alarm but without knowing expected usage|CloudWatch alarm based on Anomaly Detection|
|HTTP 502 errors from CloudFront|Error in the validation of the SSL/TLS certificate on the origin server|
|Monitor network between ECS tasks|Choose `awsvpc` network mode and enable CloudWatch Logs on the ENI of each task|

* **A VPC Flow Log cannot be modified.**

---

### Reliability and Business Continuity

|Requirement|Service|
|-----------|-------|
|Find out if resources in an Account experienced an outage|AWS Personal Health Dashboard|
|Find out if a service in a Region had an outage|AWS Service Health Dashboard|

---

### Cost and Performance Optimization

|Requirement|Service|
|-----------|-------|
|Separate costs into categories|Use Cost Allocation Tags|
|Analyze resources (EC2, EBS, ECS on Fargate, Lambda) to provide insights on how to improve performance and reduce costs|AWS Compute Optimizer|

# Compute

---

### EC2

|Requirement|Service|
|-----------|-------|
|Migrate an EC2 instance in another AZ|Create an AMI from the instance and create a new instance from the AMI|
|Linearly increase traffic to EC2 instance that needs time before being able to receive all the requests|Configure Slow Start Mode for the Target Group|
|||
|Getting `InsufficientInstanceCapacity` error when trying to launch an EC2 instance|AWS does not have enough on-demand capacity in the AZ|
|Getting `InstanceLimitExceeded`  error when trying to launch an EC2 instance|Ask for a Quota increase|
|Log Processes running on an EC2 instance|Install Unified Cloud Agent with `procstat` plugin|
|||
|Pack instances close together in an AZ to achieve the low-latency network for HPC|Cluster Placement Group|
|Spread instances across logical partitions (using different underlying) for large distributed and replicated workloads (Hadoop, Cassandra, Kafka).|Partition Placement Group|
|Strictly places instances across distinct underlying hardware to reduce correlated failures.|Spread Placement Group|

* Move an EC2 instance in or out of a Placement Group:
  * Stop the instance,
  * Use CLI with `modify-instance-placement`,
  * Start the instace.

---

### Lambda

* The maximum size of `/tmp` in a Lambda is 10240 MB.

# Databases

---

### Aurora

|Requirement|Service|
|-----------|-------|
|Restore the DB Cluster in the same DB Cluster|Aurora Backtracking (Rewind the Cluster)|
|Restore the DB Cluster creating a new DB Cluster|Point in Time Recovery|
|||
|Highly available database for multi-tenant workloads|Aurora multi-master DB cluster|

* The maximum number of Read Replicas for in a single Aurora Cluster is 15.
* Aurora Cluster Automatic Backups cannot be disabled.

---

### RDS

|Requirement|Service|
|-----------|-------|
|Get notifications when there is a change in a database instance|RDS Event & Event Subscription|
|Troubleshoot performance issues on databases instances with dashboards|RDS Performance Insights|

* **Auto Scaling for RDS instance can only scale up once every 6 hours.**
* The maximum number of Read Replicas for an RDS instance is 15.
* It is required for the RDS database to be encrypted in order to create encrypted Read Replicas.

---

### Memcached

|Requirement|Service|
|-----------|-------|
|Connect a fleet of EC2 to ElasticCache Memcached|Memcached Auto Discovery|
|Memcached Evictions are high|Need to scale up (increase memory) or scale out (add additional node)|

# Management and Governance

---

### CloudFormation

|Requirement|Service|
|-----------|-------|
|Delete a CloudFormation Stack without deleting the resources|Add a Retain Deletion Policy on the resources to keep|

---

### AWS CloudTrail

|Requirement|Service|
|-----------|-------|
|Ensure CloudTrail logs store in S3 haven't been modified or deleted|CloudTrail Log File Integrity Validation (verify file integrity with AWS CLI)|
|Detect unusual activity in the Account with CloudTrail enabled|CloudTrail Insights|

---

### AWS Config

|Requirement|Service|
|-----------|-------|
|Evaluate compliance over time|AWS Config|
|Automatically reconfigure to match compliance|AWS Config Remediation|

---

### AWS Organization

|Requirement|Service|
|-----------|-------|
|Standardize Tags in all AWS Account in an AWS Organizations|AWS Organizations Tag Policies|

---

### AWS System Manager

|Requirement|Service|
|-----------|-------|
|One time patch a fleet of EC2 instances|SSM Run Command|
|Automatically patch a fleet of EC2 instances|SSM Patch Manager|
|||
|Policy that needs to be assigned to an EC2 instance to connect via SSM|AmazonSSMManagedInstanceCore|
|Instance is not able to get SSM Parameters even with the right IAM permissions|Install the SSM agent on the instance|

# Networking and Content Delivery

---

### VPC

* The maximum size of CIDR in AWS VPC is `/16`.
* When creating a VPC, AWS "reserve" 5 IPs addresses (the four firsts IPs and the last one).
  * `10.0.0.0`: Network address.
  * `10.0.0.1`: Reserved by AWS for the VPC router.
  * `10.0.0.2`: Reserved by AWS for VPCs with multiple CIDR blocks, the IP address of the DNS server.
  * `10.0.0.3`: Reserved by AWS for future use.
  * `10.0.255`: Network broadcast address (broadcast is not supported in a VPC, therefore AWS reserve this address).

---

### Route 53

* In order to use a Route 53 domain name with S3 Website Hosting, the bucket has to be the same as the record set in Route 53.
* To set an automated failover, you need to create two Routing Policy:
  * Create a Primary Failover Routing Policy record with a Health Check
  * Create a Secondary Failover Routing Policy

# Security Identity, and Compliance

---

### Cognito

|Requirement|Service|
|-----------|-------|
|Authenticate to get tokens|Cognito User Pool|
|Use Web Identity Providers|Cognito User Pool|
|Exchange Tokens for AWS credentials (access to services)|Cognitoy Identity Pools|
|Provide guest access to a web application|Cognito Identity Pools|

---

### KMS

|Requirement|Service|
|-----------|-------|
|Control Access to KMS CMK|Use KMS Key|
|Periodically rotate CMK that is in KMS|Create a new Key and use Key Aliases in KMS (keep old Key to decrypt old data)|
|||
|Dedicated hardware module to manage encryption keys (full control over them)|AWS CloudHSM|

* CMK stands for Customer Managed Key.
* When Automatic Rotation is enabled on KMS CMK, the backing key is rotated every 1 year.

# Storage

---

### S3

|Requirement|Service|
|-----------|-------|
|Get insights on the optimal numbers of days to move S3 objects to different storage tiers|S3 Analytics (Storage Class Analysis)|
|Create reports on the replication and encryption status on objects in S3|S3 Inventory|
|When multiple applications are using a bucket so it became complex to manage the bucket policy|S3 Access Points|

* It is required to enable S3 Versioning on buckets before enabling S3 Replication.
* It is required to enable S3 Versioning on a bucket before enabling MFA Delete.

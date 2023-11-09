---
title: AWS Cheat Sheet SAA-003
summary: A cheat sheet to study the Solution Architect Associate certification.
description: A cheat sheet to study the Solution Architect Associate certification.
tag: aws
---

# Cost Management

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Predictable capacity and uptime requirements|Reserved Instance|
|Sockets and cores capacity|Dedicated Host|

# Serverless

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|**Least operational overhead means**|**Serverless**|
|Lambda function needs to be invoked by a third party via a webhook|Lambda URL|

---

### Lambda

* **Lambda execution max duration is 15 min.**

* **Lambda function can go up to 10 GB of memory (free tier only allow 512MB).**

* Lambda SnapStart for Java (only Java 11 and Java 17) can improve startup performance for latency-sensitive applications by up to 10x at no extra cost with no changes to your function code.

---

### SQS

* SQS and SNS messages are limited to 256KB.

# Application Integration

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Managing services events|Amazon EventBridge|
|SaaS integration|Amazon AppFlow|
|||
|GraphQL serverless|AWS AppSync|
|RESTful web services (not GraphQL)|API Gateway|
|||
|Send email|SES (Simple Email Service)|
|Migration from RabbitMQ|Amazon MQ|

# Containers

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Running K8s on premise but use AWS-managed service for managing multiple clusters of nodes|EKS Anywhere|

---

### ECS

* ECS Anywhere requires the installation of AWS System Manager (this allows the agent to register itself).

---

### EKS

* EKS distribution includes open-source K8S components only.

# Networking and Content Delivery

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Non-full manage Access to internet|NAT Instance|
|Fully managed access to internet from private VPC for IPv4|NAT gateway|
|Fully managed access to internet from private VPC for IPv6|Egress-only Internet Gateway|
|||
|**Connect API Gateway to a VPC securely**|**VPC Link**|
|VPC traffic to S3 or DynamoDB|VPC Gateway Endpoint|
|Link API endpoint in the same VPC|VPC Interface Gateway|
|||
|AWS side of the VPN|Virtual Private Gateway|
|Customer side of the VPN|Customer Gateway|
|||
|Add new IPs when all IPs in a VPC are used|Add a secondary CIDR range to the VPC (it automatically create a route).|
|Low latency and high throughput for high-performance computing|Elastic Fabric Adapter|
|||
|Web content distribution|Amazon CloudFront|
|Accelerate IP traffic distribution|Global Accelerator|
|DynamoDB Table distribution for multiple region|DynamoDB Global Tables|
|Implement some logic at CDN level (e. g. resize images)|Lambda@Edge|

# Analytics

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|SQL-based analytical queries on S3|Amazon Athena|
|Complex queries on S3 (without coping to Redshift)|Redshift Spectrum|
|Creating data visualizations|Amazon QuickSight|
|||
|Data intensive workload, managed cluster platform for running big data framework (Hadoop, Spark)|Amazon EMR (Elastic MapReduce)|
|Extract, Transform and Load data|AWS Glue|
|Convert files to Apache Parquet|AWS Glue|
|||
|Capture, transform and load data from various sources in **Near Real Time**|Kinesis Data Firehose|
|Capture **Real Time Data** of GBs every second|Kinesis Data Streams|
|Capture Real Time Data for use cases like video playback|Kinesis Video Stream|
|Gather streaming data and run analysis by performing queries (SQL)|Kinesis Data Analytics|

---

### Kinesis

* Kinesis Data Streams has a data retention of up to 365 days.
* Kinesis Data Streams can be used as the source to Kinesis Data Firehose.

# Database

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Graph database, highly connected datasets|Amazon Neptune|
|Time series database for IoT|Amazon Timestream|
|HA and scalable database supporting Cassandra|Amazon Keyspaces|
|Petabyte scale database|Amazon Redshift|
|MongoDB compatible database|Amazon DocumentDB|
|Key-value NoSQL for web apps|Amazon DynamoDB|
|||
|Database connection issues (timeout, rejection)|RDS Proxy|
|Read performance issues|Amazon ElastiCache|
|Cache that support replication and archival|Amazon ElastiCache for Redis|
|Cache that doesn't need advanced functionalities|Amazon ElastiCache for Memcached|

---

### RDS

* RDS only support IO1, it does not support IO2 or IO2express
* Storage autoscaling can be enabled on a running RDS.
* Enable RDS encryption:
  1. Create snapshot
  1. Copy the snapshot with encryption enabled
  1. Restore DB using encrypted snapshot

* RDS Multi AZ Instance:
  * One Primary.
  * One Standby.
  * An RDS Instance can be converted to a Multi-AZ deployment (modify the Instance and specify the Multi-AZ option).

![RDS-Multi_AZ_Instance.png](../../attachments/RDS-Multi_AZ_Instance.png)
Credit: [AWS Doc](https://aws.amazon.com/blogs/database/choose-the-right-amazon-rds-deployment-option-single-az-instance-multi-az-instance-or-multi-az-database-cluster/)

* Multi-AZ DB Cluster: 
  * One Primary.
  * Two Readable Standby.
    * **They are not read replica (as read replica only work in same AZ).**
    * When a failure occurs, RDS performs an automatic failover to the standby.
  * The Reader Endpoint for an Amazon RDS DB cluster provides load-balancing support for read-only connections to the cluster.
  * **Multi-AZ Cluster is not available with MariaDB, Oracle or SQL Server.**

![RDS-Multi_AS_Cluster.png](../../attachments/RDS-Multi_AS_Cluster.png)
Credit: [AWS Doc](https://aws.amazon.com/blogs/database/choose-the-right-amazon-rds-deployment-option-single-az-instance-multi-az-instance-or-multi-az-database-cluster/)

---

### Aurora

* Aurora is Highly Available: 2 copies of data are kept in each AZ with a minimum of 3 AZ.
* Aurora Serverless v2 scales compute capacity automatically based on actual usage, **down to zero when not in use**.

# Storage

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|POSIX file System|Amazon EFS (Elastic File System)|
|Samba, Windows|Amazon FSx for Windows File Server|
|High-performance compute on Linux|Amazon FSx for Lustre|
|||
|Like a NAS on the cloud where NFS or SMB can be used seamlessly|AWS Storage Gateway File Gateway (S3)|
|Like a NAS on the cloud for block storage|AWS Storage Gateway Volume Gateway (EBS)|
|Store **a subset** of on premise data that is frequently accessed|AWS Storage Gateway Volume Cached Volume|
|Store **entire** on premise data that is frequently accessed|AWS Storage Gateway Volume Stored Volume|

### S3

* **Upload object in a single operation: max 5 GB. BUT it is recommended use multipart upload when the object size is > 100MB.**

* **Upload object in parts: max 5 TB.**

* A `DELETE` API call on an object does not delete the actual object, but places a marker on it.

* Only the standard Amazon SQS queue is allowed as an Amazon S3 event notification destination.

* S3 website URL:
  
  * `http://bucket-name.s3-website.Region.amazonaws.com`
  * `http://bucket-name.s3-website-Region.amazonaws.com`
* Amazon S3 Standard stores data in a minimum of three Availability Zones.

* **Glacier Flexible Retrieval:**
  
  * **Expedited (1-5 min) > Standard (3-5 min) > Bulk (5 - 12 hours).**
  * If you delete, overwrite, or transition the object to a different storage class before the 90-day minimum, **you are charged for 90 days**.
*  **Glacier Deep Archive:**
  
  * **Standard (12 hours) > Bulk Retrieval (within 48 hours).**
     -  If you delete, overwrite, or transition the object to a different storage class before the 180-day minimum, **you are charged for 180 days**.

# Migration and Transfer

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Migrate Database|AWS DMS (Database Migration Service)|
|Migrate data (specify data source and destination)|AWS DataSync|
|SFTP, FTPS or FTP and no changes to the customer’s application|AWS Transfer Family|
|||
|Data transfer device and data processing, storage up to 8TB|AWS Snowcone|
|Data transfer device and data processing, storage up to 14TB|AWS Snowcone SSD|
|Data transfer device and data processing, storage up to 80TB|AWS Snowball Edge|

# Machine Learning

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Service that turns text into lifelike speech|Amazon Polly|
|Natural Language Processing (NLP), to uncover valuable insight and connections|Amazon Comprehend|
|Extract text from printed text, handwriting, scanned documents|Amazon Textract|
|Identify objects, people, text, scene and activities image and videos|Amazon Rekognition|

# Security and Compliance

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Store secrets (passwords, AMI IDs, ...), no rotation, low-cost|AWS System Manager Parameter Store|
|Store secret that require automatic rotation, specifically designed for RDS creds or API keys|AWS Secrets Manager|
|||
|Ensure that all objects uploaded to an S3 bucket are encrypted|Update policy to deny if `PutObject` doesn't have the `x-amz-server-side-encryption` header set|
|Find and protect sensitive data from unauthorized access in S3|Amazon Macie|
|||
|URL filtering|AWS Network Firewall|
|Protect against DDoS attack, layer 3, 4 and 7|AWS Shield|
|Protect against injections (SQL, XSS, ...)|AWS WAF|
|||
|Automated vulnerability assessment service (vulnerabilities, and network exposure)|AWS Inspector|
|Intelligent threat detection service (form CloudTrail, VPC Flow Logs, DNS Query Logs)|Amazon GuardDuty|
|Investigate to identify root cause of security issue (from GuardDuty, Macie and Security Hub)|Amazon Detective|

# Manager & Governance

---

### Service / Requirement

|Requirements|Service|
|------------|-------|
|Automated deployment in multi-account environments|Control Tower|
|Share resource with other accounts joined to an organization|AWS Resource Access Manager|
|||
|Input custom values to the template|CloudFormation Parameter|
|Declare output value that can be imported into other stack|CloudFormation Outputs|
|Roll out package installation|AWS System Manager Run Command|
|||
|Performance Metrics|CloudWatch|
|Capture which resource accessed an API|CloudWatch Access Logging|
|Capture user request and response, error traces|CloudWatch Execution Logging|
|Capture info about IP traffic|VPC Flow Log|
|Microservice and Serverless analyze|AWS X-Ray|
|Auditing solution to check API calls (for compliance, governance, ..)|AWS CloudTrail|
|Compliance reports for AWS resources|AWS Artifact|

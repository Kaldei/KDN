---
title: AWS Cheat Sheet SAA-C03
summary: A cheat sheet to study the Solution Architect Associate certification.
description: A cheat sheet to study the Solution Architect Associate certification.
tags:
  - aws
---

# SAA Specific

---

### Design Cost-Optimized Architectures

|Requirement|Service|
|-----------|-------|
|Predictable capacity and uptime requirements|Reserved Instance|
|Sockets and cores capacity|Dedicated Host|

---

### Design Resilient Architectures (Disaster Recovery)

|Requirements|Service|
|------------|-------|
|RPO/RTO happens in real time|Multi Site (Active/Active)|
|RPO/RTO happens in minutes|Warm Standby|
|RPO/RTO happens in minutes, lower cost (RPO in seconds and RTO 5-20 min)|Pilot Light|
|RPO/RTO happens in hours.|Backup and Restore|

# Analytics

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|SQL-based analytical queries on S3|Amazon Athena|
|Complex queries on S3 (without copying to Redshift)|Redshift Spectrum|
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
|Send marketing emails|SES (Simple Email Service)|
|Migration from RabbitMQ|Amazon MQ|

---

### SQS

* SQS and SNS messages are limited to 256KB.
* SQS can retain messages from 1 minute to 14 days.
* The type of queue (Standard or FIFO) must be chosen when the queue is created.

# Compute

---

### EC2

|Requirement|Service|
|-----------|-------|
|Get Instance AMI ID from Metadata|`http://169.254.169.254/latest/meta-data/ami-id`|
|Get Instance Public IP from Metadata|`http://169.254.169.254/latest/meta-data/public-ip`|
|||
|Instance launch type for short workloads, reliable|On Demand Instances|
|Instance launch type for short workloads that can be stopped at any time, cheaper|Spot Instances|
|Instance launch type for long workloads (minimum 1 year)|Reserved Instances|
|Instance launch type for long workloads (minimum 1 year) with flexible instances types|Convertible reserved Instances|
|Instance launch type for use cases that require no other customers use the same hardware|Dedicated Instances|
|Instance launch type for use cases that require an entire physical server (host affinity, licenses that operate at core, CPU socket level)|Dedicated Hosts|

* **AMI IDs are Region specific.**

# Containers

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Running K8s on premise but use AWS-managed service for managing multiple clusters of nodes|EKS Anywhere Installer|
|Connect an EKS Anywhere Cluster to AWS|EKS Connector|

---

### ECS

* ECS Anywhere requires the installation of two agents (these agents register themselves):
  * ECS Agent,
  * SSM Agent.

---

### EKS

* Amazon EKS distribution includes open-source K8S components and few more tools on top of it.

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
|Handle write intensive traffic peak|RDS Proxy|
|Read performance issues|Amazon ElastiCache|
|Cache that support replication, HA, multi AZ failover, archival|Amazon ElastiCache for Redis|
|Cache for multi node partitioning (sharding)|Amazon ElastiCache for Memcached|

---

### RDS

* RDS only support IO1, it does not support IO2 or IO2express
* Storage autoscaling can be enabled on a running RDS.
* Enable RDS encryption:
  1. Create snapshot
  1. Copy the snapshot with encryption enabled
  1. Restore DB using encrypted snapshot

---

### Aurora

* Aurora is Highly Available: 2 copies of data are kept in each AZ with a minimum of 3 AZ.
* Aurora Serverless v2 scales compute capacity automatically based on actual usage, **down to zero when not in use**.

---

### DynamoDB

* DynamoDB is highly scalable.

* There are 2 read types:
  
  * **Query (using Index):** I know what I'm looking for.
  * **Scan:** Scan all the database to find what I'm looking for.
* An Index is composed of 2 keys:
  
  * The **Partition Key** is used to group the data. Data with the same Partition Key is stored together (this allows to query a "partition" in 1 query).
  * The **Sort Key** is optional, it determines the way data with the same Partition Key is stored.
* For better performance, the keys have to be well architected in order to use Queries instead of Scanning the database.

* AWS offers the ability to add a secondary Index (warning, paid by hour).

# Machine Learning

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Service that turns text into lifelike speech|Amazon Polly|
|Natural Language Processing (NLP), to uncover valuable insight and connections|Amazon Comprehend|
|Extract text from printed text, handwriting, scanned documents|Amazon Textract|
|Identify objects, people, text, scene and activities image and videos|Amazon Rekognition|

# Management & Governance

---

### Service / Requirement

|Requirements|Service|
|------------|-------|
|Automated deployment in multi-Account environments|Control Tower|
|Share resource with other Accounts within an Organization|AWS Resource Access Manager|
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
|Auditing solution to check API calls (for compliance, governance, ...)|AWS CloudTrail|
|Compliance reports for AWS resources|AWS Artifact|

---

### AWS Organizations

* **SCP does not affect users or roles in the management account.**
* Service Control Policies (SCP) are similar to IAM permissions policies, but are a feature of AWS Organizations. They can be attached to Roots, OU, or Accounts in an Organization.

# Migration and Transfer

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Migrate Database|AWS DMS (Database Migration Service)|
|Migrate data (specify data source and an AWS managed service as a destination)|AWS DataSync|
|SFTP, FTPS or FTP and no changes to the customer’s application|AWS Transfer Family|
|||
|Data transfer device and data processing, storage up to 8TB|AWS Snowcone|
|Data transfer device and data processing, storage up to 14TB|AWS Snowcone SSD|
|Data transfer device and data processing, storage up to 80TB|AWS Snowball Edge|

* **DataSync is the only option that can transfer metadata and file permissions of files.**

# Networking

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
|Add new IPs when all IPs in a VPC are used|Add a secondary CIDR range to the VPC (it automatically create a route)|
|Low latency and high throughput for high-performance computing|Elastic Fabric Adapter|
|||
|Web content distribution|Amazon CloudFront|
|Accelerate IP traffic distribution|Global Accelerator|
|DynamoDB Table distribution for multiple region|DynamoDB Global Tables|
|Implement some logic at CDN level (e. g. resize images)|Lambda@Edge|

---

### VPC

* **The default NACL in the default VPC allow all traffic in and out.**
* **Security Groups deny all in and allow all out by default.**
* Each subnet has a single Route Table. The VPC and all its subnets are always reachable via the default `local`route (it cannot be modified or removed).
* VPC Peering is not transitive: a VPC cannot use the NAT Gateway of a peered VPC.
* **A VPC cannot reference the security group of a peer VPC that's in a different Region.**
* VPC Endpoint work with Kinesis.
* VPC Endpoint always takes precedence (priority) over NAT Gateway or Internet Gateway.

---

### ELB

* ELB can only balance traffic in one region

---

### CloudFront

* To be able to use an ACM Certificate with CloudFront, the certificate must be requested or imported (third party) in `us-eaast-1` Region.

# Security Identity, and Compliance

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
  reserved c
* Lambda SnapStart for Java (only Java 11 and Java 17) can improve startup performance for latency-sensitive applications by up to 10x at no extra cost with no changes to your function code.

# Storage

---

### Service / Requirement

|Requirement|Service|
|-----------|-------|
|Physical drive attached to an instance|Local Instance Store|
|Network drive that can be attached to only one instance|Amazon EBS (Elastic Block Storage)|
|||
|POSIX file system|Amazon EFS (Elastic File System)|
|High Performance Computing (HPC) Linux file system|Amazon FSx for Lustre|
|High Performance Windows file system (compatible with SMB, NTFS, AD, ...)|Amazon FSx for Windows File Server|
|High Performance ONTAP file system (compatible NFS, SMB, iSCSI)|Amazon FSx for NEtApp ONTAP|
|||
|Like a NAS on the cloud where NFS or SMB can be used seamlessly|AWS Storage Gateway File Gateway (S3)|
|Like a NAS on the cloud for block storage|AWS Storage Gateway Volume Gateway (EBS)|
|Store **a subset** of on premise data that is frequently accessed|AWS Storage Gateway Volume Cached Volume|
|Store **entire** on premise data that is frequently accessed|AWS Storage Gateway Volume Stored Volume|

---

### EBS

|Requirement|Service|
|-----------|-------|
|General purpose SSD volume that go up to 16000 IOPS|EBS GP2 or GP3 (GP3 is more cost-effective)|
|High performance SSD volume|EBS IO1 or IO2|
|Low Cost HDD volume for throughput intensive workloads|EBS ST1|
|Low Cost HDD volume for less frequently accessed workloads|EBS SC1|
|EBS volumes types that can be used as boot volumes|GP2, GP3, IO1, IO2|
|||
|Create a fully initialized at creation volume from snapshot (eliminates latency of I/O when accessing a block for the first time)|EBS Fast Snapshot Restore (FSR)|
|Attach an EBS volume to multiple instance in the same AZ|EBS Multi Attach (only IO1 and IO2)|

---

### S3

|Requirement|Service|
|-----------|-------|
|Read the first 250 bytes of each objects in S3|Use Byte Range Fetch|
|Increase transfer speed of S3 by transferring files through AWS Edge Location|S3 Transfer Acceleration|

* **Upload object in a single operation: max 5 GB. BUT it is recommended use multipart upload when the object size is > 100MB.**

* **Upload object in parts: max 5 TB.**

* IAM roles cannot be assigned to S3 buckets.

* A `DELETE` API call on an object does not delete the actual object, but places a marker on it.

* **Only the standard Amazon SQS queue is allowed as an Amazon S3 event notification destination.**

* S3 website URL:
  
  * `http://bucket-name.s3-website.Region.amazonaws.com`
  * `http://bucket-name.s3-website-Region.amazonaws.com`
* Amazon S3 Standard stores data in a minimum of three Availability Zones.

* SSE-S3 encryption is automatically enabled on new objects stored in S3 (keys are managed by AWS).

* **Glacier Flexible Retrieval:**
  
  * **Expedited (1-5 min) > Standard (3-5 min) > Bulk (5 - 12 hours).**
  * If you delete, overwrite, or transition the object to a different storage class before the 90-day minimum, **you are charged for 90 days**.
*  **Glacier Deep Archive:**
  
  * **Standard (12 hours) > Bulk Retrieval (within 48 hours).**
     -  If you delete, overwrite, or transition the object to a different storage class before the 180-day minimum, **you are charged for 180 days**.

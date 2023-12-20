---
title: AWS Services
summary: A note to briefly introduce AWS services.
description: A note to briefly introduce AWS services.
tags:
  - aws
---

# Security, Identity, & Compliance

![Arch-Category_Security-Identity-Compliance_64.svg](../../attachments/Arch-Category_Security-Identity-Compliance_64.svg)

---

### IAM & STS (Security Token Service)

![Arch_AWS-Identity-and-Access-Management_48.svg](../../attachments/Arch_AWS-Identity-and-Access-Management_48.svg)

IAM is the service used for controlling how users and programs in an AWS account can interact with the AWS API.

---

### Cognito

![Arch_Amazon-Cognito_48.svg](../../attachments/Arch_Amazon-Cognito_48.svg)

Amazon Cognito provides authentication, authorization, and user management for web and mobile apps. 
It can be configured to work with a regular user/password or with a third party identity providers that support SAML or OpenID Connect (e. g. Facebook or Google).

There are two services in Cognito:

* **User Pools (Authentication Service)**: User directories that provide sign-up and sign-in options for your app users. Returns OIDC Tokens.
  * Free under 50000 active users per month.
  * External Provider for federated user pool.
* **Identity Pools (Authorization Service)**: Used to grant access to other AWS services. Return an STS Session (assumed IAM Role) in exchange for a token.
  * Free to use.

---

### Secret Manager

![Arch_AWS-Secrets-Manager_48.svg](../../attachments/Arch_AWS-Secrets-Manager_48.svg)

Secret Manager can store secrets and automatically rotate them.

---

### Macie

![Arch_Amazon-Macie_48.svg](../../attachments/Arch_Amazon-Macie_48.svg)

Amazon Macie is a data security service that uses machine learning (ML) and pattern matching to discover and help protect your sensitive data.

---

### AWS Certificate Manager (ACM)

![Arch_AWS-Certificate-Manager_48.svg](../../attachments/Arch_AWS-Certificate-Manager_48.svg)

AWS Certificate Manager

---

### WAF & Shields

![Arch_AWS-WAF_48.svg](../../attachments/Arch_AWS-WAF_48.svg)

To create a WAF protection, it is required to first create a condition (like `Geo match` for example), and then create a rule using this condition.
After that, create an ACL (Access Control List) with the rule previously created and associate it to the resource to protect (a Load Balancer for example).

Summary: ACL based on a Rule using a Condition.

# Networking and Content Delivery

![Arch-Category_Networking-Content-Delivery_64.svg](../../attachments/Arch-Category_Networking-Content-Delivery_64.svg)

---

### Route 53

![Arch_Amazon-Route-53_48.svg](../../attachments/Arch_Amazon-Route-53_48.svg)

![AWS-Service-Route_53.png](../../attachments/AWS-Service-Route_53.png)
Credit: [Stephane Maarek](https://www.youtube.com/watch?v=10JKpg-eqZU)

---

### VPC (Virtual Private Cloud)

![Arch_Amazon-Virtual-Private-Cloud_48.svg](../../attachments/Arch_Amazon-Virtual-Private-Cloud_48.svg)

VPC stands for Virtual Private Cloud. It's Virtual Network in which to place Virtual Machines. A VPC reside in a Region (this means it is available to all Availability Zones within the Region). 

In order to build a highly available network, it is recommended to deploy it in at least two Availability Zones.

---

### CloudFront (CDN)

![Arch_Amazon-CloudFront_48.svg](../../attachments/Arch_Amazon-CloudFront_48.svg)

CloudFront improves performance for both cacheable content (such as images and videos) and dynamic content (such as API acceleration and dynamic site delivery).

CDN with over 160 points of presence. Creating a distribution takes around 10-15 min.

Only outgoing bandwidth is charged (and CloudFront's costs around 10-15% less than S3's).

---

### Global Accelerator

![Arch_AWS-Global-Accelerator_48.svg](../../attachments/Arch_AWS-Global-Accelerator_48.svg)

Global Accelerator improves performance for a wide range of applications over TCP or UDP by proxying packets at the edge to applications running in one or more AWS Regions.

Use cases: 

* Good fit for non-HTTP use cases, such as gaming (UDP), IoT (MQTT), or Voice over IP.
* Good for HTTP use cases that require static IP addresses.
* Good for HTTP use cases that required deterministic, fast regional failover.

---

### ELB (Elastic Load Balancer)

![Arch_Elastic-Load-Balancing_48.svg](../../attachments/Arch_Elastic-Load-Balancing_48.svg)

ELB is a managed load balancer (by AWS).
It costs more than a self-managed load balancer, but it is effortless to manage.

ELB allows "Sitckiness" (Session Affinity): a user will end up using the same instance.

---

### Network ACL vs Security Group

![AWS-Service-NACL_Security_Group.png](../../attachments/AWS-Service-NACL_Security_Group.png)

#### Network ACL

A NACL is bound to a Subnet. It only applies (evaluate a packet) when crossing a subnet.

A Security group is **Stateless** (check very packets that cross border).

* Stateless firewall
* Access Control In
* Access Control Out

The `Defaut Network ACL` of an AWS allows all inbound and outbound traffic

#### Security Group

A Security Group is bound to an ENI (Elastic Network Interface). It applies to check if packets can reach specific instances or not:

* Protocol (UDP or TCP),
* Port Range,
* Source.

**The source can be another Security Group!** 

A Security group is **Stateful**.

* Stateful firewall,
* Deny all Inbound traffic by default,
* Allow all Outbound traffic by default,
* Can only create "Allow" rules.

# Compute

![Arch-Category_Compute_64.svg](../../attachments/Arch-Category_Compute_64.svg)

---

### Lightsail

![Arch_Amazon-Lightsail_48.svg](../../attachments/Arch_Amazon-Lightsail_48.svg)

Little virtual servers stacks for simple websites, or development/tests environments.

OS available : Amazon Linux, Ubuntu, Debian, FreeBSD, Windows Server
Stacks available : Node.js, GitLab, LAMP, Nginx, Django, ...

---

### EC2 (Elastic Compute Cloud)

![Arch_Amazon-EC2_48.svg](../../attachments/Arch_Amazon-EC2_48.svg)

EC2 stands for Elastic Compute Cloud. It's the same as Lightsail, but with more options and features.

Note: to give a name to an instance, add a Tag with the key `Name`.

---

### Lambda (Serverless Function)

![Arch_AWS-Lambda_48.svg](../../attachments/Arch_AWS-Lambda_48.svg)

AWS Lambda is a serverless function.

---

### Beanstalk

![Arch_AWS-Elastic-Beanstalk_48.svg](../../attachments/Arch_AWS-Elastic-Beanstalk_48.svg)

With given code and configuration settings, Elastic Beanstalk deploys the resources necessary (EC@, QSG,ELB, RDS, ...) to perform the following tasks:

* Adjust capacity
* Load balancing
* Automatic scaling
* Application health monitoring

# Containers

![Arch-Category_Containers_64.svg](../../attachments/Arch-Category_Containers_64.svg)

---

### ECS (Elastic Container Service)

![Arch_Amazon-Elastic-Container-Service_48.svg](../../attachments/Arch_Amazon-Elastic-Container-Service_48.svg)

Container orchestrator made by Amazon.
Containers can be run on AWS Fargate (serverless), EC2 instances or ECS Anywhere (External Instance)

Terminology:

* Service: containers designed to run continuously (equivalent to a Pod in Kubernetes?).
* Task: a container that will execute a task and then stop.

---

### EKS (Elastic Kubernetes Service)

![Arch_Amazon-Elastic-Kubernetes-Service_48.svg](../../attachments/Arch_Amazon-Elastic-Kubernetes-Service_48.svg)

Container orchestrator Kubernetes.

---

### Fargate (Serverless Compute Engine)

![Arch_AWS-Fargate_48.svg](../../attachments/Arch_AWS-Fargate_48.svg)

Fargate is a serverless compute engine for containers (uses ECS and EKS).

# Storage

![Arch-Category_Storage_64.svg](../../attachments/Arch-Category_Storage_64.svg)

---

### S3 (Simple Storage Service)

![Arch_Amazon-Simple-Storage-Service_48.svg](../../attachments/Arch_Amazon-Simple-Storage-Service_48.svg)

S3 (Simple Storage Service) is a file storage service accessible via HTTP and HTTPS requests.

It's an **object** storage: when there is a change to the object, the entire file must be re-uploaded.

---

### EBS (Elastic Bock Store)

![Arch_Amazon-Elastic-Block-Store_48.svg](../../attachments/Arch_Amazon-Elastic-Block-Store_48.svg)

#### Basis

Amazon Elastic Block Store is a service that provides block-level storage volumes that you can use with Amazon EC2 instances. If you stop or terminate an Amazon EC2 instance, all the data on the attached EBS volume remains available.

**Block storage** breaks files in small blocks: when a change is made to the file, only modified blocks are re-uploaded.

Multi Attach EBS max to 16 instances.

#### EBS FSR

Amazon EBS Fast Snapshot Restore (FSR) enables you to create a volume from a snapshot that is fully initialized at creation. This eliminates the latency of I/O operations on a block when it is accessed for the first time.

---

### EFS (Elastic File System)

![Arch_Amazon-EFS_48.svg](../../attachments/Arch_Amazon-EFS_48.svg)

EFS (Elastic File System) allows you to have multiple EC2 instances accessing data at the same time.

---

### AWS Backup

![Arch_AWS-Backup_48.svg](../../attachments/Arch_AWS-Backup_48.svg)

AWS Backup is a simple and cost-effective way to protect your data by backing up your Amazon EFS file systems. Amazon EFS is natively integrated with AWS Backup.

---

### S3 vs EBS vs EFS

#### S3 vs EBS

S3:

* When using complete objects or occasional changes.

EBS: 

* When using complex read, write change functions.

#### EBS vs EFS

EBS: 

* It's a volume attached to EC2 instances.
* Availability Zone level resource (requires to be in the same AZ as the EC2 instances to be attached to it).

EFS: 

* Multiple instances can read and write at the same time.
* Linus file system (like NFS).
* It's a regional resource.
* Automatically scales?

# Database

![Arch-Category_Database_64.svg](../../attachments/Arch-Category_Database_64.svg)

---

### RDS (Relational Database Service)

![Arch_Amazon-RDS_48.svg](../../attachments/Arch_Amazon-RDS_48.svg)

RDS stands for Relational Database Service.
Available databases are: AWS Aurora (MySQL Compatible), AWS Aurora (PostgreSQL Compatible), MySQL, MariaDB, PostgreSQL, Oracle and Microsoft SQL Server.

---

### Amazon Aurora (Relational Database)

![Arch_Amazon-Aurora_48.svg](../../attachments/Arch_Amazon-Aurora_48.svg)

Aurora is a cloud optimized database service from AWS (proprietary tech).
Available databases are: MySQL and PostgreSQL.

Cost 20% more than RDS, but it is more efficient and comes with functionalities like:

* storage automatically grows (10Gb to 64 TB),
* data replication (up to 15 replicas),
* backup to S3,
* high availability (with failover instantaneous),
* point-in-time recovery (Backtrack),
* can't ssh.

![AWS-Aurora-Read_scaling.png](../../attachments/AWS-Aurora-Read_scaling.png)
Credit: Stephane Maarek

---

### DynamoDB (NoSQL Database)

![Arch_Amazon-DynamoDB_48.svg](../../attachments/Arch_Amazon-DynamoDB_48.svg)

Amazon DynamoDB(opens in a new tab) is a key-value database service. It delivers single-digit millisecond performance at any scale.
DynamoDB is serverless, which means that you do not have to provision, patch, or manage servers.

---

### Amazon Redshift (Data Warehouse)

![Arch_Amazon-Redshift_48.svg](../../attachments/Arch_Amazon-Redshift_48.svg)

Amazon Redshift is a data warehousing service that you can use for big data analytics. It offers the ability to collect data from many sources and helps you to understand relationships and trends across your data.

---

### DMS (Database Migration Service)

![Arch_AWS-Database-Migration-Service_48.svg](../../attachments/Arch_AWS-Database-Migration-Service_48.svg)

AWS DMS, allows moving data between a source database and a target database. The source and target databases can be of the same type or different types. 

The source can be a database on premise, an EC2 or an RDS. 
The target can be an EC2 or an RDS.

During the migration, your source database remains operational, reducing downtime for any applications that rely on the database.

**AWS Migration Hub** can be used to track the progress of migrations.

Uses cases:

* Database migration (to the cloud).
* Development and test database migration (copy production database to test database).
* Database consolidation (migrate multiple databases into one).
* Continuous database replication (disaster recovery or geographic separation).

---

### Other Databases

* **Amazon DocumentDB:** a document database service that supports MongoDB workloads.

* **Amazon Neptune:** a graph database service. For building and running applications that work with highly connected datasets, such as recommendation engines, fraud detection, and knowledge graphs.

* **Amazon QLDB (Amazon Quantum Ledger Database):** a ledger database service. For reviewing a complete history of all the changes that have been made to your application data.

* **Amazon Managed Blockchain:** a service that can be used to create and manage blockchain networks with open-source frameworks. Blockchain is a distributed ledger system that lets multiple parties run transactions and share data without a central authority.

* **Amazon ElastiCache:** a service that adds caching layers on top of databases to help improve the read times of common requests. It supports two types of data stores: Redis and Memcached.

* **Amazon DAX (DynamoDB Accelerator):** an in-memory cache for DynamoDB. It helps improve response times from single-digit milliseconds to microseconds.

# Application Integration

![Arch-Category_Application-Integration_64.svg](../../attachments/Arch-Category_Application-Integration_64.svg)

---

### SQS (Simple Queue Service)

![Arch_Amazon-Simple-Queue-Service_48.svg](../../attachments/Arch_Amazon-Simple-Queue-Service_48.svg)

Send, store, receive messages at any volume.
SQS queues are where messages are places until they are consumed.

---

### SQS (Simple Notification Service)

![Arch_Amazon-Simple-Notification-Service_48.svg](../../attachments/Arch_Amazon-Simple-Notification-Service_48.svg)

Similar to SQS, but can send notification to end users (publish/subscribe mode).
An SNS topic is a channel for messages to be deliverd.

# Analytics

---

### Kinesis

![Arch_Amazon-Kinesis_48.svg](../../attachments/Arch_Amazon-Kinesis_48.svg)

Collect, process, and analyze real-time data streams.

---

### Kinesis vs SQS FIFO

#### Kinesis Data Stream

Ordering Data with Kinesis is done by distributing data in the multiple shards available resulting in a kind of FIFO.

![AWS-Service-Kinesis-Ordering_Data.png](../../attachments/AWS-Service-Kinesis-Ordering_Data.png)

#### SQS FIFO

In a SQS FIFO only one customer can be set if no Group IDs are configured.

Using a Group ID result in a similar approach to Kinesis. The key difference is that in order to add a customer it is necessary to add a Group ID (in Kinesis it is necessary to add shards, which cost more).

![AWS-Service-SQS-FIFO.png](../../attachments/AWS-Service-SQS-FIFO.png)

# Management & Governance

![Arch-Category_Management-Governance_64.svg](../../attachments/Arch-Category_Management-Governance_64.svg)

---

### CloudWatch (Logs)

![Arch_Amazon-CloudWatch_48.svg](../../attachments/Arch_Amazon-CloudWatch_48.svg)

Metrics and logs about resources. 
These metrics can be used to create Dashboards and Alarms.

---

### CloudTrail

![Arch_AWS-CloudTrail_48.svg](../../attachments/Arch_AWS-CloudTrail_48.svg)

CloudTrail records API calls for your account (useful for auditing). 
The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller, ...

---

### Trusted Advisor

![Arch_AWS-Trusted-Advisor_48.svg](../../attachments/Arch_AWS-Trusted-Advisor_48.svg)

Trusted Advisor gives recommendation on our AWS resources: 

* Cost optimization
* Performance
* Security
* Fault tolerance
* Service limits

---

### CloudFormation

![Arch_AWS-CloudFormation_48.svg](../../attachments/Arch_AWS-CloudFormation_48.svg)

CloudFormation is a service to automate deployment of AWS resources. It is an IaC tool using JSON or YAML files.

Note: In CloudFormation, all actions are resources (including actions to attach items to each other).

 

---

### Service Catalog

![Arch_AWS-Service-Catalog_48.svg](../../attachments/Arch_AWS-Service-Catalog_48.svg)

AWS Service Catalog allows you to create and manage catalogs of IT services that can be deployed within your organization. 

With Service Catalog, you can define a standardized set of products (solutions and tools in this case) that customers can self-service provision. By creating Service Catalog products, you can control and enforce the deployment of approved and validated solutions and tools.

---
title: AWS CLI
summary: A note about the AWS CLI.
description: A note about the AWS CLI.
tags:
  - aws
---

# Basis

---

### Command Structure


 > 
 > **<font color=red>aws</font> serviceName commands**
 > General structure of a command.

 > 
 > **<font color=red>--region </font>us-east-1**</br>
 > Set the region for this command (change from default).
 > 
 > **<font color=red>--no-sign-request</font>**</br>
 > Access to public objects (no signing in).
 > 
 > **<font color=red>--profile</font> myProfile**</br>
 > Set profile ot use for this command (change from default).

---

### Profile Configuration

https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html

Profile configuration are stored in two files:

* `~/.aws/config` 

````toml
[default]
region=eu-west-1
output=json
````

* `~/.aws/credentials`

````toml
[default]
aws_access_key_id=[ACCESS_KEY_ID]
aws_secret_access_key=[SECRET_ACCESS_KEY]
````

 > 
 > **<font color=red>aws configure list-profiles</font>**</br>
 > List created profiles.

 > 
 > **<font color=red>aws configure --profile</font> myProfileName**</br>
 > Create or modify a profile.
 > 
 > **<font color=red>aws configure set aws_session_token</font> MY_AWS_SESSION_TOKEN <font color=red>--profile</font> myProfileName**</br>
 > Set a `AWS_SESSION_TOKEN` (after `aws configure`).
 > 
 > **<font color=red>aws configure list  --profile</font> myProfileName<font color=red></font>**</br>
 > Show details credentials.

---

### Query

aws glue get-jobs --query 'Jobs\[? WorkerType==`Standard`\].{a_JobName:Name,b_WorkerType:WorkerType,c_MaxCapacity:MaxCapacity,d_MaxConcurrentRuns:ExecutionProperty.MaxConcurrentRuns}' --out table

# IAM

---

### Basis


 > 
 > **<font color=red>aws sts get-access-key-info --access-key-id</font> \[AKIA_EXAMPLE\]**</br>
 > Return Account ID of the access key.

 > 
 > **<font color=red>aws sts get-caller-identity --profile</font> myProfileName**</br>
 > Return User ID, Account ID, and ARN of the selected profile.
 > 
 > ````json
 > {
 >    "UserId": "AIDATAAH6Q3WAYKDXJV5B",
 >    "Account": "206175110892",
 >    "Arn": "arn:aws:iam::206175110892:user/myUserName"
 > }
 > ````

---

### Roles


 > 
 > **<font color=red>aws sts assume-role --role-arn</font> \[MY_ARN\] <font color=red>--role-session-name</font> mySessionName**</br>
 > Assume a role based on the ARN.

# Cognito

---

### Basis


 > 
 > **<font color=red>aws cognito-identity get-id --identity-pool-id</font> \[MY_IDENTOTY_POOL_ID\]**</br>
 > Return the Cognito ID for the specified identity pool ID.
 > 
 > ````json
 > {
 >    "IdentityId": "us-east-1:1b0bcc16-b32f-44c1-8f1e-14e8d4c5f7af"
 > }
 > ````

# EC2

---

### Basis


 > 
 > **<font color=red>aws ec2 describe-instances --output text --profile</font> myProfileName**</br>
 > Listing all EC2 instances running within a profile.

# Lambda

---

### Basis


 > 
 > **<font color=red>aws lambda invoke --function-name</font> my-lambda**</br>
 > Execute a Lambda.

# S3

---

### Basis


 > 
 > **<font color=red>aws s3 mb s3://</font>myBucketURL**</br>
 > Create a bucket (mb = make bucket).

 > 
 > **<font color=red>aws s3 ls</font>**</br>
 > Return all buckets for the current profile.
 > 
 > **<font color=red>aws s3 ls s3://</font>myBucketURL**</br>
 > Return bucket contents (can also be reached at `https://myBucketName.s3.amazonaws.com`).

 > 
 > **<font color=red>aws s3api put-bucket-policy s3://</font>myBucketURL myPolicyFile**</br>
 > Add policy config file to the bucket.
 > 
 > **<font color=red>aws s3api put-bucket-website s3://</font>myBucketURL myIndexFile**</br>
 > Sets the default file to be served when using the bucket as a static web server.

 > 
 > **<font color=red>aws s3 cp s3://</font>myBucketURL/myFile ./**</br>
 > Copies a bucket file to my current local directory.
 > 
 > **<font color=red>aws s3 sync</font> myFile <font color=red>s3://</font>myBucketURL**</br>
 > Synchronize a local file or directory to the buckets. 
 > 
 > **<font color=red>aws s3 sync s3://</font>myBucketURL/myFolder /myLocalFolder**</br>
 > Synchronize bucket folder to local directory/

# DynamoDB

---

### Basis


 > 
 > **<font color=red>aws dynamodb list-tables</font>**</br>
 > List tables.

 > 
 > **<font color=red>aws dynamodb describe-table --table-name</font> my-table**</br>
 > Return information about selected table.
 > 
 > **<font color=red>aws dynamodb scan --table-name</font> my-table**</br>
 > Return items (and their attributes) stored in the selected table.

# CloudWatch

---

### Basis


 > 
 > **<font color=red>aws logs describe-log-streams --log-group-name</font>  my-log-group**</br>
 > Retrieve information about log streams in a specific log group.

 > 
 > **<font color=red>aws logs get-log-events --log-group-name</font> my-log-group <font color=red>--log-stream-name</font> some-log-stream**</br>
 > Retrieve log events from a log stream in a specific log group.

# Security Hub

---

### Basis


 > 
 > **<font color=red>aws securityhub enable-security-hub --no-enable-default-standards --control-finding-generator SECURITY_CONTROL</font>**</br>
 > Enable Security Hub with no Standards enabled by default, and findings are generated based on Controls (only one finding if the controls exist in multiple Standards).

---

### Standards


 > 
 > **<font color=red>aws securityhub describe-standards</font>**</br>
 > List available Standards (packs of controls like CIS or NSIT) and whether they're enabled or not.
 > 
 > **<font color=red>aws securityhub get-enabled-standards</font>**</br>
 > List enabled Standards.

 > 
 > **<font color=red>aws securityhub batch-enable-standards --standards-subscription-requests '</font>{"arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0"}<font color=red>'</font>**</br>
 > Enable a Standard using it's ARN.

 > 
 > **<font color=red>aws securityhub describe-standards-controls --standards-subscription-arn</font> arn:aws:securityhub:eu-west-1:123456789123:subscription/cis-aws-foundations-benchmark/v/1.2.0**</br>
 > List control in a standard, and show whether they are enabled or not.

---

### Controls


 > 
 > **<font color=red>aws securityhub list-security-control-definitions</font>**</br>
 > List Security Controls IDs (and description ...).
 > 
 > **<font color=red>aws securityhub list-security-control-definitions --standards-arn</font> "arn:aws:securityhub:us-east-1::standards/cis-aws-foundations-benchmark/v/1.4.0"**</br>
 > List Security Controls IDs (and description ...) of the specified Standards.

 > 
 > **<font color=red>aws securityhub list-standards-control-associations --security-control-id</font> CloudTrail.1**</br>
 > List Standards that cover the given Control (ControlId). **This will only return Controls that belong in an enabled Standard**.
 > 
 > **<font color=red>aws securityhub batch-get-standards-control-associations --standards-control-association-ids \[{"SecurityControlId": "</font>ACM.1<font color=red>", "StandardsArn": "</font>arn:aws:securityhub:::ruleset/cis-aws-foundations-benchmark/v/1.2.0"<font color=red>},</font> ...<font color=red>\]</font>**</br>
 > For a given Control return associated Standards Controls (with ARNs) for the specified standard.

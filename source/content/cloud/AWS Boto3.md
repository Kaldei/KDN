---
title: AWS Boto3
summary: A note about the AWS Boto3 (Python SDK).
description: A note about the AWS Boto3 (Python SDK).
tags:
  - aws
  - python
---

# S3

---

### Basis


````py
import boto3

s3_client = boto3.client('s3')
````

---

### Object

#### Get Object (JSON)

````py
response = s3_client.get_object(Bucket = 'myBucketName', Key = 'myFile.txt')

fileContent = json.loads(response['Body'].read())
````

#### Put Object (JSON)

````py
s3_client.put_object(Bucket = 'myBucketName', Key = 'myFile.txt', Body = json.dumps('{...}'), ContentType = 'application/json')
````

# DynamoDB

---

### Basis


````py
import boto3

dynamodb_client = boto3.client('dynamodb')
````

---

### Query


````py
response = dynamodb_client.query(
  TableName = "tableName",

  # Use when atribute is a reserved word, contains dot or begins with number
  ExpressionAttributeName = {
    '#myAttribute': 'myAttributeName'
  },
  # Attribute to recieve when reading (kind of SELECT column)
  ProjectionExpression = "#myAttribute"


  # Same as ExpressionAttributeName but for values in used in comparaison
  ExpressionAttributeValues = {
  ':myNumberMax': 12
  },
  # Condition for the query (kind of WHERE condition)
  KeyConditionExpression = Key('#myAttribute').gt(':myNumberMax')
)

# All Items
items = response['Items']
# Specific Item
items = response['Items'][0]['myCategory']['S']
````

# SSM

---

### Basis


````py
import boto3

ssm_client = boto3.client("ssm")
````

---

### Parameter

#### Get Parameter

````py
response = ssm_client.get_parameter(Name='myParameterName')

parameterValue = response['Parameter']['Value']
````

#### Put Parameter

````py
ssm_client.put_parameter(Name="myParameterName", Value="myValue", Type='String', Overwrite=True)
````

# Security Hub

---

### Basis


````py
import boto3

ssm_securityhub = boto3.client('securityhub')
````

---

### Controls

#### List Security Control IDs

````py
paginator = securityhub.get_paginator('list_security_control_definitions')

controlsIds = paginator.paginate().search("SecurityControlDefinitions[].SecurityControlId")
````

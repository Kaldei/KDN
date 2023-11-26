---
tag: terraform aws
---

# Basis

---

### Provider


````hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.8.0"
    }
  }

  required_version = ">= 5.8.0"
}

provider "aws" {
  region  = "us-east-1"
}
````

# Compute

---

## EC2 Instance


````hcl
resource "aws_instance" "my_instance" {
  ami           = "ami-830c94e3"
  instance_type = "t2.micro"
  count         = 3              # Number of instances to deploy
  

  tags = {
    Name = "ExampleAppServerInstance"
  }
}
````

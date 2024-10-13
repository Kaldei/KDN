---
title: Kubernetes Cloud Managed
summary: A note about the spceifics of Kubernetes managed by Cloud Providers.
description: A note about the spceifics of Kubernetes managed by Cloud Providers.
tags:
  - kubernetes
  - aws
---

# Comparison

---

### AWS vs GCP vs Azure

* Metrics Server
  * Azure AKS and Google GKE comes with Metrics Server by default.
  * AWS EKS does not come with Metrics Server by default.
* Node Autoscaler
  * In AWS it is required to configure permissions and deploy the autoscaler (Auto Scaling Group)
  * In Azure and GCP, the cluster autoscaler is managed (it just needs to be enabled).
* Node Types 
  * EKS
    * Self-managed
    * Managed node groups
    * Fargate

# AWS EKS IAM

---

### Cluster

#### Assume Role

````json
{
	...
	"Principal": {
		"Service": "eks.amawonaws.com"
	}
}
````

#### Policy

For cluster using legacy Cloud Controller : `arn:aws:iam::aws:policy/AmazonEKSClusterPolicy`. Grant required permissions + ELB permission for legacy Ingress (half of the policy).

---

### Worker Nodes Policies

* `arn:aws:iam::aws:policy/AmazonEKSWoekerNodePolicy`: core EC2 permissions + required permission for Pod Identity Agent.
* `arn:aws:iam::aws:policy/AmazonEKS_CNI_Policy`: permission to modify IP address config of pods.
* `arn:aws:iam::aws:policy/AmawonEC2ContainerRegistryReadOnly`: allows to pull container images from ECR.

---

### Pod Identity Assume Role


````json
{
	...
	"Principal": {
		"Service": "pods.eks.amawonaws.com"
	}
}
````

---

### Admin Access Policy

Add `AmazonEKSClusterAdmin` to IAM Access entries in order to create and get any resources in the cluster.

# AWS Load Balancer Controller

---

### Prerequisites

The AWS LBC is not installed by default on EKS, it needs to be installed (https://aws.github.io/eks-charts/aws-load-balancer-controller).

---

### AWS NLB

Creates an NLB (Layer 4 Load Balancer).
This Load Balancer can be configured with specific [annotations](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.8/guide/service/annotations/). 

#### Configuration

````yml
# New configuration (eks >= v1.22)
king: Service
spec:
	type: LoadBalancer
	loadBalancerClass: nlb
````

````yml
# Old configuration
king: Service
spec:
	type: LoadBalancer
annotations: 
	service.beta.kubernetes.io/aws-load-balancer-type: external
````

#### Annotations

Here are some annotations that could be usefull:

````yml
metadata:
  annotations:
    # Use Instance mode
    service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: instance
    # Use IP mode
    service.beta.kubernetes.io/aws-load-balancer-nlb-target-type: ip

	# Configure a Load Balancer with public IP address
    service.beta.kubernetes.io/aws-load-balancer-scheme: internet-facing

	# Configure a Load Balancer with only a private IP address (accessible only in the VPC).
    service.beta.kubernetes.io/aws-load-balancer-scheme: internal

````

---

### Legacy Classic LB

If the AWS Load Balancer Controller is not installed or the `aws-load-balancer-type` annotation **is not set to** `nlb-ip` or `external`, AWS will use the [Legacy Load Balancer](https://kubernetes-sigs.github.io/aws-load-balancer-controller/v2.8/guide/service/annotations/#legacy-cloud-provider) and deploy an AWS Classic Load Balancer.

#### Configuration

````yml
king: Service
spec:
	type: LoadBalancer
````

---

### Ingress (ALB)

AWS Ingress, creates an ALB (Layer 7 Load Balancer). 
This Load Balancer understand TLS and will terminate it when passing traffic to the cluster. 

* [Anton Putra - Expose Kubernetes Services Running on Amazon EKS (9 Ways)](https://www.youtube.com/watch?v=ePqUq06WoLk&list=PLiMWaCMwGJXkbN7J_j3qFEZVBacdoYCPJ&index=15)
* [Anton Putra - Native EKS Ingress: AWS Load Balancer Controller](https://www.youtube.com/watch?v=ZfjpWOC5eoE)

#### Configuration

````yml
king: Ingress
spec:
	ingressClassName: alb
````

#### Annotations

Here are some annotations that could be usefull:

````yml
metadata:
  annotations:
    # Listen on ports 80 and 443
    alb.ingress.kubernetes.io/listen-ports: '[{"HTTP:80}, {"HTTPS":443}]'
    # Redirect HTTP traffic to HTTPS
    alb.ingress.kubernetes.io/ssl-redirect: 443

    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/target-type: ip

	# Set a custom healthcheck path
	alb.ingress.kubernetes.io/healthcheck-path: /health
````

# AWS EBS CSI Driver

Driver to enable the cluster to create EBS storage on AWS.

---

### EBS

Default Storage Class is GP2. The access mode is `ReadWriteOnce`, which allows the EBS volume to be mounted only to one pod (one node).

````yml
apiVersion: v1
kind: PersistantVolume
spec:
	volumeMode: Filesystem
	accessModes: [ReadWrtieOnce]
	storageCapacity: 5Gi
````

---

### EFS

This can be mounted to multiple pods.

````yml
apiVersion: v1
kind: PersistantVolumeClaim
spec:
	storageClassName: efs
	accessModes: [ReadWrtieMany]
	resources:
		requests
			storage: 5Gi
````

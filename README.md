# Terraform AWS Infrastructure

## Overview

Implement production ready highly available, scalable and resilient AWS 
infrastructure using Terraform.

### Infrastructure

* Defines Remote State Configuration
* Creates a VPC
* Creates Public and Private Subnets across three region AZN's
* Creates Route Tables for public and private routes
* Associates the route tables with subnets
* Creates a NAT Gateway and adds it to the route table
* Creates an Elastic IP for the NAT gateway
* Creates and adds an Internet Gateway to the route table
* Outputs Remote State Variables

### Instances

* Defines Backend Remote State and reads remote state from Infrastructure
* Creates Security Groups for EC2 Instances and ELB
* Creates an IAM Role and AM Role Policy for EC2 Instances
* Creates an IAM Instance Profile
* Uses latest available AMI for EC2 Instances
* Creates a launch configuration for Public and Private EC2 Instances
* Creates Load Balancers for the Public Web App and Private Backend App
* Creates Auto-Scaling Groups for Public and Private EC2 Instances
* Creates Auto-Scaling Policies for Public and Private EC2 Instances
* Creates SNS Topics and Subscription for SMS Auto-Scaling Notifications
* Defines Auto-Scaling Notifications to trigger events

## Requirements

Requires a key-pair to connect to the launched EC2 instances in addition to 
standard AWS access privileges.

## Setup

From the project root directory run the following commands.

```shell
$ cd infrastructure/
$ terraform init -backend-config="infrastructure-prod.config"
$ terraform plan -var-file="production.tfvars"
$ terraform apply -var-file="production.tfvars"

$ cd ../instances/
$ terraform init -backend-config="backend-prod.config"
$ terraform plan -var-file="production.tfvars"
$ terraform apply -var-file="production.tfvars"
```

## Teardown

From the project root directory run the following commands to destroy 
the AWS instances and infrastructure. 

```shell
$ cd instances/
$ terraform destroy -var-file="production.tfvars"

$ cd ../infrastructure/
$ terraform destroy -var-file="production.tfvars"
```

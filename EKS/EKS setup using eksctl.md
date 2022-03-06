# Elastic Kubernetes Service (Amazon EKS cluster setup using ***eksctl***)

## Prerequisites

* Before starting this tutorial, you must install and configure the following tools and resources that you need to create and manage an Amazon EKS cluster.

1. ***eksctl*** - A command line utility for creating and managing Kubernetes clusters on AWS.

2. ***AWS CLI*** – A command line tool for working with AWS services, including Amazon EKS. This guide requires that you use version 2.2.5 or later or 1.19.75 or later. For more information, see Installing, updating, and uninstalling the AWS CLI in the AWS Command Line Interface User Guide. After installing the AWS CLI, we recommend that you also configure it. For more information, see Quick configuration with aws configure in the AWS Command Line Interface User Guide.

3. ***kubectl*** – A command line tool for working with Kubernetes clusters. This guide requires that you use version 1.20 or later. For more information, see Installing kubectl.

4. ***Required IAM permissions*** – The IAM security principal that you're using must have permissions to work with Amazon EKS IAM roles and service linked roles, AWS CloudFormation, and a VPC and related resources. For more information, see Actions, resources, and condition keys for Amazon Elastic Container Service for Kubernetes and Using service-linked roles in the IAM User Guide. You must complete all steps in this guide as the same user.

## Configure AWS credentials

Before configuring aws credential you have to create a user or add user to a group

### Set up a Group

Set up a group with the Permissions of:

1. AmazonEC2FullAccess
2. IAMFullAccess
3. AWSCloudFormationFullAccess

You also need to create an inline policy, using the following:

```sh
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "eks:*",
      "Resource": "*"
    },
    {
      "Action": [
        "ssm:GetParameter",
        "ssm:GetParameters"
      ],
      "Resource": "*",
      "Effect": "Allow"
    }
  ]
}
```

### Add a user to the group

Use the console to add a user to your new group, and then use "aws configure" to input the credentials

Configure the AWS credentials using the below command

```sh
aws configure
```

## Start Your Cluster

```sh
eksctl create cluster --name <CLUSTER_NAME> --nodes-min=<NO_OF_WORKER_NODES_IN NUMERIC>
```

---
title: AWS CLI
sidebar: mydoc_sidebar
permalink: aws_cdk.html
folder: aws
---

### ASW Cloud Development Kit (CDK)

- Define your cloud infrastructure using a familiar language:
  - Javascript / TypeScript, Python, Java and .NET
- Contains high level components called constructs
- The code is compiled into a CloudFormation template (YAML/JSON)
- You can therefore **deploy infrastructure and application runtime code together**
  - Great for Lambda functions
  - Great for Docker containers in ECS/EKS
  - {% include image.html file="cdk.png" %}

### CDK in a diagram
  - {% include image.html file="cdk2.png" %}

### CDK vs SAM
  - SAM:
    - Serverless focused
    - Write your template declaratively in JSON or YAML
    - Great for quickly getting started with Lambda
    - Leverages CloudFormation
  - CDK:
    - All AWS services
    - Write infra in a programming language JavaScript/TypeScript, Python, Java and .NET
    - Leverages CloudFormation

### CDK Hands-On
  - {% include image.html file="cdk3.png" %}

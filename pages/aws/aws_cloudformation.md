---
title: AWS CloudFormation
sidebar: mydoc_sidebar
permalink: aws_cloudformation.html
folder: aws
---

### CloudFormation Overview

#### Infrastructure as Code
  - Currently, we have been doing a lot of manual work
  - All this manual work will be very tough to reproduce:
    - In another region
    - In another AWS account
    - Within the same region if everything was delete
  - Wouldn't it be great if all our infrastructure was ... code?
  - That code would be deployed and create/ update/ delete our infrastructure

#### What is CloudFormation
  - CloudFormation is a declarative way of outlining your AWS Infrastructure for any resources (most of them are supported)
  - For example, within a Cloudformation template, you say:
    - I want a security group
    - I want two EC2 machines using this security group
    - I want two Elastic IPs for these EC2 machines
    - I want an S3 bucket
    - I want a load balancer(ELB) in front of these machines

  - Then Cloudformation creates those for you, in the **right order** with the **exact configuration** that you specify

#### Benefits of AWS CloudFormation (1/2)
  - Infrastructure as code
    - No resources are manually created, which is excellent for control
    - The code can be version controlled for example using git
    - Changes to the infrastructure are reviewed through code

  - Cost
    - Each resources within the stack is stacked with an identifier so you can easily see how much a stack costs you
    - You can estimate the costs of your resources using the CloudFormation template
    - Savings strategy: In Dev, you could automation deletion of templates at 5 PM and recreated at 8 AM, safely

#### Benefit of AWS CloudFormation (2/2)
  - Productivity
    - Ability to destroy and re-create an infrastructure on the cloud on the fly
    - Automated generation of Diagram for your templates!
    - Declarative programming (no need to figure out ordering and orchestration)

  - Separation of concern: create many stacks for many apps, and many layers.Ex:
    - VPC stacks
    - Network stacks
    - App stacks

  - Don't re-invent the wheel
    - Leverage existing templates on the web!
    - Leverage the documentation!

#### How CloudFormation Works
  - Template have to be uploaded in S# and then referenced in CloudFormation
  - To update a template, **we can't edit previous ones**. We have to re-upload a new version of the template to AWS
  - Stacks are identified by a name
  - **Deleting a stack deletes every single artifact that was created by CloudFormation**

#### Deploying CloudFormation template
  - Manual way:
    - Editing templates in the CloudFormation Designer
    - Using the console to input parameters, etc

  - Automated way:
    - Editing templates in a YAML file
    - Using the AWS CLI (Command Line Interface) to deploy the templates
    - Recommend way when you fully want to automate your flow

#### CloudFormation Building Blocks
  - Template components (one course section for each):
    - 1. Resources: your AWS resources declared in the template **(MANDATORY)**
    - 2. Parameters: the dynamic inputs for your template
    - 3. Mappings: the static variables for your template
    - 4. Outputs: References to what has been created
    - 5. Conditionals: List of conditions to perform resource creation
    - 6. Metadata
  - Template helpers
    - 1. References
    - 2. Functions

### YAML Crash Course
  - Key Value paris
  - Nested Objects
  - Support Arrays
  - Multi line strings
  - Can include comments
  - 
  ```bash
  Parameters:
  KeyName:
    Description: |
                The EC2 Key Pair to allow SSH access 
                to the instance
    Type: 'AWS::EC2::KeyPair::KeyName'
  Resources:
  Ec2Instance:
    Type: 'AWS::EC2::Instance'
    Properties:
      SecurityGroups:
        - !Ref InstanceSecurityGroup
        - MyExistingSecurityGroup
      KeyName: !Ref KeyName
      ImageId: ami-7a11e213
  InstanceSecurityGroup:
    Type: 'AWS::EC2::SecurityGroup'
    Properties:
      GroupDescription: Enable SSH access via port 22
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: '22'
          ToPort: '22'
          CidrIp: 0.0.0.0/0
  ```

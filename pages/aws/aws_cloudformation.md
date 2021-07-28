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
    MyInstance:
      Type: 'AWS::EC2::Instance'
      Properties:
        AvailabilityZone: us-east-1a
        ImageId: ami-ac47edb2
        SecurityGroups:
          - !Ref SSHSecurityGroup
          - !Ref ServerSecurityGroup
    # an elastic IP for our instance
    MyEIP:
      Type: AWS::EC2::MyEIP
      Properties:
        InstanceId: !Ref MyInstance

    # our EC@ security group
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

### CloudFormation Resources
#### What are resources?
  - Resources are the core of your CloudFormation template (MANDATORY)
  - They represent the different AWS Components that will be created and configured
  - Resources are declared and can reference each other
  - AWS figures out creation, updates and deletes of resources for us
  - There are over 224 types of resources
  - Resource types identifiers are of the form:
  - **AWS::aws-product-name::data-type-name**

#### How do I find resource documentation?
  - All the resources can be found here:
    - https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-template-resource-type-ref.html
  - EC2 example here
    - https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-ec2-instance.html

#### FAQ for resources
  - Can I create a dynamic amount of resources?
  - No, you can't. Everything in the CloudFormation template has to be declared. You can't perform code generation there
  - Is every AWS service supported?
  - Almost. Only a select few niches are not there yet
  - You can work around that using AWS Lambda Custom Resources

### CloudFormation Parameters

#### What are parameters?
  - Parameters are a way to provide inputs to your AWS CloudFormation template
  - They're important to know about if:
    - You want to reuse your templates across the company
    - Some inputs can not be determined ahead of time
  - Parameters are extremely powerful, controlled and can prevent errors from happening in your templates thanks to types

#### When should you use a parameter?
  - Ask yourself this:
    - Is this CloudFormation resource configuration likely to change in the future?
    - If so, make it a parameter
  - You won't have to re-upload a template to change its content
    - 
      ```yaml
      Parameters:
        SecurityGroupDescription:
          Description: Security Group Description
          (Simple parameter)
          Type: String
      ```

#### Parameters Settings
  - Parameters can be controlled by all these settings:
  - 
    ```yaml
      - Type:
        - String
        - Number
        - CommaDelimitedList
        - List<Type>
        - AWS Parameter (to help catch invalid values - match against existing values in the AWS Account)
      - Description
      - Constraints
      - ConstraintDescription (String)
      - Min/MaxLength
      - Min/MaxVAlue
      - Defaults
      - AllowedValues (array)
      - AllowedPattern (regexp)
      - NoEcho (Boolean)
    ```

#### How to Reference a Parameter
  - The Fn::Ref function can be leveraged to reference parameters or AWS resources
  - Parameters can be used anywhere in a template
  - The shorthand for this in YAML is !Ref
  - The function can also reference other elements within the template

#### Concept: Pseudo Parameters
  - AWS offers us pseudo parameters in any CloudFormation template
  - These can be used at any time and are enabled by default
  - 
    |Reference Value|Example Return Value|
    | ------ |--- |
    |AWS::AccountId|1234567890|
    |AWS::NotificationARNs|[arn:aws:sns:us-east-1:123456789015:MyTopic]|
    |AWS::NoValue|Does not return a value|
    |AWS::Region|us-east-2|
    |AWS::StackId|arn:aws:cloudformation:us-east-1:12345644789012:stack/MyStack/1c2fa650-54sdf5adfs-s5df44sd|
    |AWS::Region|us-east-2|

### CloudFormation Mappings

#### What are mappings?
  - Mappings are **fixed variables** within your CloudFormation Template
  - They're very handy to differentiate between different environments (dev vs prod), regions (AWS region), AMI types, etc
  - All the values are **hardcoded** within the Template
  - Example: {% include image.html file="mappings.png" %}

#### When would you use mappings vs parameters?
  - Mappings are great when you know in advance all the values that can be taken and that they can be deduced from variables such as
    - Region
    - Availability Zone
    - AWS Account
    - Environment (dev vs prod)
    - Etc...
  - They allow safer control over the template
  - Use parameters when the values are really user specific

#### Fn::FindInMap : Accessing Mapping Values
  - We use Fn:FindInMap to return a named value from a specific key
  - !FindInMap [MapName, TopLevelKey, SecondLevelKey]
  - {% include image.html file="findmap.png" %}
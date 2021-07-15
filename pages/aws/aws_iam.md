---
title: AWS IAM
sidebar: mydoc_sidebar
permalink: aws_iam.html
folder: aws
---

### IAM: Users & Groups

- **Global Service**
- Root account created by default, shouldn't be used or shared
- Users are people within your organization, and can be grouped
- **Groups only contain users, not other groups**
- Users don't have to belong to a group (not best practice), and **user can belong to multiple groups**

### IAM: Permissions

- Users or Groups can be assinged JSON documents called policies.

{% include image.html file="policies.png" %}

- These **policies define the permissions of the Users**
- In AWS you apply the **least privilege principle**: don't give more permissions than a user needs


### IAM: Policies inheritance

- Attach policies to a group that users in the same group can have access to and inherit the policies
- Inline policy : Attach policy to a user directly without using group

{% include image.html file="iam_policy.png" %}

### IAM: Policies Structure

{% include image.html file="policy_structure.png" %}

- Consists of
  - Version: policy language version, always include "2012-10-17"
  - Id: an identifier for the policy (optional)
  - Statement: one or more individual statements (required)

- Statements consists of
  - Sid: identifier for the statement (optional)
  - Effect: wheter the statement allows or denies access (Allow, Deny)
  - Principal: account/user/role to which this policy applied to
  - Action: list of actions this policy allows or denies
  - Resource: list of resources to which the actions applied to
  - Condition: conditions for when this policy is in effect (optional)

### IAM: Password Policy

- Strong passwords = higher security for your account
- In AWS, you can setup a password policy
  - Set a minimum password length
  - Require specific character types:
    - including uppercase letters
    - lowercase letters
    - numbers
    - non-alphanumeric characters
  - Allow all IAM users to change their own passwords
  - Require users to change their password after some time (password expiration)
  - Prevent password re-use

### Multi Factor Authentication - MFA

- Users have access to your account and can possibly change configurations or delete resources in your AWS account
- You want to protect your Root Accounts and IAM users
- MFA = password you know + security device you own
- Main benefit of MFA: If a password is stolen or hacked, the account is not compromised
- Virtual MFA device: Support for multiple tokens on a single device
  - Google Authenticator (phone only)
  - Twillio Authy (multi-device)

### How can users access AWS?

- To access AWS, you have three options:
  - AWS Management Console (protected by password + MFA)
  - AWS Command Line Interface (CLI): protected by access keys
  - AWS Sofware Development Kit (SDK) - for code: protected by access keys
- Access keys are generated through the AWS Console
- Users manage their own access keys
- **Access Keys are secret, just like a password. Don't share them**
- Access Key ID = username
- Secret Access Key = password
- **Do not use root user to create security credentials**

### IAM Roles for Services

- Some AWS service will need to perform actions on your behalf
- To do so, we will assign permissions to AWS services with IAM Roles
- Common roles:
  - EC2 Instance Roles
  - Lambda Function Roles
  - Roles for CloudFormation

{% include image.html file="iam_roles.png" %}

### IAM Security Tools

- IAM Credentials Report(account-level)
  - a report that lists all your account's users and the status of their various credentials

- IAM Access Advisor (user-level)
  - Access advisor shows the service permissions granted to a user and when those services were last accessed
  - You can use this information to revise your policies. Reduce permissions users can get in line with that principle of **least privilies**

### IAM Guidlines & Best Practices

- Don't use the root account except for AWS account setup
- One physical user = One AWS user
- Assign users to groups and assign permissions policies to groups (Or create custom policies and assign policies to them)
- Create a strong password policy
- Use and enforce the use of Multi Factor Authentication (MFA)
- Create use Roles for giving permissions to AWS services
- Use Access Keys for Programmatic Access (CLI/SDK)
- Audit permission of your account with the IAM Credentials Report
- Never share IAM users & Access Keys
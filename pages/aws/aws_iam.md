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
  - Authy (multi-device)
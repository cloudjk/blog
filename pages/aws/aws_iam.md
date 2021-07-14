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


### IAM Policies inheritance

- Attach policies to a group that users in the same group can have access to and inherit the policies
- Inline policy : Attach policy to a user directly without using group

{% include image.html file="iam_policy.png" %}

### IAM Policies Structure

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
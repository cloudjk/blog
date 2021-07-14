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
---
title: AWS CLI
sidebar: mydoc_sidebar
permalink: aws_cognito.html
folder: aws
---

### Cognito Overview

- We want to give our users an identity so that they can interact with our application
- Cognito User Pools:
  - **Sign in functionality for app users**
  - **Integrate with API Gateway & Application Load Balancer**
- Cognito Identity Pools (Federated Identity):
  - **Provide AWS credentials to users to they can access AWS resources directly**
  - Integrate with Cognito User Pools as an identity provider
- Cognito Sync
  - Synchronize data from device to Cognito
  - Is deprecated and replaced by AppSync
- Cognito vs IAM: "hundreds of users", "mobile users", "authenticate with SAML"

### Cognito User Pools (CUP) - User Features

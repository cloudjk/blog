---
title: AWS Cognito
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

### Cognito User Pools (CUP) 
#### User Features
- Create a serverless database of user for your web & mobile apps
- Simple login: Username (or email) / password combination
- Password reset
- Email & Phone Number verification
- Multi-factor authentication (MFA)
- Federated Identities: users from Facebook, Google, SAML...
- Feature: block users if their credentials are compromised elsewhere
- Login sends back a JSON Web Token (JWT)

#### Diagram
- {% include image.html file="cup_diagram.png" %}

#### Integrations
- CUP integrates with API Gateway and Application Load Balancer
- {% include image.html file="cup_integrations.png" %}

#### Lambda Triggers
- CUP can invoke a Lambda function synchronously on these triggers
- {% include image.html file="cup_lambdatriggers.png" %}

#### Hosted Authentication UI
- Cognito has a hosted authentication UI that you can add to your app to handle sign-up and sign-in workflows
- Using the hosted UI, you have a foundation for integration with social logins, OIDC and SAML
- Can customize with a custom logo and custom CSS

### Cognito Identity Pools (Federated Identities)
#### Overview
- Get identities for users so they obtain temporary AWS credentials
- Your identity pool (e.g identity source) can include:
  - Public Providers (Login with Amazon, Facebook, Google, Apple ...)
  - Users is an Amazon Cognito suer pool
  - OpenId Connect Providers & SAM Identity Providers
  - Developer Authenticated Identities (custom login server)
  - Cognito Identity Pools allow for **unauthenticated (guest) access**
- Users can then access AWS services directly or through API Gateway
  - The IAM policies applied to the credentials are defined in Cognito
  - They can be customized based on the user_id for fine grained control

#### Cognito Identity Pools - Diagram
- {% include image.html file="cognito_identity_pools_diagram.png" %}

#### Cognito Identity Pools - Diagram with CUP
- {% include image.html file="cognito_identity_pools_diagram_w_cup.png" %}

#### Cognito Identity Pools - IAM Roles
- Default IAM roles for authenticated and guest users
- Define rules to choose the role for each user based on the User's ID
- You can partition your users' access using policy variables
- IAM credentials are obtained by Cognito Identity Pools through STS
- The roles must have a "trust" policy of Cognito Identity Pools

#### Cognito Identity Pools - Guest User example
- {% include image.html file="cip_guest.png" %}

#### Cognito Identity Pools - Policy variable on S3
- {% include image.html file="cid_policy.png" %}

#### Cognito Identity Pools - DynamoDB
- {% include image.html file="cip_dynamo_db.png" %}

### Cognito User Pools vs Identity Pools
#### Cognito User Pools:
- Database of users for your web and mobile application
- Allows to federate logins through Public Social, OIDC, SAML ...
- Can customize the hosted UI for authentication (including the log)
- Has triggers with AWS Lambda during the authentication flow
#### Cognito Identity Pools:
- Obtain AWS credentials for your users
- Users can login through Public Social, OIDC, SAML & Cognito User Pools
- Users can be unauthenticated(guests)
- Users are mapped to IAM roles & policies, can leverage policy variables
#### CUP + CIP = manage user/password + access AWS services

#### Cognito Identity Pools - Diagram with CUP
- {% include image.html file="cip_diagram_w_cup.png" %}

### Cognito Sync
- Deprecated - user AWS AppSync now
- Store preferences, configuration, state of app
- Corss device synchronization (any platform - iOS, Android, etc...)
- Offline capability (synchronization when back online)
- Store data in datasets (up to 1MB), up to 20 datasets to synchronize
- Push Sync: silently notify across all devices when identity data changes
- Cognito Stream: stream data from Cognito into Kinesis
- Cognito Events: execute Lambda functions in response to events

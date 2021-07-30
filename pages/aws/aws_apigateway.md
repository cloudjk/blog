---
title: AWS API Gateway
sidebar: mydoc_sidebar
permalink: aws_apigateway.html
folder: aws
---


### API Gateway Overview

#### Building a Serverless API
  - {% include image.html file="serverless_api.png" %}

#### API Gateway
  - AWS Lambda + API Gateway: **No infrastructure to manage**
  - Support for the WebSocket Protocol
  - Handle API version (v1, v2...)
  - Handle different environments (dev, test, prod...)
  - Handle security (Authentication and Authorization)
  - Create API keys, handle request throttling
  - Swagger / Open API import to quickly define APIs
  - Transform and validate requests and responses
  - Generate SDK and API specifications
  - Cache API responses

#### Integrations High Level
  - Lambda Function
    - Invoke Lambda function
    - Easy way to expose REST API backed by AWS Lambda
  - HTTP
    - Expose HTTP endpoints in the backend
    - Example: internal HTTP API on premise, Application Load Balancer...
    - Why? Add rate limiting, caching, user authentications, API keys, etc...
  - AWS Service
    - Expose any AWS API through the API Gateway?
    - Example: start an AWS Step Function workflow, post a message to SQS
    - Why? Add authentication, deploy publicly, rate control...

#### Endpoint Types
  - Edge-Optimized (default): For global clients
    - Requests are routed through the CloudFront Edge locations (improves latency)
    - The API Gateway still lives in only one region
  - Regional:
    - For clients within the same region
    - Could manually combine with CloudFront (more control over the caching strategies and the distribution)
  - Private:
    - Can only be accessed from you VPC using an interface VPC endpoint (ENI)
    - Use a resource policy to define access

### API Gateway - Stages and Deployment
  
#### Deployment Stages
  - Making changes in the API Gateway does not mean they're effective
  - You need to make a "deployment" for them to be in effect
  - It's a common source of confusion
  - Changes are deployed to "Stages" (as many as you want)
  - Use the naming you like for stages (dev, staging, prod)
  - Each stage has its own configuration parameters
  - Stages can be rolled back as a history of deployments is kept

#### Stages v1 and v2
  - {% include image.html file="api_v1_v2.png" %}

#### Stage Variables
  - Stage variables are like **environment variables for API Gateway**
  - Use them to change often changing configuration values
  - They can be used in:
    - Lambda function ARN
    - HTTP Endpoint
    - Parameter mapping templates
  - Use cases:
    - Configure HTTP endpoints your stages talk to (dev, staging, prod ...)
    - Pass configuration parameters to AWS Lambda through mapping templates
  - Stage variables are passed to the "context" object in AWS Lambda

#### Canary Deployment
  - Possibility to enable canary deployments for any stage (usually prod)
  - Choose the % of traffic the canary channel receives
  - Metrics & Logs are separate (for better monitoring)
  - Possibility to override stage variables for canary
  - This is blue/green deployment with AWS Lambda & API Gateway


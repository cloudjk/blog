---
title: AWS SQS & SNS
sidebar: mydoc_sidebar
permalink: aws_sqs_sns.html
folder: aws
---

### Introduction to Messaging

#### Section Introduction
- When we start deploying multiple applications, they will inevitably need to communicate with one another
- There are two patterns of application communication
- {% include image.html file="messaging.png" %}
- **Synchronous between applications can be problematic if there are sudden spikes of traffic**
- What if you need to suddenly encode 1000 videos but usually it's 10?
- In that case, it's better to **decouple** your applications.
  - using SQS: queue model
  - using SNS: pub/sub model
  - using Kinesis: real-time streaming model
- These services can scale independently from our application!

### Standard Queue Overview

#### What is a queue?
- {% include image.html file="what_is_queue.png" %}

#### Standard Queue
- Oldest offering (over 10 years old)
- Fully managed service, used to decouple applications
- Attributes
  - **Unlimited throughput**, unlimited number of messages in queue
  - Default retention of messages: 4 days, maximum of 14 days
  - Low latency (<10 ms on publish and receive)
  - Limitation of 256KB per message sent
- Can have duplicate messages (at least once delivery, occasionally)
- Can have out of order messages (best effort ordering)

#### Producing Messages
- Produced to SQS using the SDK (SendMessage API)
- The message is persisted in SQS until a customer deletes it
- Message retention: default 4 days, up to 14 days
- Example: send an order to be processed
  - Order id
  - Customer id
  - Any attributes you want
  - {% include image.html file="producing_message.png" %}
- SQS Standard: unlimited throughput

#### Consuming Messages
- Consumers (running on EC2 instances, servers or AWS Lambda)...
- Poll SQS for messages (receive up to 10 messages at a time)
- Process the messages (example: insert the message into a RDS database)
- Delete the messages using the DeleteMessage API
- {% include image.html file="consuming_message.png" %}

#### Multiple EC@ Instances Consumers
- {% include image.html file="ec2_consumers.png" %}
- Consumers receive and process messages in parallel
- At least once delivery
- Best-effort message ordering
- Consumers delete messages after processing themes
- We can scale consumers horizontally to improve throughput of processing the

#### SQS with Auto Scaling Group(ASG)
- {% include image.html file="sqs_asg.png" %}

#### SQS to decouple between application tiers
- {% include image.html file="decouple.png" %}

#### Security
- Encryption:
  - In-flight encryption using HTTPS API
  - At-rest encryption using KMS keys
  - Client-side encryption if the client wants to perform encryption/decryption itself
  - Access Controls: IAM policies to regulate access to the SQS API
  - SQS Access Policies (similar to S# bucket policies)
  - Useful for allowing other services (SNS, S3...) to write to an SQS queue

### SQS Queue Access Policy
- {% include image.html file="access_policy.png" %}
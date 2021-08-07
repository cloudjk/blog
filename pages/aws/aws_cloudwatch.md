---
title: AWS CloudWatch
sidebar: mydoc_sidebar
permalink: aws_cloudwatch.html
folder: aws
---

### Monitoring Overview

#### Why Monitoring is important
- We know how to deploy applications
  - Safely
  - Automatically
  - Using Infrastructure as Code
  - Leveraging the best AWS components
- Our applications are deployed and our users don't care how we did it...
- Our users only care that the application is working
  - Application latency: will it increase over time?
  - Application outages: customer experience should not be degraded
  - Users contacting the IT department or complaining is not a good outcome
  - Troubleshooting and remediation
- Internal Monitoring
  - Can we prevent issues before they happen?
  - Performance and Cost
  - Trends (scaling patterns)
  - Learning and Improvement

#### Monitoring in AWS
- AWS CloudWatch:
  - Metrics: Collect and track key metrics
  - Logs: Collect, monitor, analyze and store log files
  - Events: Send notifications when certain events happen in your AWS
  - Alarms: React in real-time to metrics/events
- AWS X-Ray:
  - Troubleshooting application performance and errors
  - Distributed tracing of microservices
- AWS CloudTrail:
  - Internal monitoring of API calls being made
  - Audit changes to AWS Resources by your users

### AWS CloudWatch Metrics
#### Overview
- CloudWatch provides metrics for every services in AWS
- **Metric is a variable to monitor** (CPUUtilization, NetworkIn...)
- Metrics belong to namespaces
- Dimension is an attribute of a metric (instance id, environment, etc...)
- Up to 10 dimensions per metric
- **Metrics have timestamps**

#### EC2 Detailed monitoring
- EC2 instance metrics have metrics "every 5 minutes"
- With detailed monitoring (for a cost), you get data "every 1 minute"
- Use detailed monitoring if you want to scale faster for your ASG
- The AWS Free Tier allows us to have 10 detailed monitoring metrics
- Note: EC2 memory usage is by default not pushed (must be pushed from inside the instance as a custom metric)
- 

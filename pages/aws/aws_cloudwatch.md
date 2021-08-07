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

### AWS CloudWatch Custom Metrics
- Possibility to define and send your own custom metrics to CloudWatch
- Example: memory(RAM) usage, disk space, number of logged in users ...
- **Use API call PutMetricData**
- Ability to use dimensions (attributes) to segment metrics
  - Instance.id
  - Environment.name
- Metric resolution (StorageResolution API parameter - two possible value):
  - Standard: 1 minute (60 seconds)
  - High Resolution: 1/5/10/30 second(s) - Higher cost
- Important: Accepts metric data points two weeks in the past and two hours in the future (make sure to configure your EC2 instance time correctly)
- [winston](https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_PutMetricData.html)

### AWS CloudWatch Logs
- **Applications can send logs to CloudWatch using the SDK**
- **CloudWatch can collect log from:**
  - Elastic Beanstalk: collection of logs from application
  - ECS: collection from containers
  - AWS Lambda: collection from function logs
  - VPC Flow Logs: VPC specific logs
  - API Gateway
  - CloudTrail based on filter
  - CloudWatch log agents: for example on EC2 machines
  - Route53: Log DNS queries
- CloudWatch Logs can go to:
  - Batch exporter to S3 for archival
  - Stream to ElasticSearch cluster for further analytics
- CloudWatch Logs can user filter expressions
- Logs storage architecture:
  - Log groups: arbitrary name, usually representing an application
  - Log stream: instances within application / log files / containers
- Can define log expiration policies (never expire, 30 days, etc...)
- Using the AWS CLI we can tail CloudWatch logs
- To send logs to CloudWatch, make sure IAM permissions are correct
- Security: encryption of logs using KMS at the Group Level
  
### CloudWatch Log Agent & CloudWatch Unified Agent

#### CloudWatch Logs for EC2
- By default, no logs from your EC2 machine will go to CloudWatch
- You need to run a CloudWatch agent on EC2 to push the log files you want
- Make sure IAM permission are correct
- The CloudWatch log agent can be setup on on-premises too
- {% include image.html file="cw_logs.png" %}

#### CloudWatch Logs Agent & CloudWatch Unified Agent
- For virtual servers (EC2 instances, on-premise servers...)
- CloudWatch Logs Agent
  - Old version of the agent
  - Can only send to CloudWatch Logs
- CloudWatch Unified Agent
  - Collect additional system-level metrics such as RAM, process, etc...
  - Collect logs to send to CloudWatch Logs
  - Centralized configuration using SSM Parameter Store

#### CloudWatch Unified Agent - Metrics
- Collected directly on your Linux server/EC2 instance
- CPU (active, guest, idle, system, user, steal)
- Disk metrics (free, used, total), Disk IO(writes, reads, bytes, iops)
- RAM (free, inactive, used, total, cached)
- Netstat (number of TCP and UDP connections, net packets, bytes)
- Processes (total, dead, bloqued, idle, running, sleep)
- Swap Space (free, used, used %)
- Reminder: out-of-the-box metrics for EC2- disk, CPU, network (high level)

### CloudWatch Alarms
#### Overview
- Alarms are used to trigger notifications for any metric
- Various options (sampling, %, max, min, etc...)
- Alarm States:
  - OK
  - INSUFFICIENT_DATA
  - ALARM
- Period:
  - Length of time in seconds to evaluate the metric
  - High resolution custom metrics: 10 sec, 30 sec or multiples of 60 sec
#### CloudWatch Alarm Targets
- Stop, Terminate, Reboot or Recover an EC2 Instance
- Trigger Auto Scaling Action
- Send notification to SNS (from which you can do pretty much anything)
- {% include image.html file="cw_alarm_targets.png" %}

#### EC2 Instance Recovery
- Status Check:
  - Instance status = check the EC2 VM
  - System status = check the underlying hardware
  - {% include image.html file="cw_ec2_recovery.png" %}
- Recovery: Same Private, Public, Elastic IP, metadata, placement group

#### CloudWatch Alarm: good to know
- Alarms can be created based on CloudWatch Logs Metrics Filters
- {% include image.html file="cw_goodtoknow.png" %}
- To test alarms and notifications, set the alarm state to Alarm using CLI
- 
    ```bash
    aws cloudwatch set-alarm-state --alarm-name "myalarm" --state-value ALARM --state-reason "testing purposes"
    ```

### CloudWatch Events
- Event Pattern: **Intercept events from AWS services** (Sources)
  - Example sources: EC2 Instance Start, CodeBuild Failure, S#, Trusted Advisor
  - Can intercept any API call with CloudTrail integration
- Schedule or Cron (example: create an event every 4 hours)
- **A JSON payload is created from the event and passed to a target...**
  - Compute: Lambda, Batch, ECS task
  - Integration: SQS, SNS, Kinesis, Data Streams, Kinesis Data Firehose
  - Orchestration: Step Functions, CodePipeline, CodeBuild
  - Maintenance: SSM, EC2 Actions
  - 
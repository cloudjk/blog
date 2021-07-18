---
title: AWS Route53
sidebar: mydoc_sidebar
permalink: aws_route53.html
folder: aws
---

### Route53 Overview

- Route53 is a Managed DNS (Domain Name System)
- DNS is a collection of rules and records which helps clients understand how to reach a server through its domain name
- In AWS, the most common records are:
  - A: hostname to IPv4
  - AAAA: hostname to IPv6
  - CNAME: hostname to hostname
  - Alias: hostname to AWS resource

- Diagram for A Record
  - {% include image.html file="diagram_a_record.png" %}

- Route53 can use:
  - public domain names you own (or buy)
    - (e.g.) applicationI.mypublicdomain.com
  - private domain names that can be resolved by your instances in your VPCs
    - (e.g.) applicationI.company.internal

- Route53 has advanced features such as:
  - Load balancing (through DNS - also called client load balancing)
  - Health Check (although limited...)
  - Routing policy: simple, failover, geolocation, latency, weighted, multi value

- You pay $0.50 per month per host zone

- To find the IPv4 info use **dig** or *nslookup* in mac (no http://!!)

  ```bash
  # show detailed info (including TTL)
  dig www.google.com
  # show just ip
  nslookup www.google.com
  ```

### DNS Records TTL (Time To Live)

- TTL is basically a way for web browsers and client to cache the response of a DNS query not to overload DNS
- {% include image.html file="ttl.png" %}

### CNAME vs Alias

- AWS Resources (Load Balancers, CloudFront...) expose an AWS hostname: **lbl-1234.us-east-2.elb.amazonaws.com** and you want **myapp.mydomain.com**
- CNAME:
  - Points a hostname to any other hostname (app.mydomain.com => blabla.anything.com)
  - **Only for Non Root Domain (e.g.) something.mydomain.com**
- Alias:
  - Points a hostname to an AWS Resource (app.mydomain.com => blabla.amazonaws.com)
  - **Works for Root Domain and Non Root Domain (e.g.) mydomain.com * something.mydomain.com**
  - Free of charge
  - Native health check

### Routing Policy
#### Simple Routing Policy
  - Use when you need to redirect to a single resource
  - You can't attach health checks to a simple routing policy
  - **If multiple values are returned, a random one is chosen by the client**
  - {% include image.html file="simple_routing.png" %}

#### Weighted Routing Policy
  - Control the % of the requests that go to specific endpoint
  - Helpful to test 1 % of traffic on new app version for example
  - Helpful to split traffic between two regions
  - Can be associated with Health Checks
  - {% include image.html file="weighted_routing.png" %}

#### Latency Routing Policy
  - Redirect to the server that has the least latency close to us
  - Super helpful when latency of users is a priority
  - Latency is evaluated in terms of user to designated AWS Region
  - Germany may be directed to the US (if that's the lowest latency)
  - {% include image.html file="latency_routing.png" %}

#### Failover Routing Policy
  - {% include image.html file="failover_policy.png" %}

#### Geo Location Routing Policy
  - Different from Latency based!
  - This is routing based on user location
  - Here we specify: traffic from the UK should go to this specific IP
  - Should create a **default policy** (in case there's n omatch on location)
  - {% include image.html file="geo_routing.png" %}

#### Geoproximity Routing Policy

  - Route traffic to your resources based on the geographic location of users and resources
  - Ability to shift more traffic to resources based on the defined bias
  - To change the size of the geographic region, specify bias values:
    - To expand (1 to 99) : more traffic to the resource
    - To shrink (-1 to -99) : less traffic to the resource
  - Resources can be:
    - AWS resources (specify AWS region)
    - Non-AWS resources (specify Latitude and Longitude)
  - You must use Route53 Traffic Flow (advanced) to use this feature

### Health Checks

-  Have X health checks failed => unhealthy (default 3)
-  After X health checks passed => healthy (default 3)
-  Default Health Check Interval: 30s (can set to 10s - higher cost)
-  **About 15 health checkers will check the endpoint health** (i.e.) one request every 2 seconds on average
-  Can have HTTP, TPC and HTTPS health checks (no SSL verification)
-  Possibility of integrating the health check with CloudWatch
-  **Health checks can be linked to Route53 DNS queries!**
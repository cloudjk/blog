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


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

#### Diagram for A Record
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
dig www.google.com
# or
nslookup www.google.com
```


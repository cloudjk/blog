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

#### Multi Value Routing Policy

  - Use when routing traffic to multiple resources
  - Want to associate a Route 53 health checks with records
  - Up to 8 healthy records are returned for each Multi Value query
  - Multi Value is not a substitue for having an ELB (ELB is for same region, multi value is for different region)
  - 
  | Name             | Type     | Value        | TTL | Set ID | Health Check |
  | ---------------  | -------- | ------------ | --- | ------ | ------------ |
  | www.example.com  | A Record | 192.0.2.2    | 60  | Web1   | A            |  
  | www.example.com  | A Record | 198.51.100.2 | 60  | Web2   | B            |
  | www.example.com  | A Record | 203.0.113.2  | 60  | Web3   | C            |

### Health Checks

-  Have X health checks failed => unhealthy (default 3)
-  After X health checks passed => healthy (default 3)
-  Default Health Check Interval: 30s (can set to 10s - higher cost)
-  **About 15 health checkers will check the endpoint health** (i.e.) one request every 2 seconds on average
-  Can have HTTP, TPC and HTTPS health checks (no SSL verification)
-  Possibility of integrating the health check with CloudWatch
-  **Health checks can be linked to Route53 DNS queries!**

### 3rd Party Domains and Route53
#### Route53 as a Registrar
- A domain name registrar is an organization that manages the reservation of Internet domain names
- Famous names:
  - GoDaddy
  - Google Domains
  - Etc...
- And also... Route53 (e.g.AWS)!
- Domain Registrar !== DNS

#### 3rd Party Registrar with AWS Route53
  - If you buy your domain on 3rd party website, you can still use Route53
    - 1) Create a Hosted Zone using 3rd party domain in Route53
    - 2) Update NS Records on 3rd party website to use Route53 name servers
  - Domain Registrar !== DNS
  - But each domain registrar usually comes with some DNS features
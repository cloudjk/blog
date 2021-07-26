---
title: AWS CloudFront
sidebar: mydoc_sidebar
permalink: aws_cloudfront.html
folder: aws
---

### CloudFront Overview
- Content Delivery Network (CDN)
- Improves read performance, content is cached at the edge
- 216 Point of Presence globally (edge locations)
- DDos protection, integration with Shield, AWS Web Application Firewall
- Can expose external HTTPS and can talk to internal HTTPS backends
- {% include image.html file="cloudfront.png" %}

#### CloudFront - Origins
- S3 bucket
  - For distributing files and caching them at the edge
  - Enhanced security with CloudFront Origin Access Identity (OAI)
  - CloudFront can be used as an ingress (to upload files to S3)

#### Custom Origin (HTTP)
  - Application Load Balancer
  - EC2 instance
  - S3 website (must first enable the bucket as a static s3 website)
  - Any HTTP backend you want

#### CloudFront at a high level
  - {% include image.html file="cloudfront_highlevel.png" %}

#### CloudFront - S3 as an Origin
  - {% include image.html file="cloudfront_s3_origin.png" %}

#### CloudFront - ALB OR EC2 as an origin
  - {% include image.html file="cloudfront_alb_ec2.png" %}

#### CloudFront Geo Restriction
  - You can restrict who can access your distribution
    - Whitelist: Allow your users to access your content only if they're in one of the countries on a list of approved countries
    - Blacklist: Prevent your users from accessing your content if they're in one of the countries on a blacklist of banned countries
  - The country is determined using a 3rd party Geo-IP database
  - Use case: Copyright Laws to control access to content

#### CloudFront and HTTPS
  - Viewer Protocol Policy:
    - Redirect HTTP to HTTPS
    - Or use HTTPS only
  - Origin Protocol Policy (HTTP or S3)
    - HTTPS only
    - Or **Match Viewer**
      (HTTP => HTTP & HTTPS => HTTPS)
  - Note : S3 bucket "websites" don't support HTTPS
  - {% include image.html file="protocol_policy.png" %}

#### CloudFront vs S3 Cross Region Replication
  - CloudFront:
    - Global Edge network
    - Files are cached for a TTL
    - Great for static content that must be available everywhere

  - S3 Cross Region Replication
    - Must be setup for each region you want replication to happen
    - Files are updated in near real-time
    - Read only
    - Great for dynamic content that needs to be available at low-latency in few regions

### CloudFront Caching & Caching Invalidations
  - Cache based on
    - Headers
    - Session Cookies
    - Query String Parameters
  - The cache lives at each CloudFront Edge Location
  - You want to maximize the cache hit rate to minimize requests on the origin
  - Control the TTL (0 seconds to 1 year), can be set by the origin using the Cache-Control header, Expires header...
  - You can invalidate part of the cache using the CreateInvalidation API
  - {% include image.html file="caching.png" %}

### CloudFront - Maximize cache hits by separating static and dynamic distributions
  - {% include image.html file="maximize_cache.png" %}
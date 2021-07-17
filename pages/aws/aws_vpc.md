---
title: AWS VPC, Subnet, IGW, RouteTable, etc
sidebar: mydoc_sidebar
permalink: aws_vpc.html
folder: aws
---

### CIDR
#### Understanding CIDR - IPv4

- Classless Inter-Domain Routing
- CIDR are used for Security Groups rules, or AWS networking in general
- They help to define IP address range
  - WW.XX.YY.ZZ/32 == one IP
  - 0.0.0.0/0 == all IP
  - 192.168.0.0/26 : 192.168.0.0 - 192.168.0.63 (64 IP)

#### Understanding CIDR

- A CIDR has two components:
  - The base IP (XX.XX.XX.XX)
  - The Subnet Mask (/26)
- The base IP represents an IP contained in the range
- The subnet masks define how many bits can change in the IP
- The subnet mask can take two form. Examples:
  - 255.255.255.0 <- less common
  - /24           <- more common

#### Understanding CIDR Subnet Masks

- The subnet masks basically allows part of the underlying IP to get additional next values from the base IP
- IPv4 is composed of 4 8bit binary(octet) 
```bash
/32 - no IP number can change
/24 - last IP number can change (2^8)
/16 - last IP two numbers can change (2^16)
/8 - last IP three numbers can change (2^24)
/0 - all IP numbers can change (2^32)
```
- 192.168.0.0/24 = 2^8 = 256
  - 192.168.0.0 - 192.168.0.255 (256 IP)
- 192.168.0.0/16 = 2^16 = 65536
  - 192.168.0.0 - 192.168.255.255
- 134.56.78.123/32 = 2^0 = 1
  - 134.56.78.123
- 0.0.0.0/0 = all IP!
- When in doubt, use this website : https://www.ipaddressguide.com/cidr

#### Private vs Public IP (IPv4) Allowed ranges

- The Internet Assinged Numbers Authority(IANA) established certain blocks of IPv4 addresses for the use of private(LAN) and public(Internet) addresses.
- Private IP can only allow certain values
  - 10.0.0.0 - 10.255.255.255 (10.0.0.0/8) <= in big networks
  - 172.16.0.0 - 172.31.255.255 (172.16.0.0/12) <= default AWS one
  - 192.168.0.0 - 192.168.255.255 (192.168.0.0/16) <= example: home networks
- All the rest of the IP on the internet are public IP

### Default VPC Walk-through

- All new accounts have a default VPC
- New instances are launched into default VPC if no subnet is specified
- Default VPC have internet connectivity and all instances have public IP

### VPC in AWS - IPv4

- VPC = Virtual Private Cloud
- You can have multiple VPCs in a region (max 5 per region - soft limit)
- Max CIDR per VPC is 5. For each CIDR:
  - Min size is /28 = 16 IP Addresses
  - Max size is /16 = 65536 IP Addresses
- Because VPC is private, only the Private IP ranges are allowed:
  - 10.0.0.0 - 10.255.255.255 (10.0.0.0/8)
  - 172.16.0.0 - 172.31.255.255 (172.16.0.0/12)
  - 192.168.0.0 - 192.168.255.255 (192.168.0.0/16)
- **Your VPC CIDR should not overlap with your other networks**

### Subnet

- Subnet is a logical subdivision of an IP network
- Usually a public subnet is much smaller than a private subnet because in a public subnet you would put your load balancers only, where as in the private subnet you would put all your applications et cetera.
- AWS reserves 5 IPs address (first 4 and last 1 IP address) in each Subnet
- These 5 IPs are not available for use and cannot be assigned to an instance
- Ex, if CIDR block 10.0.0.0/24, reserved IP are:
  - 10.0.0.0: Network address
  - 10.0.0.1: Reserved by AWS for the VPC router
  - 10.0.0.2: Reserved by AWS for mapping to Amazon-provided DNS
  - 10.0.0.3: Reserved by AWS for future use
  - 10.0.0.255: Network broadcast address. AWS does not support broadcast in a VPC, therefore the address is reserved

### Internet Gateways

- Internet gateways help our VPC instances connect with the internet
- It scales horizontally and is HA and redundant
- Must be created separately from VPC
- One VPC can only be attached to one IGW and vice versa
- Internet Gateway is also a NAT for the instances that have a public IPv4
- Internet Gateways on their own do not allow internet access
- Route tables must also be edited

{% include image.html file="aws_vpc.png" %}
{% include image.html file="public_rt.png" %}
{% include image.html file="private_rt.png" %}

### NAT Instances - Network Address Translation (Outdated but still at the exam)

- Allow instances in the private subnets to connect to the internet
- Must be launched in a public subnet
- Must disable EC2 flag: Source/Destination Check
- Must have Elastic IP attached to it
- Route table must be configured to route traffic from private subnets to NAT instance

{% include image.html file="nat_instance.png" %}

### NAT Instances - Comments

- Amazon Linux AMI pre-configured are available
- Not highly available / resilient setup out of the box
- Would need to create ASG in multi AZ + resilient user-data script
- Internet traffic bandwidth depends on EC2 instance Performance
- Must manage security groups & rules
  - Inbound:
    - Allow HTTP / HTTPS traffic coming from private subnets
    - Allow SSH from your home network (access is provided through Internet Gateway)
  - OUtbound:
    - Allow HTTP/HTTPS traffic to the internet

### NAT Gateway

- AWS managed NAT, higher bandwidth, better availability, no admin
- Pay by the hour for usage and bandwidth
- NAT is created in specific AZ, uses an EIP
- Cannot be used by an instance in that subnet (only from other subnets)
- Requires an IGW (Private Subnet => NAT GW => IGW)
- 5 Gbps bandwidth with automatic scaling up to 45 Gbps
- No security group to manage / required

{% include image.html file="nat_gw.png" %}

### NAT Gateway with High Availability

- NAT Gateway is resilient within a single-AZ
- Must create multiple NAT Gateway in multiple AZ for fault-tolerance
- There is no cross AZ failover needed because if an AZ goes down it doesn't need NAT

{% include image.html file="nat_gw_failover.png" %}

### Compare NAT gateways and NAT instances

https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-comparison.html
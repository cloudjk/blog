---
title: Connecting to AWS EC2 using Pem key via .ssh/config
sidebar: mydoc_sidebar
permalink: aws_ssh_connect_ec2.html
folder: aws
---
# Connecting to AWS EC2 using Pem key via .ssh/config

```bash
Host <an easy to remember name for the server>
HostName <IP address of the server>
IdentityFile <full path of the private Key file>
User <username>

# example
Host personal-aws
HostName 13.211.120.243
User ec2-user
IdentityFile ~/.ssh/personal-ryan.pem

# How to connect
ssh personal-aws
```


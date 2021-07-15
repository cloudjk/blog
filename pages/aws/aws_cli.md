---
title: AWS CLI
sidebar: mydoc_sidebar
permalink: aws_cli.html
folder: aws
---

### What's the AWS CLI?

- A tool that enables you to interact with AWS services using commands in your command-line shell
- Direct Access to the public APIs of AWS services
- You can develop scripts to manage your resources
- It's open source https://github.com/aws/aws-cli
- Alternative to using AWS Management Console

{% include image.html file="aws-cli.png" %}

### AWS CLI Configuration

- Download and install AWS CLI latest stable version
- Configure AWS CLI
- Check whether AWS CLI is installed
```bash
aws --version
```

- To configure add AWS Access Key Id and Secret Access Key
```bash
aws configure
```

- To check aws configuration, go to credentials file path
```bash
vim ~/.aws/credentials
```

- To handle multiple accounts, use --profile option. But default account does not need it.
```bash
aws configure --profile account1
```

### AWS CLI Cheatsheet
- run command you want to check
```bash
aws iam list-users
```
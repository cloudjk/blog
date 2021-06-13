---
layout: post
title: Connecting AWS EC2 using just SSH Key
subtitle: AWS Connecting EC2 using just SSH Key
author: cloudjk
tags: [aws, connect, ec2, ssh, without, pem]
---

# Create SSH Key

## 1. What is SSH Key?

When connecting to server, use secure shell key instead of password.

## 2. When is it used ?

-   when we need higher level of security for server connection instead of using password
-   when we connect to server without log in process.

## 3. How SSH Key works

-   SSH Key is composed of public key and private key. Private key is located in the local machine(SSH Client) and public key is located in remote machine(SSH Server).
-   When we try to connect to server using SSH Key, SSH client verifies whether private key in local machine corresponds to public key in remote machine.

## 4. How to make SSH Key

-   When we connect to server using SSH Key in Unix(Linux, Mac), we use ssh-keygen program.

## 5. How to use SSH Keygen

```bash
$ ssh-keygen
```

-   Once pressing enter, ssh key is created in the default home path($Home/.ssh). SSH Client basically tries to verify using key in this directory.
-   Passphrase is kind of password and it encrypts private key using input value. The recommended value is 10 ~ 30 characters and it is optional. **If you want auto connection, it should be skipped**.
-   verify key

```bash
$ ls-al ~/.ssh/
```

-   id_rsa : private key, never expose it to others.
-   id_rsa.pub : public key, put in the authorized_keys in remote machine.
-   authroized_keys : located in .ssh directory in remote machine and saves id_rsa.pub key value.
-   Now we should add id_rsa.pub to $HOME/.ssh/authrozied_keys in remote server

![id-rsa](/assets/img/posts/id-rsa.png)

-   contents in authroized_keys should correspond to id_rsa.pub in SSH Client.

```bash
# 1. Using SCP(Secure copy command), copy id_rsa.pub file in SSH Client to SSH Server.
$ scp -i Documents/AWS/pem/keyformyfirstec2.pem ~/.ssh/id_rsa.pub ec2-user@3.26.25.236:.ssh

# 2. After copying file using above command, add authorized_keys file using below command in remote server
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys

# 3. Delete id_rsa.pub
$ rm ~/.ssh/id_rsa.pub

# 4. permission for authorized_keys should be 600
$ sudo chmod 600 ~/.ssh/authorized_keys
```

## 6. Connect using SSH

-   It is possible to connect without password like below

```bash
$ ssh id_of_remote@host_address_of_remote
```

-   If id_rsa file is created not in default directory ($HOME/.ssh/id_rsa) use i option. In case of conenction error, use -v option to track down the cause of error

```bash
$ ssh -i $HOME/auth id_of_remote@host_address_of_remote
```

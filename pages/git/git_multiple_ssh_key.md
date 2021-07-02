---
title: SSH Key setting for multiple github accounts
sidebar: mydoc_sidebar
permalink: git_multiple_ssh_key.html
folder: git
---
## 1. Create multiple host in ~/.ssh/config
```bash
# Default Github
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

Host probaka-github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/probaka76
```

## 2. Must change git clone address like below to use non-default github ssh host
```bash
# git: use git as a user always
# probaka-github.com: name of the host set in config. for default github host, just use github@com
# probaka76: github account
# test.git : name of the repository
git@probaka-github.com:probaka76/test.git
```

## 3. Do not use ssh-add! This only allows to interact with github until session expires.
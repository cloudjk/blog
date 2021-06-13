---
title: Multiple SSH Keys settings for different github account
sidebar: mydoc_sidebar
permalink: git_multiple_ssh_key.html
folder: git
---
## Create different ssh keys
```bash
ssh-keygen -t rsa -C "your_email@youremail.com"
```

## Add to ssh key agents
```bash
ssh-add ~/.ssh/id_rsa_activehacker
ssh-add ~/.ssh/id_rsa_jexchan
```

## Delete all cached keys
```bash
ssh-add -D
```

## Check saved keys
```bash
ssh-add -l
```

## add to ssh config 
```bash
#activehacker account
Host github.com.activehacker
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa_activehacker

#jexchan account
Host github.com.jexchan
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_rsa_jexchan
```

## Important!!! change git clone address using config Host
```bash
git clone git@github.com.activehacker:activehacker/gfs.git gfs_jexchan
as oppose to
git clone git@github.com:activehacker/gfs.git gfs_jexchan
```
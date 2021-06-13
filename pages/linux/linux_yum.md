---
layout: post
title: How To List all repository packages with Yum Command
author: cloudjk
tags: [linux, yum]
---

# How to List all repository packages with Yum Command

I have added a new repository into my repositories and I want to list all packages. Find the total count of packages and filter some of the packages I am interested in. And now we can start the process.

1.List All Repository Packages
yum command have list option which will list all packages from currently available repositories. This will check all currently enabled repositories.

```bash
$ yum list
```

2.Filter Listed Packages
While listing packages we may need to specific packages. We will get the help of grep command while using yum list . We will grep packages which name have stack .

```bash
$ yum list | grep stack
```

3.List Installed Packages
If we need only installed packages to list we need to provide the installed at the end of the yum list command like below.

```bash
$ yum list installed
```

4.list packages which names contains user .

```bash
$ yum list installed | grep "user"
```

List Package History

```bash
$ sudo yum history list
```

5.List Group Packages
Distributions like CentOS, Fedora, RedHat provides group packages which contains multiple package to setup different environments. These environments can be development, XFCE etc. We can use grouplist in order to list this group packages.

```bash
$ yum grouplist
```

Filter Group Packages
In some cases we may need to filter listed group packages. We will again use grep command in order to filter listed group packages. In this example we will filter groups packages which name contains Desktop in order to list desktop group packages.

```bash
$ yum grouplist | grep Desktop
```

Count Packages
We can count packages too. We can count total packages those starts with a like below. We will use wc command with the -l option.

```bash
$ yum list | grep -e "^a" | wc -l
```

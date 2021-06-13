---
layout: post
title: How to Patch easily in Git
author: cloudjk
tags: [git, patch]
---

### 1. How to create git patch and apply

For example, bugfix/TFH-346 branch is fixed from tfclient-master

1. **git format-patch tfclient-master --stdout > tfh-346.patch**
    - creates tfh-346.patch. (current branch is bugfix/TFH-346, tfclient-maser must be up-to-date)
2. **git checkout mobclient-master && git pull**
3. **git checkout -b bugfix/TFH-346-M**
4. **git apply --check tfh-346.patch**
    - This command usually works well
5. **git apply tfh-346.patch**
    - Next step is commit and push

**If step 4 raise an error then should do manual patch. (can refer to tfh-346.patch)**

### 2. How to do patch manually

1. **create branch from master**
2. **using git lens compare, compare created branch and fixed branch**
3. **apply modified parts to the created branch**
4. **merge created branch to master**

### 3. How to do patch manually with prompt
**git checkout --patch tfapi-master application/config/migration.php**
---
title: What is Fork and how to use it ?
sidebar: mydoc_sidebar
permalink: git_fork_clone_diifference.html
folder: git
---

1. What is Github Fork?

1) Fork creates a copy of the repository of open source library on Github.  
2) After forking it to my Github account, I can clone this copied repository to my local and set up to track it.  
3) The reason why using Fork is do not allow people to commit, push and make progress branches which can mess up the main repository.  
4) So, after forking, people can contribute to the open source library just by pull request.  

2. How to Fork?

[STEP 1] Find the open source library you want to contribute to in Github and then click Fork button top right corner of the screen.  
[STEP 2] After a successful Fork, you can see new library repository is added to your account. Clone it to your local.  
[STEP 3] In the new cloned repository, you can check its remote status.  
[STEP 4] To get sync with original main repository, you need to clone main repository using "git remote add upstream".  


![fork](/assets/img/posts/forkedSuccess.png)
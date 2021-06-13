---
title: Adding SSH Key to GitHub
sidebar: mydoc_sidebar
permalink: git_adding_ssh_key_to_github.html
folder: git
---

1. SSH enables the user to log in to github and submit the request without username and password.  

STEP1) Generate new SSH key  
If you want to generate SSH key as a default file name (id_rsa) then You dont' need to input "~/.ssh/cloudjk_rsa". Just enter.

![Keygen](/assets/img/posts/keygen.png)

STEP2) ADD SSH key to SSH Agent

![SSHAgent](/assets/img/posts/ssh-agent.png)

STEP3) ADD SSH key

![AddSSH](/assets/img/posts/ssh-add.png)

STEP4) Put SSH keys into your github page  

1) Go to your github page and in the settings menu click in "SSH and GPG keys"  
2) Click New SSH key to generate new one  
3) Input title whatever you want  
4) Copy new SSH key to clipboard  

![Clipboard](/assets/img/posts/copy-to-clipboard.png)

STEP5) Add new SSH key to github

![addKey](/assets/img/posts/add-key-to-github.png)

![addedKey](/assets/img/posts/added-key.png)

2. How to create a new respository in github and set up to track remote branch.

STEP1) Create a new repository

![sshAddress](/assets/img/posts/ssh-address.png)

STEP2) Copy SSH address

![setupToTradckdownRemoteBranch](/assets/img/posts/setup-to-track-remote-branch.png)

![setupToTradckdownRemoteBranch](/assets/img/posts/track-remote-branch.png)

3. Trouble shooting

<a href="https://help.github.com/en/github/authenticating-to-github/error-permission-denied-publickey">Permission Denied Error</a>

1) After running "remote add origin", if you run "git push -u origin master" command right away, this will raise an error like below.

![pushError](/assets/img/posts/push-error.png)

**=> Just add file and run commit command and then run push command.**

2) If you come across this error, it means that there is a problem related to adding SSH and Identity is not added properly.

![pushError](/assets/img/posts/permission-denied.png)

3) You can check whether SSH is added properly, by implementing below command. It shows that SSH is not added and so there is no identity.

![checkIdentity](/assets/img/posts/check-identity.png)

4) Running below command will enable to push. And to verify it is added successfully, go back to 3.

![checkIdentity](/assets/img/posts/add-ssh.png)

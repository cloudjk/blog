---
title: Bash
sidebar: mydoc_sidebar
permalink: linux_bash.html
folder: linux
---
### Set variable only for current shell

```bash
VARNAME = "my value"
```

### Set it for current shell and all processes started from current shell (Disappears when session out!!)

```bash
export VARNAME = "my value" # this will add VARNAME to process.env.VARNAME
```

### To set it permanently for all future bash sessions add such lines to your .bashrc(or .zshrc when you use zsh) in your $HOME directory

### To set it permanently and system wide (all users, all processes) add set variable in /etc/environment

```bash
sudo -H gedit /etc/environment
```

### Which Shell am I using?

```bash
echo $SHELL
```

### Where is my home directory?

```bash
echo $HOME
```

### Show me bash manual

```bash
man bash
```

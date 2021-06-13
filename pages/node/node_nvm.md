---
title: NVM
sidebar: mydoc_sidebar
permalink: node_nvm.html
folder: node
---

### Node NVM

Install NVM

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```

Install NVM will add the source lines to ~/.nvm and ~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc
However in mycase, the source lines added only to ~/.bashrc and nvm command didn't work.
So I added them to ~/.zshrc and applied source ~/.zshrc. and it worked!

```bash
nvm ls-remote
```

install previous version using NVM

```bash
nvm i v4
nvm i 4.9.1
```

To use different version

```bash
nvm use v14
```

How to set default version

```bash
nvm alias default 6.11.5
```

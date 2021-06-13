---
layout: post
title: Homebrew
subtitle: Homebrew
author: cloudjk
tags: [java, homebrew]
---

# Homebrew

- [Homebrew](#homebrew)
  - [What is Homebrew?](#what-is-homebrew)
  - [First to install](#first-to-install)
  - [install commands](#install-commands)
  - [remove commands](#remove-commands)
  - [other commands](#other-commands)

## What is Homebrew?

> Package manger for Mac

## First to install

> cask should be installed first.
> cask is a package enable to install programs working with Graphic like Safari, Chrom, Word..

## install commands

```bash
# check if the program to install exists
brew search program_name

# install
brew install program_name

# cask install
brew cask install google-chrome

# check installed program list
brew list

# check installed cask program list
brew cask list

# verify Launchpad it is installed successfully
```

## remove commands

> Programs installed through Homebrew only can be removed

```bash
# check installed list
brew cask list

# remove
brew cask remove karabiner-elements # Purging files ... which means successfully removed

# check program list
brew cask list

# check launch pad
```

## other commands

```bash
# update brew to the latest version
brew update

# update to the latest version
brew upgrade program_name

# remove previous versions not using after update
brew cleanup

# show installed program info
brew info tomcat
```

---
layout: post
title: Git commands cheatsheet
author: cloudjk
tags: [git, cheatsheet]
---

## GIT COMMANDS

![git](/assets/img/posts/git.png)

### Remote Branch Tracking

```git
git branch -u origin/{BRANCH-NAME}
```

### Log in one line

```git
git log --oneline
```

### Revert

```git
git revert head : revert latest commit
git log --oneline
git revert {COMMIT-ID} : revert a specific commit
```

### Delete Local Branch

```git
git branch -d branch_name
git branch -D branch_name : force delete
```

### Delete Remote Branch

```git
git push origin -d {REMOTE-BRANCH-NAME}
```

### Rebase

: When many derived branches are merged, its hitory can be quite messy. By applying rebase instead of merge, commit history can be straigtened up.
It is similar to merge so there is possibility of conflict.

```git
git rebase {BRANCH_NAME, COMMIT-ID}
```

### Reflog

: show reference logs in order

```git
git reflog
```

### Commit amend

```git
git commit --amend -m "new commit message"
```

### Add undo

```git
git reset
```

## Diff

: Shows difference between working directory and stage area

```git
git diff : shows all difference by lines
git diff --color-words : shows difference by word
git diff --word-diff : show difference by word explicitly
```

## Diff HEAD

: Shows difference between working directory and Local repository

```git
git diff head
```

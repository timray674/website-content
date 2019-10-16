---
title: How to update a Git branch from another branch
description: "Given a Git branch that's not up to date with another branch, how do you merge the changes?"
date: 2019-10-17T07:00:00+02:00
tags: git
---

You checkout the branch you want to update:

```sh
git checkout my-branch
```

and you merge from the branch you want to update from:

```sh
git merge another-branch
```

This will create a merge commit, which will include all the differences between the 2 branches - in a single commit.

Also check my [Git guide](/git/).
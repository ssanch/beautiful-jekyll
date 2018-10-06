---
layout: post
title: Ignoring local changes in Git
subtitle: Keep changes local in a file managed by Git
gh-badge: [star, fork, follow]
share-img: /img/javascript.jpg
tags: [tips, git, source control]
---

# Ignoring local changes to file under git management
When working with code solutions that are being managed with Git, we often want to make some local changes. Example of this are configuration files. Maybe we have specific settings in our development environment or we need to connect to specific sources. 

This isn't uncommon and the real problem when this happens is that we want those changes to remain but we don't want to share them with the rest of the team. That leaves us with two options
- Undo your changes every time you commit or pull down changes
- Or ignore those local changes using git

The first one is a burden really. So let's explore the second approach. Our new two favorite commands
```bash
git update-index --skip-worktree
```

### git update-index --skip-worktree

When to use? **Whenever we want changes to be consider local and we do not want Git to manage that change** These essentially means we can change something and Git will ignore such change. Which is exactly what we want most of the times

To execute this just open a terminal and type
``` bash
git update-index --skip-worktree <path to file>
```

There will be no output but you can confirm the change using
```bash
git ls-files -v | grep ^S

# git ls-files  - Lists all files under Git's management
# -v            - Filters the files being ignored
```

Now you might run into a scenario where a user made a change to that file and pushed those changes to the repo. Next time to get latest Git will warn you about your local changes and it will ask you to commit or discard yours before pulling down.

The easiest thing to do is to undo your changes, get latest and merge if needed. So you restore Git's management to the file having conflicts bu running
```bash
git update-index --no-skip-worktree <path to file>

And that's it :)
```
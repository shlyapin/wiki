---
title: Git
layout: page
permalink: /git
nav_order: 3
---

Table of contents:
* Table of contents
{:toc}

# Create a new repository

```
echo "# my_repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:shlyapin/my_repo.git
git push -u origin main
```

# Push an existing repository

```
git remote add origin git@github.com:shlyapin/my_repo.git
git branch -M main
git push -u origin main
```

# Create a new branch

```
git checkout -b my_branch
```

The command above is equivalent to these two commands:

```
git branch my_branch
git checkout my_branch
```

# Make changes and push to GitHub (or an alternative)

```
git add .
git commit -m "Some commit message"
git push --set-upstream origin my_branch
# After the initial --set-upstream, you can just use git push without --set-upstream
```

# Checkout a remote branch

```
git checkout my_branch
```

# Reset a local branch to match the remote main branch

**Warning**: it will discard all local changes.

```
git reset --hard origin/main
```

# Rebase

**Warning**: any command with `--force` is dangerous since it rewrites the commit history.

```
git checkout main
git pull
git checkout my_branch
git rebase main
git push --force
```

Alternatively, if you have multiple remotes:
```
git checkout main
git pull
git fetch origin
git checkout my_branch
git rebase origin/main # Rebases the current branch onto origin/main.
git push --force
```

# Rename a local and remote branch

```
# Rename the local branch to the new name
git branch -m old_branch_name new_branch_name

git push origin --delete old_branch_name

# Prevent git from using the old name when pushing in the next step.
# Otherwise, git will use the old upstream name.
git branch --unset-upstream new_branch_name

# Push the new branch to remote
git push origin new_branch_name

# Reset the upstream branch for the new_branch_name local branch
git push origin -u new_branch_name
```

# Log

```
# show the 5 last commits in short form
git log --pretty=oneline -n 5
```

# Squash

```
# squash the last 3 commits
git rebase -i HEAD~3
```

Or
```
# squash the last 3 commits
git reset --soft HEAD~3
```

# Roll back commits

```
# remove the 2 last commits
git reset HEAD~2 
```

# Restore only one file

```
git checkout HEAD -- my_file.txt
```

# Remove a branch locally and remotely

```
# delete the branch locally
git branch -d my_branch

# delete the branch remotely
git push origin --delete my_branch
```

# Checkout a remote branch no matter what 

When you try to checkout a remote branch, git won't allow you to do this if the changes in your current working directory would be overwritten by the checkout. The commands below checkout a remote branch despite it. Also, they remove all files (including files that are not under version control) in the directory that are not in the remote branch.

**Warning**: potentially dangerous. Read the comment above.

```
git fetch
git clean -xdf
git reset --hard HEAD
git checkout my_branch
git reset origin/my_branch
git clean -xdf
git reset --hard HEAD
```

# Change the URL of a remote repository

```
# For the first time (no origin yet)
git remote add origin git@github.com:shlyapin/my_repo.git
# For the second time and later (origin already exists)
git remote set-url origin git@github.com:shlyapin/my_repo.git
# To check what URL is set
git config --get remote.origin.url
```

# Solve when git status shows all files as modified but the content is not changed

```
# The solution (if it's caused by a change of mode (chmod))
git config core.filemode false
```

# Check the difference between branches

```
git diff my_branch main -- file.py
```

# Merge into main

```
git checkout main
git pull origin main
git merge my_branch
git push origin main
```

# Check the changes that occurred on my_branch since it diverged from main

```
git diff main...my_branch
```

# Other

```
# to abort rebase
git rebase --abort 

# to show differences in comparison with the last commit
git diff
```

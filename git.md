---
title: git
layout: page
permalink: /git
---

# GitHub instruction for new repositories

If you want to create a new repository on the command line

```
echo "# my_repo" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:alshlyapin/my_repo.git
git push -u origin main
```

If you want to push an existing repository from the command line

```
git remote add origin git@github.com:alshlyapin/my_repo.git
git branch -M main
git push -u origin main
```

# Creating a new branch

```
git checkout -b <branch>
# or
git branch <branch>
git checkout <branch>
```

# Actions when changing something

```
git add .
git commit -m "<commit_message>"
git push --set-upstream origin <branch>
# After initial  --set-upstream, you can just use git push without --set-upstream
```

# Force git pull

```
git reset --hard origin/master
```

# Rebase

```
git checkout master
git pull
git fetch origin
git checkout my_branch
git rebase origin/master # Rebases current branch onto origin/maste
git push --force
```

Alternatively, if only one remote
```
git checkout master
git pull
git checkout my_branch
git rebase master
git push --force
```

# Rename local and remote branch

```
# Rename the local branch to the new name
git branch -m <old_branch_name> <new_branch_name>

git push origin --delete <old_branch_name>

# Prevent git from using the old name when pushing in the next step.
# Otherwise, git will use the old upstream name instead of <new_name>.
git branch --unset-upstream <new_branch_name>

# Push the new branch to remote
git push origin <new_branch_name>

# Reset the upstream branch for the new_name local branch
git push origin -u <new_branch_name>
```

# Log

```
# show 5 last commits in short form
git log --pretty=oneline -n 5
```

# Squash

```
# squash last 3 commits
git rebase -i HEAD~3
git commit

# or

git reset --soft HEAD~3
git commit
```

# Roll back a commit

```
# remove 2 last commits
git reset HEAD~2 
```

# Restore only one file

```
git checkout HEAD -- my_file.txt
```

# Remove branch locally and remotely

```
# delete branch locally
git branch -d <branch>

# delete branch remotely
git push origin --delete <branch>

# reset to origin/master
git reset --hard origin/master
```

# Checkout a remote branch

Short version:
```
git checkout <branch>
```

Checkout a remote branch, delete all not commited files
```
git fetch
git clean -xdf
git reset --hard HEAD
git checkout my_branch
git reset origin/my_branch
git clean -xdf
git reset --hard HEAD
```

# Change URL of a remote repo

```
# first time (no origin yet)
git remote add origin https://github.com/user/repo.git
# second time and later (origin already exists)
git remote set-url origin ssh://git@github.com:alshlyapin/my_repo.git
# check what's set
git config --get remote.origin.url
```

# Solve git status shows all files as modified but the content is not changed

```
# solution (if it's caused by change of mode (chmod))
git config core.filemode false
```

# Check difference between branches

```
git diff my_branch master -- file.py
```

# Merge into master

```
git checkout master
git pull origin master
git merge my_branch
git push origin master
```

# Compare a branch to master

```
git diff master...my_branch
```

# Other

```
# to abort rebase
git rebase --abort 

# show differences in comparison with the last commit
git diff
```

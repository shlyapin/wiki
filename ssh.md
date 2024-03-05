---
title: SSH
layout: page
permalink: /ssh
---

# Add SSH connection to config

You can use `ssh my_machine` instead of `ssh my_user@123.456.901.234` to connect to the machine. To do this you need to create or edit a config file for SSH. The path for a user is `~/.ssh/config`

```
Host my_machine
  HostName 123.456.901.234
  User my_user
```

There are a lot of options:

```
Host my_machine
  HostName 123.456.901.234
  IdentityFile ~/.ssh/my_key.pem
  User my_user
  Port 1234
```

You can add multiple connections:

```
Host my_machine
  HostName 123.456.901.234
  User my_user

Host my_machine_2
  HostName 987.654.321.987
  User my_user_2
```

# Send a file to a machine or upload a file from a machine

If you created a config in "Add SSH connection to config" section of this page:

```
# send file to my_machine
scp my_file.txt my_machine:/my/path
# upload file from my_machine
scp my_machine:/my/path/my_file.txt my_file.txt
```

You need to run it from a machine where the SSH config (with my_machine configuration) is stored.

# Allow two users to push to GitHub using different SSH keys on the same Linux machine

`~/.ssh/config`:

```
# User 1's GitHub account
Host github.com-user1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_user1

# User 2's GitHub account
Host github.com-user2
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_user2
```

git clone:

```bash
# For user 1
git clone git@github.com-user1:user1/repo_user1.git

# For user 2
git clone git@github.com-user2:user2/repo_user2.git
```

After that, any Git commands executed in the repo_user1 folder will utilize user1’s keys, and any Git commands performed in the repo_user2 folder will use user2’s keys.

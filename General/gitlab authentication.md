# Git Cheat Sheet and FAQ

## SSH Key Management

### Check Existing SSH Keys

To see what SSH keys you have:

```bash
$ ls -al ~/.ssh
```

### Copy SSH Key to Clipboard

To copy an SSH key to your clipboard (replace <key_to_copy> with your actual key filename):

```bash
$ clip < ~/.ssh/<key_to_copy>
```

### Test SSH Access to GitHub

To check if your SSH key has access:

```bash
$ ssh -T git@github.com
```

## Repository Authentication

### Clone via HTTPS

When SSH causes issues, use HTTPS. Replace placeholders with your details:

```bash
git clone https://oauth2:<GitLab_Access_Token>@gitlab.com/yourusername/project.git project
```

## Update Repository Authentication Method

### Modify the .git/config file to update authentication:

```bash
[remote "origin"]
    url = https://oauth2:<Access_Token>@gitlab.uwe.ac.uk/yourusername/project.git
    fetch = +refs/heads/*:refs/remotes/origin/*
```

## Branch and Remote Management

### Prune Local Remote Branches

Remove local references to deleted remote branches:

```bash
git fetch --prune
```

## Additional Useful Commands

### List Remote Branches

```bash
git branch -r
```

### Delete Local Branch

```bash
git branch -d <branch_name>
```

### Delete Remote Branch

```bash
git push origin --delete <branch_name>
```

## Troubleshooting Tips

* Always ensure your access tokens are current
* Use g`it config --global user.name` and `git config --global user.email` to set up your identity
* When encountering authentication issues, first verify your credentials
#devops

1. Install `git`
```bash
brew install git
git --version
```

2. Configure Git
```bash
git config --global user.name "himanshu864"
git config --global user.email "himanshu864000@gmail.com"
```

3. Check for existing SSH Keys
```bash
ls -al ~/.ssh
```
Look for files named `id_rsa` and `id_rsa.pub`. If exists, you already have an SSH key. Hence, skip 4th step.

4. Generate new SSH keys
```bash
ssh-keygen -t rsa -b 4096 -C "himanshu864000@gmail.com"
```

5. Add SSH Key to SSH Agent
```bash
eval "$(ssh-agent -s)"

ssh-add --apple-use-keychain ~/.ssh/id_rsa
```

6. Add SSH Key to GitHub Account
```bash
# copy public key to clipboard
pbcopy < ~/.ssh/id_rsa.pub
```

And paste it to GitHub Browser > Settings > SSH and GPG keys > New SSH Key

7. Test SSH Connection
```bash
ssh -T git@github.com
```

type `yes` and enter to get the following message if successful

	Hi himanshu864, You've successfully authenticated, but GitHub does not provide shell access.

8. Clone Repositories and Try Pushing changes!

## And you're done!

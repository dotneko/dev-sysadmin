# References and Links

- [Git Reference](http://gitref.org/index.html)
- [Git-Guide for Open Source Contributions](https://github.com/chhavip/Git-Guide)
- [Git Cheatsheet](https://github.com/tiimgreen/github-cheat-sheet)

# Authentication with SSH Key

- Ran into problems with 2FA when trying to connect to my own repository despite trying out various methods using https and personal access tokens.

    - Username: <username> Password <personal-access-token> => Failed

- Eventually was able to successfully authenticate my Github identity using an SSH key ([Stackoverflow...Jossef Harush](http://stackoverflow.com/questions/25550481/git-authentication-fails-after-enabling-2fa):

### Generate new SSH Key with email as label

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### Link key to Github account

- Use `cat ~/.ssh/id_rsa.pub` to output the generated public key, which should output something like:
```
ssh-rsa AAASDFlkajdsflkadsf23j23l4kjkalsdfja ... asdfkEWR== your_email@example.com
```
- Next go to https://github.com > Settings > SSH and GPG keys
- Click on "New SSH key", add a title and paste the key above into the box.

### Change git origin from `https://` to `ssh`

- Go to your repository location and type:

```
git remote set-url origin git@github.com:<github username>/<repository name>
```

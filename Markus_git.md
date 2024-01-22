# How to use Git on Markus without reentering your password

Don't let the words `SSH` and `git` confuse you. You're using this so you don't have to enter your username and password all the time.

Firstly, [follow this](https://github.com/MarkUsProject/Wiki/blob/v2.4.3/SSH_Keypair_Instructions_Linux-OSX.md)

Once you're done:

- Clone the Markus Git repository.
- In your Git repository folder, run this:

```
git remote set-url origin <MARKUS REPOSITORY SSH LINK>
```

Where `<MARKUS REPOSITORY SSH LINK>`  should be in the form:

```
ssh://drprj@markus.teach.cs.toronto.edu/20XX-0X/....git
```

Once you've done that, running `git pull` and `git push` for that repository alone will not require you to authenticate.

## Error messages?

Getting this?

```
fatal: not a git repository (or any parent up to mount point /gpfs)
Stopping at filesystem boundary (GIT_DISCOVERY_ACROSS_FILESYSTEM not set).
```

You're probably in the wrong folder.
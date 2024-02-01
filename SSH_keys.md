# How to SSH without having to type your password every single time

On your Windows command line, run `ssh-keygen`. Follow all steps, keeping all default names. You may leave the passphrase blank.

Then, in a **WSL** instance or on Git Bash (because that's where `ssh-copy-id` exists although I'm pretty sure there's a way to get it on Windows):

- CD to ``C:\Users\%USERNAME%\.ssh``. Remember, WSL uses `/mnt/c` instead of `C:`
- Run `ssh-copy-id -i id_rsa.pub user@host` in that folder. Log in like normal, and once you've finished doing that you can SSH to that server **on the windows terminal (NOT WSL)** without having to enter your password.

## Aliasing

Add this to the `config` file (no extension) if you want to alias the SSH domain:

```
Host <alias>
  HostName <host>
  User <user>
  IdentityFile ~/.ssh/id_rsa
```

Where you should set `<alias>` to be what you want to type in place of `user@host`; `user` is before the `@` and host is after the `@`. For example, `user@host.com` means

```
Host thatoneserveriwanttoconnectto
  HostName host.com
  User user
  IdentityFile ~/.ssh/id_rsa
```

# Sudoer Configuration

As root, add the target user you want to make a sudoer into the `wheel` group:

```
# pw user  mod  famicoman -G wheel
```

Then install `sudo`:

```
# pkg install sudo
```

Now enter `visudo` to edit sudoers:

```
# visudo
```

Uncomment out the following line and save/exit the file:

```
# Uncomment to allow people in group wheel to run all commands
# and set environment variables.
%wheel  ALL=(ALL) SETENV: ALL
```

Now open a NEW console session and log in as the user `famicoman`. Try a `sudo` command:

```
$ sudo ls /root
```

## Sources
* https://www.cyberciti.biz/tips/freebsd-becoming-super-user-su-or-enabling-su-access-to-user.html
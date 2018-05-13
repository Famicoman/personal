# Sudoer Configuration

As root, add the target user you want to make a sudoer into the `wheel` group:

```
# pw user  mod  famicoman -G wheel
```

Now open a NEW console session and log in as the user `famicoman`. Try a `sudo` command:

```
$ sudo ls /root
```

## Sources
* https://www.cyberciti.biz/tips/freebsd-becoming-super-user-su-or-enabling-su-access-to-user.html
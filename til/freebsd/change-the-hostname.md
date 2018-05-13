# Change the Hostname

First, change the hostname in `rc.conf`:

```
# vi /etc/rc.conf
```

Modify the following line and save:

```
hostname="new-server-name-here"
```

This will change the hostname after reboot, but before that happens we can do the following"

```
# hostname new-server-name-here
```

## Sources
* https://www.cyberciti.biz/faq/howot-freebsd-change-hostname-without-reboot/
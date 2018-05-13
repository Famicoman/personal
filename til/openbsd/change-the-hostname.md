# Change the Hostname

First, change the hostname in `myname`:

```
# echo "puffy" >  /etc/myname
```

This will change the hostname after reboot, but before that happens we can do the following"

```
# hostname puffy
```

## Sources
* https://www.cyberciti.biz/faq/howto-openbsd-change-hostname/
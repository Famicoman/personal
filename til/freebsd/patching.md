# Patching the System

We will apply security patches as `root`.

The first command will see what security patches are available. The second will apply the patches:

```
# freebsd-update fetch
# freebsd-update install
```

It's smart to do this as a cron job that runs periodically and uses the `cron` flag. Edit `/etc/crontab` and add the following:

```
@daily                                  root    freebsd-update cron
``

## Sources
* https://www.freebsd.org/doc/handbook/updating-upgrading-freebsdupdate.html
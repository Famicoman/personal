# doas Configuration

`doas` is already included in OpenBSD as a proper alternative to `sudo`.

As root, copy the `doas` example conf to `/etc/doas.conf`:

```
# cp /etc/examples/doas.conf /etc/doas.conf
```

By default, the `wheel` group is already included:

```
# cat /etc/doas.conf

# $OpenBSD: doas.conf,v 1.1 2016/09/03 11:58:32 pirofti Exp $
# Configuration sample file for doas(1).
# See doas.conf(5) for syntax and examples.

# Non-exhaustive list of variables needed to build release(8) and ports(7)
#permit nopass setenv { \
#    FTPMODE PKG_CACHE PKG_PATH SM_PATH SSH_AUTH_SOCK \
#    DESTDIR DISTDIR FETCH_CMD FLAVOR GROUP MAKE MAKECONF \
#    MULTI_PACKAGES NOMAN OKAY_FILES OWNER PKG_DBDIR \
#    PKG_DESTDIR PKG_TMPDIR PORTSDIR RELEASEDIR SHARED_ONLY \
#    SUBPACKAGE WRKOBJDIR SUDO_PORT_V1 } :wsrc

# Allow wheel by default
permit keepenv :wheel
```

If your target user is not in the `wheel` group, add them. As of OpenBSD 6.4, it looks like the primary user created during installation (if any) is already in `wheel`.

```
# usermod -G famicoman wheel
```

Or check with `groups` to make sure they are there:

```
# groups famicoman
famicoman wheel
```

Now exit root and try to do something elevated as your target user:

```
# exit
$ doas -u root ls /root
```
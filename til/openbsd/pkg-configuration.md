# pkg Configuration

If you are starting up OpenBSD for the first time and want to install packages via the handy `pkg` tool, you might discover that it cannot seem to locate any packages. Well, it needs to be configured first.

~~As root, we need to modify `/etc/installurl` and add a mirror to this file:~~ As of OpenBSD 6.4, this is already configured!

```
# vi /etc/installurl

```

~~Paste the URL for a mirror, it should be to only line in the file:~~

```
https://ftp.eu.openbsd.org/pub/OpenBSD/
```

Then, install any package you want:

```
# pkg_add htop
quirks-2.414 signed on 2018-03-29T09:01:59Z
htop-2.1.0:libelf-0.8.13p4: ok
htop-2.1.0:libffi-3.2.1p4: ok
htop-2.1.0:pcre-8.41: ok
htop-2.1.0:bzip2-1.0.6p8: ok
htop-2.1.0:sqlite3-3.22.0p0: ok
htop-2.1.0:python-2.7.14p1: ok
htop-2.1.0:glib2-2.54.3p1: ok
htop-2.1.0:desktop-file-utils-0.23p0: ok
htop-2.1.0: ok
Look in /usr/local/share/doc/pkg-readmes for extra documentation.
--- +python-2.7.14p1 -------------------
If you want to use this package as your default system python, as root
create symbolic links like so (overwriting any previous default):
 ln -sf /usr/local/bin/python2.7 /usr/local/bin/python
 ln -sf /usr/local/bin/python2.7-2to3 /usr/local/bin/2to3
 ln -sf /usr/local/bin/python2.7-config /usr/local/bin/python-config
 ln -sf /usr/local/bin/pydoc2.7  /usr/local/bin/pydoc
```

You can update all packages or specific packages with the `-u` flag as shown:

```
# pkg_add -u
# pkg_add -u htop
```

Deletion can be done via `pkg_delete` with an optional `-a` flag to remove unused dependencies:

```
# pkg_delete -a htop
```

## Sources
* https://www.cyberciti.biz/tips/openbsd-add-package-howto.html
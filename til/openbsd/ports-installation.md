# Ports Installation

Additional packages on OpenBSD can be built using `ports`. By default, OpenBSD does not have `ports` included after OS installation, but it can be added.

The following commands were performed as root:

```
# cd /tmp
# ftp https://ftp.openbsd.org/pub/OpenBSD/$(uname -r)/{ports.tar.gz,SHA256.sig}
# signify -Cp /etc/signify/openbsd-$(uname -r | cut -c 1,3)-base.pub -x SHA256.sig ports.tar.gz
```

This downloads and verifies the `ports.tar.gz` archive. We will now untar this to `/usr` to create `/usr/ports`:

```
# cd /usr
# tar xzf /tmp/ports.tar.gz
```

Now you can install through ports:

```
# cd /usr/ports/net/tor && make && make install
```

When done, make sure you clean up temporary files from the working directory: 

```
# make clean=depends
```

If needed, remove with:

```
# make uninstall
```

## Sources
* https://www.openbsd.org/faq/ports/ports.html
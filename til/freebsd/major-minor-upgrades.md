# Major/Minor Version Upgrades

For what we want to upgrade to the latest **RELEASE** version.

We will apply security patches as `root`.

Run `freebsd-update` and specify the `RELEASE` version to upgrade to. Here, we use `9.1` as an example:

```
# freebsd-update -r 9.1-RELEASE upgrade

Looking up update.FreeBSD.org mirrors... 1 mirrors found.
Fetching metadata signature for 9.0-RELEASE from update1.FreeBSD.org... done.
Fetching metadata index... done.
Inspecting system... done.

The following components of FreeBSD seem to be installed:
kernel/smp src/base src/bin src/contrib src/crypto src/etc src/games
src/gnu src/include src/krb5 src/lib src/libexec src/release src/rescue
src/sbin src/secure src/share src/sys src/tools src/ubin src/usbin
world/base world/info world/lib32 world/manpages

The following components of FreeBSD do not seem to be installed:
kernel/generic world/catpages world/dict world/doc world/games
world/proflibs

Does this look reasonable (y/n)? y
```

Make sure everything is sane and proceed with `y`.

When it finishes, we will write changes to the disk:

```
# freebsd-update install
```

When that is done, restart so the kernel gets patched:

```
# shutdown -r now
```

When the machine comes back on line, run this to clean out the shared libraries and gunk:

```
# freebsd-update install
```

## Sources
* https://www.freebsd.org/doc/handbook/updating-upgrading-freebsdupdate.html
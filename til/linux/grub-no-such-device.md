# Grub: No such device

I made the mistake of installing another copy of Debian on a removable drive and then installing/updating Grub on my primary drive to account for the new installation. I should have installed Grub to the same drive the new OS was installed to. Now, whenever I remove the drive, booting the machine results in launching Grub rescue with a "no such device" error.

Provided that you can get back into the primary installation, I observed no combination of the following commands (with the removable drive removed) seemed to help and on every boot I would have to make sure that the removble drive was inserted to get the Grub menu:

```
# update-grub
# grub-install /dev/sdb
# grub-mkconfig -o /boot/grub/grub.cfg
```

Specifically, `update-grub` outputs the following where it finds two images:

```
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-5.10.0-26-amd64
Found initrd image: /boot/initrd.img-5.10.0-26-amd64
Found linux image: /boot/vmlinuz-5.10.0-22-amd64
Found initrd image: /boot/initrd.img-5.10.0-22-amd64
Warning: os-prober will be executed to detect other bootable partitions.
Its output will be used to detect bootable binaries on them and create new boot entries.
done
```

Grub wants you to edit files in `/etc/grub.d/` and `/etc/default/grub` which are then used by `update-grub` to generated `/boot/grub/grub.cfg`. Reading `grub.cfg` doesn't give us many hints since the menu entries in there all reference files in `/boot/` of the primary drive.

The way I figured out how to fully blow away entries from the removable drive was to figure out the kernel version my primary drive was running:

```
# uname -a
Linux kabelsalat 5.10.0-26-amd64 #1 SMP Debian 5.10.197-1 (2023-09-29) x86_64 GNU/Linux
```

Checking `dpkg` I see another kernel:

```
t# dpkg -l | grep linux-image
rc  linux-image-5.10.0-22-amd64      5.10.178-3                     amd64        Linux 5.10 for 64-bit PCs (signed)
ii  linux-image-5.10.0-26-amd64      5.10.197-1                     amd64        Linux 5.10 for 64-bit PCs (signed)
ii  linux-image-amd64                5.10.197-1                     amd64        Linux for 64-bit PCs (meta-package)
```

We see the same in `/boot`:

```
# ls /boot
config-5.10.0-22-amd64  grub                        initrd.img-5.10.0-26-amd64  System.map-5.10.0-26-amd64  vmlinuz-5.10.0-26-amd64
config-5.10.0-26-amd64  initrd.img-5.10.0-22-amd64  System.map-5.10.0-22-amd64  vmlinuz-5.10.0-22-amd64
```

Uninstall the offending kernel:

```
# apt remove linux-image-5.10.0-22-amd64 --verbose-versions
```

This should ultimately update Grub automatically but we can do the following for safety (notice only one image is found):

```
# update-grub
Generating grub configuration file ...
Found linux image: /boot/vmlinuz-5.10.0-26-amd64
Found initrd image: /boot/initrd.img-5.10.0-26-amd64
Warning: os-prober will be executed to detect other bootable partitions.
Its output will be used to detect bootable binaries on them and create new boot entries.
done
```

The old files are gone from `boot` and you should see a more appropriate number of entries in `/boot/grub/grub.cfg`:

```
# ls /boot
config-5.10.0-26-amd64  grub  initrd.img-5.10.0-26-amd64  System.map-5.10.0-26-amd64  vmlinuz-5.10.0-26-amd64
```
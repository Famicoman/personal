# Format a Large (>2TB) Disk

We have a 4TB drive and we want to use the entirety of the drive in one partition.

Install `parted`:

```
# apt install parted
```

Identify the disk and run `parted` to create the partition:

```
# lsblk -f
# parted /dev/sda
mklabel gpt
mkpart primary 0% 100%
quit
```

Format the partition as `ext4`:

```
# mkfs -t ext4 /dev/sda1
# lsblk -f
```

Make a mount point and set the permissions:

```
# mkdir /mnt/storage
# chown -R $USER:$USER /mnt/storage
```

Add it to `/etc/fstab` so it will mount on boot and then mount it immediately:

```
# cat /etc/fstab | grep /mnt/storage
/dev/sda1       /mnt/storage    ext4    defaults        0       0
# mount -a
```

## Sources
* https://www.cyberciti.biz/tips/fdisk-unable-to-create-partition-greater-2tb.html
* https://www.linuxbabe.com/desktop-linux/how-to-automount-file-systems-on-linux
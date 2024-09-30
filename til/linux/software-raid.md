# Software raid

We have two new hard drives we want to set up using RAID 1 (mirrored).

First, we need to identify the disks we will be using, we will be targeting `/dev/sdb` and `/dev/sdc`:

```
# lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:16   0 111.8G  0 disk
├─sda1   8:17   0 110.8G  0 part /
├─sda2   8:18   0     1K  0 part
└─sda5   8:21   0   975M  0 part [SWAP]
sdb      8:112  0  10.9T  0 disk
sdc      8:128  0  10.9T  0 disk
sr0     11:0    1  1024M  0 rom
```

Now, we setup new MBR partition tables on each of the drives. This will wipe out all the data. Note that we are using `gpt` because our drives are over 2TB:

```
$ sudo parted /dev/sdb mklabel gpt
$ sudo parted /dev/sdc mklabel gpt
```

Next, we use fdisk to create a Linux RAID partition on each drive. Here we will first modify `/dev/sdb`:

```
$sudo fdisk /dev/sdb
```

Follow these instructions:

1) Type `n` to create a new partition
2) Type `1` to create `/dev/sdb1`
3) Press `Enter` to choose default first sector
4) Press `Enter` to choose default last sector
5) Type `t` to change the partition type
6) Enter `29` to select Linux RAID
7) Type `p` to check partiton type
8) Type `w` to write changes and exit.

Follow the same process for `/dev/sdc`.

Now we install `mdadm`:

```
$ sudo apt install mdadm
```

We can create the RAID using the two partitions we just created:

```
$ sudo mdadm --create /dev/md0 --level=mirror --raid-devices=2 /dev/sdb1 /dev/sdc1
```

Check the status of our RAID:

```
$ sudo cat /proc/mdstat
```

Create our file system on the RAID:

```
$ sudo mkfs.ext4 /dev/md0
```

Now we can mount the array to `/mnt/raid0`:

```
$ sudo mkdir /mnt/raid
$ sudo mount /dev/md0 /mnt/raid0`
```

Save our RAID configuration:

```
$ sudo mdadm --detail --scan --verbose | sudo tee -a /etc/mdadm/mdadm.conf
```

Update initramfs:

```
$ sudo update-initramfs -u
```

Now we want to add the array to our `fstab` so it mounts on bootup. First get the UUID of the array:

```
$ sudo blkid | grep md0
/dev/md0: UUID="165d6aea-addf-40eb-a2ca-c13c5542a74e" BLOCK_SIZE="4096" TYPE="ext4"
```

Now add the UUID to our `fstab`:

```
$ sudo nano /etc/fstab`
...
UUID=165d6aea-addf-40eb-a2ca-c13c5542a74e       /mnt/raid0      ext4    defaults,nofail 0       0
```

## Sources

* https://www.linuxbabe.com/linux-server/linux-software-raid-1-setup
* https://www.jeffgeerling.com/blog/2021/htgwa-create-raid-array-linux-mdadm
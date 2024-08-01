# Hard Disk Health Check

Got refurbished drives from GoHardDrive and need to test them out.

First, we need to identify the disk to test, we will be targeting `/dev/sdi`:

```
# lsblk
NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda      8:0    0   3.6T  0 disk
└─sda1   8:1    0   3.6T  0 part /mnt/storage
sdb      8:16   0 111.8G  0 disk
├─sdb1   8:17   0 110.8G  0 part /
├─sdb2   8:18   0     1K  0 part
└─sdb5   8:21   0   975M  0 part [SWAP]
sdh      8:112  0  10.9T  0 disk
sdi      8:128  0  10.9T  0 disk
sr0     11:0    1  1024M  0 rom
```

First, we start with checking to see if the drive supports SMART:

```
# smartctl -i /dev/sdi
smartctl 7.2 2020-12-30 r5155 [x86_64-linux-5.10.0-26-amd64] (local build)
Copyright (C) 2002-20, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF INFORMATION SECTION ===
Device Model:     HUH721212ALE601
Serial Number:    XXXXXXXXX
LU WWN Device Id: 5 000cca 26fe1430e
Firmware Version: LEGL0002
User Capacity:    12,000,138,625,024 bytes [12.0 TB]
Sector Sizes:     512 bytes logical, 4096 bytes physical
Rotation Rate:    7200 rpm
Form Factor:      3.5 inches
Device is:        Not in smartctl database [for details use: -P showall]
ATA Version is:   ACS-2, ATA8-ACS T13/1699-D revision 4
SATA Version is:  SATA 3.2, 6.0 Gb/s (current: 3.0 Gb/s)
Local Time is:    Tue Jul 23 15:05:39 2024 EDT
SMART support is: Available - device has SMART capability.
SMART support is: Enabled
```

Next, a short test:

```
# smartctl -t short /dev/sdi
smartctl 7.2 2020-12-30 r5155 [x86_64-linux-5.10.0-26-amd64] (local build)
Copyright (C) 2002-20, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF OFFLINE IMMEDIATE AND SELF-TEST SECTION ===
Sending command: "Execute SMART Short self-test routine immediately in off-line mode".
Drive command "Execute SMART Short self-test routine immediately in off-line mode" successful.
Testing has begun.
Please wait 1 minutes for test to complete.
Test will complete after Tue Jul 23 22:17:23 2024 EDT
Use smartctl -X to abort test.
```

The test is run on the drive controller itself so after some time we can check the drive and look for `Self-test execution status`:

```
# smartctl --capabilities /dev/sdi
smartctl 7.2 2020-12-30 r5155 [x86_64-linux-5.10.0-26-amd64] (local build)
Copyright (C) 2002-20, Bruce Allen, Christian Franke, www.smartmontools.org

=== START OF READ SMART DATA SECTION ===
General SMART Values:
Offline data collection status:  (0x80) Offline data collection activity
                                        was never started.
                                        Auto Offline Data Collection: Enabled.
Self-test execution status:      (   0) The previous self-test routine completed
                                        without error or no self-test has ever
                                        been run.
```

Not supported on all drives, but it can be good to run a conveyance test:

```
# smartctl -t conveyance /dev/sdi
```

Now a `badblocks` test to check for bad sectors, this will perform 4 rounds of write/verify. Note that this test took ~6 days for a 12TB drive.

```
# badblocks -b 4096 -ws /dev/sdi
```

Finally, a long SMART test. Note that this test took ~1 day for a 12TB drive.

```
# smartctl -t long /dev/sdi
```

Cheaper USB drive adapters can go to sleep after a while and half the test. Monitor it with a loop to keep things awake:

```
#  while true; do smartctl -d sat -c /dev/sdi; sleep 30; done
```
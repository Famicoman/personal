# Installing Debian 11 on APU2C4

## How to Connect

I always forget the specifics of connecting to the APU2 so here is a friendly reminder about the bitrate:

```
screen /dev/ttyUSB0 115200,8n1
```

## Enable Boot Console

We need to make sure the boot console is enabled. For some reason I disabled this before, probably when I hooked this up to a terminal and it freaked out at GRUB.

First, hold the S1 button down on the APU2 (to the left of the SD card) and boot the device, when prompted press `F10` to see the boot menu, then press `6` to go to *Payload [setup]*.

Next, press `t` to toggle serial console and make sure it is enabled. Then press `s` to save and reboot if prompted (I forget if it asks or just does it).

## Create Bootable Debian Device

We meed to get the latest Debian net install iso: https://www.debian.org/distrib/netinst

We can write this to a flash drive with `dd` like this:

```
sudo dd if=debian* of=/dev/sdX bs=8M
```

Or if you somehow need to use Windows like I was forced to after my Mac didn't understand USB drives and I didn't actualy insert the disk into my Linux machine causing big problems, just use unetbootin. 

## Install Debian

This is really as simple as inserting the USB drive into the APU2 and starting it up. On boot, press `F10` to get to the boot menu and select the option to boot from the USB drive (I think it was `1` for me).

At the Debian boot menu, press `tab` to edit the boot parameters. You should get existing parameters like this:

```
/install.amd/vmlinuz vga=788 initrd=/install.amd/gtk/initrd.gz --- quiet
```

The Internet tells me to change it to this, but I'm lazy at retyping things:

```
/install.amd/vmlinuz vga=off initrd=/install.amd/gtk/initrd.gz --- quiet console=ttyS0,115200u8
```

Instead I just append `console=ttyS0,115200n8` to get this:

```
/install.amd/vmlinuz vga=788 initrd=/install.amd/gtk/initrd.gz --- quiet console=ttyS0,115200n8
```

Press `Enter` and then it will freak out and ask you to check VGA modes. Do so and press `0` to select the only one available. This will give you the classic Debian installer over serial!

That's it, do the install as normal. Don't worry about black screens that last for a few seconds, this happens when things are loading.
# dmesg

The `dmesg` command displays the system message buffer's content, and during boot, a copy of it is saved to `/var/run/dmesg.boot`. There is a lot of useful information in there, including the OS release, name and version, identified devices, and other messages. This can be useful to those who are trying to check certain hardware compatibility.

```
openbsd$ dmesg

OpenBSD 6.3 (GENERIC.MP) #491: Sat Mar 24 14:38:11 MDT 2018
    xxx@xxx.xxx:/usr/src/sys/arch/i386/compile/GENERIC.MP
cpu0: Intel(R) Atom(TM) CPU 230 @ 1.60GHz ("GenuineIntel" 686-class) 1.61 GHz
cpu0: FPU,V86,DE,PSE,TSC,MSR,PAE,MCE,CX8,APIC,SEP,MTRR,PGE,MCA,CMOV,PAT,CFLUSH,DS,ACPI,MMX,FXSR,SSE,SSE2,SS,HTT,TM,PBE,NXE,LONG,SSE3,DTES64,MWAIT,DS-CPL,TM2,SSSE3,CX16,xTPR,PDCM,MOVBE,LAHF,PERF,SENSOR
real mem  = 1073233920 (1023MB)
avail mem = 1039650816 (991MB)
mpath0 at root
scsibus0 at mpath0: 256 targets
mainbus0 at root
bios0 at mainbus0: date 11/03/09, BIOS32 rev. 0 @ 0xf0010, SMBIOS rev. 2.6 @ 0xfd740 (26 entries)
bios0: vendor American Megatrends Inc. version "P01-A4" date 11/03/2009
bios0: Acer Aspire R1600
acpi0 at bios0: rev 2
acpi0: sleep states S0 S3 S4 S5
acpi0: tables DSDT FACP APIC MCFG SLIC WDRT OEMB HPET NVHD AWMI
acpi0: wakeup devices SMB0(S4) USB0(S3) USB2(S3) NMAC(S5) PBB0(S4) HDAC(S4) XVR0(S4) XVR1(S4) P0P5(S4) P0P6(S4) P0P7(S4) P0P8(S4) P0P9(S4)
acpitimer0 at acpi0: 3579545 Hz, 32 bits
acpimadt0 at acpi0 addr 0xfee00000: PC-AT compat
cpu0 at mainbus0: apid 0 (boot processor)
mtrr: Pentium Pro MTRR support, 8 var ranges, 88 fixed ranges
cpu0: apic clock running at 133MHz
cpu0: mwait min=64, max=64, C-substates=0.1, IBE
cpu1 at mainbus0: apid 1 (application processor)
cpu1: Intel(R) Atom(TM) CPU 230 @ 1.60GHz ("GenuineIntel" 686-class) 1.60 GHz
cpu1: FPU,V86,DE,PSE,TSC,MSR,PAE,MCE,CX8,APIC,SEP,MTRR,PGE,MCA,CMOV,PAT,CFLUSH,DS,ACPI,MMX,FXSR,SSE,SSE2,SS,HTT,TM,PBE,NXE,LONG,SSE3,DTES64,MWAIT,DS-CPL,TM2,SSSE3,CX16,xTPR,PDCM,MOVBE,LAHF,PERF,SENSOR
ioapic0 at mainbus0: apid 2 pa 0xfec00000, version 11, 24 pins
, remapped to apid 2
acpimcfg0 at acpi0 addr 0xfc000000, bus 0-31
acpihpet0 at acpi0: 25000000 Hz
acpiprt0 at acpi0: bus 0 (PCI0)
acpiprt1 at acpi0: bus 1 (PBB0)
acpiprt2 at acpi0: bus 3 (IXVE)
acpiprt3 at acpi0: bus 2 (XVR0)
acpiprt4 at acpi0: bus -1 (XVR1)
acpiprt5 at acpi0: bus -1 (P0P5)
acpiprt6 at acpi0: bus 4 (P0P6)
acpiprt7 at acpi0: bus 5 (P0P7)
acpiprt8 at acpi0: bus 6 (P0P8)
acpiprt9 at acpi0: bus 7 (P0P9)
acpicpu0 at acpi0: C1(@1 halt!)
acpicpu1 at acpi0: C1(@1 halt!)
acpitz0 at acpi0: critical temperature is 90 degC
"pnp0c14" at acpi0 not configured
acpibtn0 at acpi0: PWRB
"PNP0C14" at acpi0 not configured
bios0: ROM list: 0xc0000/0xec00
pci0 at mainbus0 bus 0: configuration mode 1 (bios)
pchb0 at pci0 dev 0 function 0 "NVIDIA MCP79 Host" rev 0xb1
"NVIDIA MCP79 Memory" rev 0xb1 at pci0 dev 0 function 1 not configured
pcib0 at pci0 dev 3 function 0 "NVIDIA MCP79 ISA" rev 0xb3
"NVIDIA MCP79 Memory" rev 0xb1 at pci0 dev 3 function 1 not configured
nviic0 at pci0 dev 3 function 2 "NVIDIA MCP79 SMBus" rev 0xb1
iic0 at nviic0
adt0 at iic0 addr 0x2e: adt7476 rev 0x69
iic1 at nviic0
spdmem0 at iic1 addr 0x50: 512MB DDR2 SDRAM non-parity PC2-5300CL5 SO-DIMM
spdmem1 at iic1 addr 0x51: 1GB DDR2 SDRAM non-parity PC2-6400CL6 SO-DIMM
"NVIDIA MCP79 Memory" rev 0xb1 at pci0 dev 3 function 3 not configured
"NVIDIA MCP79 Co-processor" rev 0xb1 at pci0 dev 3 function 5 not configured
ohci0 at pci0 dev 4 function 0 "NVIDIA MCP79 USB" rev 0xb1: apic 2 int 9, version 1.0, legacy support
ehci0 at pci0 dev 4 function 1 "NVIDIA MCP79 USB" rev 0xb1: apic 2 int 15
usb0 at ehci0: USB revision 2.0
uhub0 at usb0 configuration 1 interface 0 "NVIDIA EHCI root hub" rev 2.00/1.00 addr 1
azalia0 at pci0 dev 8 function 0 "NVIDIA MCP79 HD Audio" rev 0xb1: apic 2 int 10
azalia0: codecs: Realtek ALC662, NVIDIA/0x0007, using Realtek ALC662
audio0 at azalia0
ppb0 at pci0 dev 9 function 0 "NVIDIA MCP79 PCIE" rev 0xb1
pci1 at ppb0 bus 1
nfe0 at pci0 dev 10 function 0 "NVIDIA MCP79 LAN" rev 0xb1: apic 2 int 11, address xx:xx:xx:xx:xx:xx
rgephy0 at nfe0 phy 1: RTL8169S/8110S/8211 PHY, rev. 2
pciide0 at pci0 dev 11 function 0 "NVIDIA MCP79 SATA" rev 0xb1: DMA
pciide0: using apic 2 int 5 for native-PCI interrupt
ppb1 at pci0 dev 12 function 0 "NVIDIA MCP79 PCIE" rev 0xb1: apic 2 int 10
pci2 at ppb1 bus 2
ppb2 at pci0 dev 16 function 0 "NVIDIA MCP79 PCIE" rev 0xb1
pci3 at ppb2 bus 3
vga1 at pci3 dev 0 function 0 vendor "NVIDIA", unknown product 0x087e rev 0xb1
wsdisplay0 at vga1 mux 1: console (80x25, vt100 emulation)
wsdisplay0: screen 1-5 added (80x25, vt100 emulation)
ppb3 at pci0 dev 21 function 0 "NVIDIA MCP79 PCIE" rev 0xb1: apic 2 int 11
pci4 at ppb3 bus 4
ppb4 at pci0 dev 22 function 0 "NVIDIA MCP79 PCIE" rev 0xb1: apic 2 int 9
pci5 at ppb4 bus 5
ppb5 at pci0 dev 23 function 0 "NVIDIA MCP79 PCIE" rev 0xb1: apic 2 int 15
pci6 at ppb5 bus 6
ppb6 at pci0 dev 24 function 0 "NVIDIA MCP79 PCIE" rev 0xb1: apic 2 int 14
pci7 at ppb6 bus 7
isa0 at pcib0
isadma0 at isa0
pckbc0 at isa0 port 0x60/5 irq 1 irq 12
pckbd0 at pckbc0 (kbd slot)
wskbd0 at pckbd0: console keyboard, using wsdisplay0
pcppi0 at isa0 port 0x61
spkr0 at pcppi0
npx0 at isa0 port 0xf0/16: reported by CPUID; using exception 16
usb1 at ohci0: USB revision 1.0
uhub1 at usb1 configuration 1 interface 0 "NVIDIA OHCI root hub" rev 1.00/1.00 addr 1
umass0 at uhub0 port 3 configuration 1 interface 0 "Kingston DataTraveler 2.0" rev 2.00/1.00 addr 2
umass0: using SCSI over Bulk-Only
scsibus1 at umass0: 2 targets, initiator 0
sd0 at scsibus1 targ 1 lun 0: <Kingston, DataTraveler 2.0, PMAP> SCSI2 0/direct removable serial.09306545EDB1E9320389
sd0: 14887MB, 512 bytes/sector, 30489408 sectors
uhidev0 at uhub1 port 1 configuration 1 interface 0 "Dell Dell USB Keyboard" rev 1.10/3.01 addr 2
uhidev0: iclass 3/1
ukbd0 at uhidev0: 8 variable keys, 6 key codes
wskbd1 at ukbd0 mux 1
wskbd1: connecting to wsdisplay0
uhidev1 at uhub1 port 4 configuration 1 interface 0 "PixArt HP USB Optical Mouse" rev 2.00/1.00 addr 3
uhidev1: iclass 3/1
ums0 at uhidev1: 3 buttons, Z dir
wsmouse0 at ums0 mux 0
vscsi0 at root
scsibus2 at vscsi0: 256 targets
softraid0 at root
scsibus3 at softraid0: 256 targets
root on sd0a (004b44eb2399d74b.a) swap on sd0b dump on sd0b
```

`dmesg` logs can be submitted to http://dmesgd.nycbug.org/
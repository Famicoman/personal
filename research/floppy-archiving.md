# Floppy Archiving

* DiscVaccuum - https://hackaday.com/2014/01/10/a-diskvaccuum-for-obsolete-disk-formats/#more-112048
* Rescuing Floppy Disks - https://www.archiveteam.org/index.php?title=Rescuing_Floppy_Disks
* Digital Archaeology: Recovering your Digital History - https://www.nypl.org/blog/2012/07/23/digital-archaeology-recovering-your-digital-history

## Hardware

* Catweasel (90 Pounds retail, $Hundreds now)
	* Meant for Amigas and PCs, PCI
	* 4 Versions
	* Read/Write
* DiscFerret - ~ $130
	* Inspired by Catweasel, more features
* KryoFlux {minimal write} - 90 Pounds for baseline
	* Captures magnetic flux, not just data
	* 3.5'' and 5.25''
* FC5025 {read-only} - $55
	* Cheap and Basic (supports less formats)
	* Might not handle copy protection well
* FDADAP - $40
	* Board to connect 8” drives to a more modern floppy cable
* Zoom Floppy
	* Can do commodore flippy disks
	
## Software

* Omniflop
	* Supports most things under the sun
	* Free
* Disk2FDI - 30 Euro Shareware
	* Makes formatted disk images.
	* Need 2 floppy drives for many operations
* dd (linux)
* daread (DOS, ported)

```--------------------------------------------------------------------------------
Amiga:
--------------------------------------------------------------------------------
Imager: Disk2FDI {commercial, 9x only, requires 2 internal floppy drives}
Imager: ADFRead {requires 2 internal floppy drives}

Hardware: AFR, http://afr.back2roots.org/ {requires external Amiga floppy drive}

--------------------------------------------------------------------------------
Atari:
--------------------------------------------------------------------------------
Imager: Disk2FDI {commercial, 9x only, requires 2 internal floppy drives?}
Imager: OmniFlop

--------------------------------------------------------------------------------
Acorn:
--------------------------------------------------------------------------------
Imager: OmniDisk {DOS/9x only, also supports BBC Micro 5.25" disks + tons of other obscure stuff}
Imager: OmniFlop {also supports BBC Micro 5.25" disks + tons of other obscure stuff}
Imager: ArcDisk {DOS/9x only}

Emulator: VirtualA5000, VirtualRPC {commercial, needs RISC OS imaging app like ADFimager, or ADFFS for copy protected disks}

Image Reader: ADFS Explorer

--------------------------------------------------------------------------------
Apple:
--------------------------------------------------------------------------------
Imager: OmniFlop
Imager: MacDrive {commercial}
Imager: MacDisk {commercial}
Imager: TransMac {commercial}

Emulator: Basilisk II

--------------------------------------------------------------------------------
Spectrum, Tandy, C64, machines that don't even exist
--------------------------------------------------------------------------------
Imager: OmniFlop {Epic, epic, epic, epic, epic.}

--------------------------------------------------------------------------------
Everything:
--------------------------------------------------------------------------------
Hardware: Catweasel
Hardware: DiscFerret
Hardware: KryoFlux {minimal write}
Hardware: FC5025 {read-only}```
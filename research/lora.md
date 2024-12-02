# LoRa

* Custom LoRa Pager - https://hackaday.com/2019/03/24/custom-lora-pager-designed-with-care/
* Beartooth - https://beartooth.com/

## Ripple Messenger

* https://www.instructables.com/id/LoRa-Mesh-Radio/
* https://github.com/spleenware/ripple
* https://github.com/espressif/esptool
* https://randomnerdtutorials.com/installing-the-esp32-board-in-arduino-ide-windows-instructions/

```
C:\Users\Mike\AppData\Local\Arduino15\packages\esp32\tools\esptool_py\2.6.1/esptool --chip esp32 --port /dev/cu.SLAB_USBtoUART --baud 921600 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 80m --flash_size detect 0xe000C:\Users\Mike\AppData\Local\Arduino15/packages/esp32/hardware/esp32/1.0.4/tools/partitions/boot_app0.bin 0x1000 C:\Users\Mike\AppData\Local\Arduino15/packages/esp32/hardware/esp32/1.0.4/tools/sdk/bin/bootloader_dio_80m.bin 0x10000 RippleV3-Bluetooth-TTGOV2.bin 0x8000 RippleV3-Bluetooth-TTGOV2.partitions.bin
```

## Meshtastic

* https://www.meshtastic.org/

## Disaster radio

* https://disaster.radio/

## Tools for RF

* Line of Sight Mapper - https://www.scadacore.com/tools/rf-path/rf-line-of-sight/
* MeshMap (Meshtastic) - https://meshmap.net/

## Antennas 

* https://www.mouser.com/ProductDetail/Taoglas/TI.92.2113?qs=P1JMDcb91o7ty6jAS%2Fx1TA%3D%3D
* https://www.mouser.com/ProductDetail/Pulse-Electronics/W1063M?qs=opBjA1TV90175GTfjmKkCg%3D%3D
* https://www.mouser.com/ProductDetail/Maxtena/MEA-915-SW-SMA?qs=aP1CjGhiNiGjQNdaSEvwhg%3D%3D
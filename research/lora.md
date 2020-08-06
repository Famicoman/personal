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
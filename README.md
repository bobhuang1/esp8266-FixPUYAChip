# esp8266-FixPUYAChip

> **Deprecated.** ESP8266 Arduino core **2.5.0 and later** handle PUYA flash chips
> themselves. Use a current core instead of this file.

Some ESP-01 modules ship with a PUYA flash chip (JEDEC ID `0x146085`). Unlike
other SPI flash chips, a PUYA chip does not AND newly written bits with the
data already in flash, which breaks SPIFFS, EEPROM and OTA updates. This repo
holds a patched `Esp.cpp` whose `EspClass::flashWrite()` does that AND in
software on PUYA chips.

## Usage (old cores only)

The file is a snapshot of the **2.4.x** core's `cores/esp8266/Esp.cpp`. It does
not match the 2.5+/3.x `Esp.h` and will not build there.

1. Find your core: `%LOCALAPPDATA%\Arduino15\packages\esp8266\hardware\esp8266\2.4.x\cores\esp8266\`.
2. Back up that folder's `Esp.cpp` and replace it with this one.
3. Re-apply after every core update, which overwrites it.

Writes must be a multiple of 4 bytes (as `spi_flash_write` requires); other
sizes return `false`.


## License

This project is free software, released under the **GNU General Public License v3.0**. You may redistribute and/or modify it under those terms; see [LICENSE.md](LICENSE.md) for the full text.

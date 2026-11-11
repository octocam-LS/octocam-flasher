# Octocam firmware installer

Web page for installing Octocam firmware over USB with [ESP Web Tools](https://esphome.github.io/esp-web-tools/)
(Chrome / Edge, Web Serial). Live at https://octocam-ls.github.io/octocam-flasher/

| Folder | Device | Chip | Version |
|---|---|---|---|
| `firmware/ls-sender-c6` | Octocam LS Sender | XIAO ESP32-C6 | 2.2.0 |
| `firmware/ls-sender-8266` | Octocam LS Sender (legacy) | Wemos D1 mini ESP8266 | 2.4.0-8266 |
| `firmware/trigger-c3` | Octocam Trigger, OLED | ESP32-C3 | 1.2.3 |

Each folder holds the separate parts from Arduino IDE "Export Compiled Binary":
bootloader `0x0`, partition table `0x8000`, `boot_app0` `0xE000`, app `0x10000`.
The NVS area (`0x9000`) is not written, so settings and pairings survive an update
unless "Erase device" is ticked.

ESP8266 (`ls-sender-8266`): one part only, the app `.bin` from arduino-cli / "Export Compiled Binary"
at `0x0` (FQBN `esp8266:esp8266:d1_mini:eesz=4M2M`). The emulated EEPROM sector (`0x3FA000`,
settings + pairings) is not written, so it survives unless "Erase device" is ticked.

To update: replace `firmware.bin` (and bootloader / partitions if they changed) and bump
`version` in that folder's `manifest.json` and on `index.html`.

# Seeed Studio XIAO ESP32-C3

The XIAO ESP32-C3 runs ESPHome and communicates with the Veris meter through the
matching RS-485 expansion board.

## Project pin assignments

| Function | XIAO pin | ESP32-C3 GPIO |
|---|---:|---:|
| RS-485 direction enable | D2 | GPIO4 |
| UART transmit | D4 | GPIO6 |
| UART receive | D5 | GPIO7 |

These assignments match Seeed Studio's RS-485 example for the XIAO ESP32-C3.
They are defined in [`config//veris-8100.yaml`](/config/veris-8100.yaml).

## References

- [Manufacturer product page](https://www.seeedstudio.com/Seeed-XIAO-ESP32C3-p-5431.html)
- [Official getting-started guide and pin map](https://wiki.seeedstudio.com/XIAO_ESP32C3_Getting_Started/)
- [Front pinout image](../../images/hardware/seeed_xiao/seeed_studio_xiao_esp32c3plus_front_pinout.png)
- [Rear pinout image](../../images/hardware/seeed_xiao/seeed_studio_xiao_esp32c3plus_rear_pinout.png)

## Installation notes

- Attach the external Wi-Fi antenna before final installation.
- Align the XIAO headers carefully with the expansion board.
- Do not power the assembly simultaneously from conflicting power sources.

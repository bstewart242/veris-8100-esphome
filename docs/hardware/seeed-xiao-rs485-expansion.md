# Seeed Studio XIAO RS-485 Expansion Board

This board provides the half-duplex RS-485 transceiver between the XIAO
ESP32-C3 UART and the H8163-CB.

## Project connections

| Expansion-board terminal | H8163-CB terminal |
|---|---|
| A | TX+/RX+ |
| B | TX-/RX- |

The H8163-CB must be configured for 2-wire operation. Use twisted-pair cable,
keep polarity consistent, and fit 120-ohm termination at the last device on a
long bus as directed by the Veris manual.

## References

- [Manufacturer product page](https://www.seeedstudio.com/RS485-Breakout-Board-for-XIAO-p-5724.html)
- [Official Seeed Studio wiki](https://wiki.seeedstudio.com/XIAO-RS485-Expansion-Board/)
- [Local schematic PDF](seeed_xiao/seeed_studio_xiao_rs485_expansion_board.pdf)
- [Project installation photos](../../images/hardware/seeed_xiao/)

The local PDF is a schematic rather than a complete installation manual. This
Markdown page provides the project-specific context while the official wiki
remains the best source for board usage.

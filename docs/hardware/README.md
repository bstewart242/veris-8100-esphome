# Hardware documentation

Each component has a Markdown page that explains how it is used in this project
and links to both the manufacturer and the locally archived source material.

| Component | Notes | Local reference |
|---|---|---|
| Seeed Studio XIAO ESP32-C3 | [Pin assignments](seeed-xiao-esp32-c3.md) | Project pinout images in [`../../images/hardware/seeed_xiao/`](../../images/hardware/seeed_xiao/) |
| XIAO RS-485 Expansion Board | [Interface and wiring](seeed-xiao-rs485-expansion.md) | [Schematic PDF](seeed_xiao/seeed_studio_xiao_rs485_expansion_board.pdf) |
| Veris H8163-CB | [DIP switches and RS-485 wiring](veris-h8163-cb.md) | [Installation guide PDF](veris/h8163_modbus_communications_board_installation_guide.pdf) |
| Veris H8167 / H81xx | [Meter notes](veris-h8167.md) | [Installation guide PDF](veris/h81xx_installation_guide.pdf) |

## Safety

The meter is installed around hazardous mains voltage. Disconnect power, verify
the circuit is de-energized, follow the manufacturer instructions, and use a
qualified electrician where required. This repository is not a substitute for
the official installation manuals or applicable electrical codes.

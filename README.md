# Veris 8100 ESPHome

An ESPHome-to-Modbus interface for Veris 8100 Series energy meters, built with a
Seeed Studio XIAO ESP32-C3 and its RS-485 expansion board.

The project exposes energy, power, voltage, current, power-factor, and demand
measurements to Home Assistant.

## Hardware

| Component | Project documentation | Manufacturer |
|---|---|---|
| Veris H8167 Energy Meter | [Hardware notes](docs/hardware/veris-h8167.md) | [Veris H81xx Series](https://www.veris.com/) |
| Veris H8163-CB Modbus Communications Board | [Configuration and wiring](docs/hardware/veris-h8163-cb.md) | [Veris Industries](https://www.veris.com/) |
| Seeed Studio XIAO ESP32-C3 | [Pin assignments](docs/hardware/seeed-xiao-esp32-c3.md) | [Product page](https://www.seeedstudio.com/Seeed-XIAO-ESP32C3-p-5431.html) |
| XIAO RS-485 Expansion Board | [Wiring notes](docs/hardware/seeed-xiao-rs485-expansion.md) | [Product page](https://www.seeedstudio.com/RS485-Breakout-Board-for-XIAO-p-5724.html) |

The downloaded manufacturer manuals, schematics, and project photos are indexed
in [the hardware documentation](docs/hardware/README.md).

## Software
- HomeAssistant
- ESPHome Builder Plugin

## Quick start

1. Install the XIAO ESP32-C3 on the RS-485 expansion board.
2. Configure the H8163-CB for 2-wire RS-485, 9600 baud, no parity, and a unique
   Modbus address. The default configuration expects address `1`.
3. With power disconnected, connect the H8163-CB `TX+/RX+` terminal to RS-485
   `A` and `TX-/RX-` to `B`. Follow the manufacturer manual and local electrical
   codes.
4. Copy `config/secrets.example.yaml` to `secrets.yaml` and enter your Wi-Fi and
   ESPHome credentials.
5. Validate and install [`veris-8100.yaml`](config/veris-8100.yaml) with ESPHome.
6. Validate readings before relying on the data. 

## Repository layout

```text
.
├── .github/                 GitHub issue and pull-request templates
├── config/                  Configuration files
├── docs/
│   ├── hardware/            Component notes and manufacturer manuals
│   └── software/            ESPHome and Modbus documentation
├── hardware/
│   └── mounting-bracket/    CAD sources, exports, and drawings
├── images/                  Project photos and diagrams
├── src/                     Future custom source components
├── veris-8100.yaml          Main ESPHome configuration
└── secrets.example.yaml     Safe credential template
```

## Exposed measurements

The reference configuration exposes:

- Total energy, real power, reactive power, apparent power, and power factor
- Average line voltage, phase voltage, and current
- Per-phase voltage, current, real power, and power factor
- Present, peak, and reactive demand

Some phase values are unavailable on single- or split-phase meter variants. See
the [validated register map](docs/software/modbus-registers.md) for model-specific
details.

![Home Assistant Exposed Measurements](images/Home%20Assistant%20Exposed%20Entities.jpg)


## Documentation

- [Documentation index](docs/README.md)
- [Hardware documentation](docs/hardware/README.md)
- [Software and configuration notes](docs/software/README.md)
- [Modbus register map](docs/software/modbus-registers.md)
- [Mounting-bracket workspace](hardware/mounting-bracket/README.md)

## Status

This is a field project, not a manufacturer-supported integration. The register
map has been transcribed from the Veris documentation, but the completed build
should be tested against a known meter before deployment.

## Changelog

Changes are recorded in [CHANGELOG.md](CHANGELOG.md).

## License

Licensed under the [MIT License](LICENSE.md).

# Veris H8163-CB Modbus Communications Board

The H8163-CB adds Modbus RTU communication to the Veris H81xx meter.

## Reference configuration

The supplied ESPHome configuration expects:

| Setting | Value |
|---|---|
| Protocol | Modbus RTU |
| Wiring | 2-wire RS-485 |
| Baud rate | 9600 |
| Parity | None |
| ESPHome default address | 1 |

Set address DIP switches 1–6 to the desired address from 1 through 63, then set
the same value in the `modbus_address` substitution in
[`../../veris-8100.yaml`](../../veris-8100.yaml).

For the communication-settings DIP bank, the reference setup is:

| Switch | Position | Meaning |
|---:|:---:|---|
| 1 | Off | Unused |
| 2 | On | 2-wire |
| 3 | Off | 9600 baud selection |
| 4 | On | 9600 baud selection |
| 5 | Off | No parity selection |
| 6 | Off | No parity selection |

## 2-wire terminal connection

Connect the combined `TX+/RX+` terminal to RS-485 `A` and `TX-/RX-` to `B`.
Install the supplied 120-ohm termination resistor only when the meter is the last
device on the RS-485 bus.

## References

- [Manufacturer website](https://www.veris.com/)
- [Local H8163-CB installation guide](veris/h8163_modbus_communications_board_installation_guide.pdf)
- [Validated Modbus register map](../software/modbus-registers.md)
- [Project photos](../../images/hardware/veris/)

Always confirm switch labels and terminal markings against the local installation
guide before energizing the equipment.

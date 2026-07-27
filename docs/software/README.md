# Software documentation

The main ESPHome configuration is
[`../../veris-8100.yaml`](../../veris-8100.yaml). The complete meter reference is
in the [Modbus register map](modbus-registers.md).

## Configuration

1. Copy `secrets.example.yaml` to `secrets.yaml`.
2. Replace every placeholder in `secrets.yaml`.
3. Match `modbus_address` in the main YAML to the H8163-CB address switches.
4. Validate the configuration with ESPHome before installation.

The repository ignores `secrets.yaml` and other `secrets.*` files, but explicitly
keeps `secrets.example.yaml`.

## Default serial settings

- 9600 baud
- 8 data bits
- No parity
- 1 stop bit
- 2-wire Modbus RTU
- 30-second polling interval

## Register interpretation

The H8163-CB guide prints the float points as addresses such as `257/258`.
The configuration uses those printed start addresses directly. The values are
32-bit IEEE-754 floats and default to ESPHome's `FP32` high-word-first order.

If communication succeeds but all numeric values are implausible:

1. Confirm the meter address, baud rate, parity, polarity, and 2-wire switch.
2. Confirm whether the installed device expects the printed address or a
   zero-based offset.
3. Test `FP32_R` in place of `FP32` if the device returns low-word-first data.

Record any field-validated address or word-order correction in the register map
and changelog.

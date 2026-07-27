# Veris H8163-CB Modbus Registers

Register reference for the Veris H8163-CB Modbus Communication Board for the H81xx/H8163 energy meter.

Source: [Veris H8163-CB Installation Guide, document Z202879-0D (2012)](https://www.veris.com/ASSETS/DOCUMENTS/ITEMS/EN/h8163-cb_i0d2.pdf), pages 7-12.

## Table of contents

- [Conventions](#conventions)
- [Measured energy and power](#measured-energy-and-power-points-1-6)
- [Voltage, current, and per-phase measurements](#voltage-current-and-per-phase-measurements-points-7-24)
- [Demand measurements](#demand-measurements-points-25-30)
- [Counters and configuration](#counters-and-configuration-points-31-40)
- [Commands, status, timestamps, and identification](#commands-status-timestamps-and-identification-points-41-59)
- [Integer scaling](#integer-scaling)
- [Model applicability](#model-applicability)
- [Operational notes](#operational-notes)
- [Verification notes](#verification-notes)

## Conventions

- Addresses are reproduced exactly as the guide prints them. The `Int` column is the 16-bit integer point address. Where present, `Float` is a pair of consecutive 16-bit addresses containing one read-only 32-bit IEEE real value.
- `R` means read-only. `R/W` means the integer point is readable and writable. A corresponding float point, when present, remains read-only; write operations must target the integer point.
- `NV` means the value is stored in non-volatile memory.
- For measured points 1-30, prefer the float representation. To convert an integer representation, multiply by the applicable multiplier or divide by the applicable divisor in [Integer scaling](#integer-scaling).
- Model suffixes `-1`, `-2`, and `-3` are reproduced from the source. See [Model applicability](#model-applicability).
- `LSB` and `MSB` describe the low and high bytes of one 16-bit integer point. `LSW` and `MSW` describe the low and high 16-bit words of the serial number.
- The guide calls these entries Modbus “points” and does not state a zero-based protocol offset or register-table/function-code convention. Do not subtract one unless the client or gateway documentation explicitly requires it.

## Measured energy and power (points 1-6)

| Int | Float | Name | Data type | Units | Access | NV | Notes |
|---:|:---:|---|---|---|:---:|:---:|---|
| 1 | 257/258 | Energy consumption, low-word integer | 16-bit integer / IEEE-754 float32 | kWh | R | Yes | Points 1 and 2 form the integer energy value. Float 257/258 and float 259/260 contain the same floating-point value. |
| 2 | 259/260 | Energy consumption, high-word integer | 16-bit integer / IEEE-754 float32 | kWh | R | Yes | High integer word; float value duplicates 257/258. |
| 3 | 261/262 | Real power | 16-bit integer / IEEE-754 float32 | kW | R | No | - |
| 4 | 263/264 | Reactive power | 16-bit integer / IEEE-754 float32 | kVAR | R | No | - |
| 5 | 265/266 | Apparent power | 16-bit integer / IEEE-754 float32 | kVA | R | No | Source spells “Apparant”; normalized here. |
| 6 | 267/268 | Total power factor | 16-bit integer / IEEE-754 float32 | PF | R | No | - |

## Voltage, current, and per-phase measurements (points 7-24)

| Int | Float | Name | Data type | Units | Access | Models / notes |
|---:|:---:|---|---|---|:---:|---|
| 7 | 269/270 | Average line-to-line voltage | 16-bit integer / IEEE-754 float32 | V L-L | R | `-1`: unavailable (`0xFFFF`/NaN); `-2`: average of 1; `-3`: average of 3. |
| 8 | 271/272 | Average line-to-neutral voltage | 16-bit integer / IEEE-754 float32 | V L-N | R | `-1`: average of 1; `-2`: average of 2; `-3`: average of 3. |
| 9 | 273/274 | Average current | 16-bit integer / IEEE-754 float32 | A | R | `-1`: average of 1; `-2`: average of 2; `-3`: average of 3. |
| 10 | 275/276 | Real power, phase A | 16-bit integer / IEEE-754 float32 | kW | R | `-1`: same as point 3; `-2/-3`: phase A. |
| 11 | 277/278 | Real power, phase B | 16-bit integer / IEEE-754 float32 | kW | R | `-1`: unavailable (`0xFFFF`/NaN); `-2/-3`: phase B. |
| 12 | 279/280 | Real power, phase C | 16-bit integer / IEEE-754 float32 | kW | R | `-1/-2`: unavailable (`0xFFFF`/NaN); `-3`: phase C. |
| 13 | 281/282 | Power factor, phase A | 16-bit integer / IEEE-754 float32 | PF | R | `-1`: same as total PF (point 6); `-2/-3`: phase A. |
| 14 | 283/284 | Power factor, phase B | 16-bit integer / IEEE-754 float32 | PF | R | `-1`: unavailable (`0xFFFF`/NaN); `-2/-3`: phase B. |
| 15 | 285/286 | Power factor, phase C | 16-bit integer / IEEE-754 float32 | PF | R | `-1/-2`: unavailable (`0xFFFF`/NaN); `-3`: phase C. |
| 16 | 287/288 | Voltage, phase A-B | 16-bit integer / IEEE-754 float32 | V | R | `-1`: unavailable (`0xFFFF`/NaN); `-2/-3`: available. |
| 17 | 289/290 | Voltage, phase B-C | 16-bit integer / IEEE-754 float32 | V | R | `-1/-2`: unavailable (`0xFFFF`/NaN); `-3`: available. |
| 18 | 291/292 | Voltage, phase A-C | 16-bit integer / IEEE-754 float32 | V | R | `-1/-2`: unavailable (`0xFFFF`/NaN); `-3`: available. |
| 19 | 293/294 | Voltage, phase A-N | 16-bit integer / IEEE-754 float32 | V | R | `-1`: same as average L-N (point 8); `-2/-3`: available. |
| 20 | 295/296 | Voltage, phase B-N | 16-bit integer / IEEE-754 float32 | V | R | `-1`: unavailable (`0xFFFF`/NaN); `-2/-3`: available. |
| 21 | 297/298 | Voltage, phase C-N | 16-bit integer / IEEE-754 float32 | V | R | `-1/-2`: unavailable (`0xFFFF`/NaN); `-3`: available. |
| 22 | 299/300 | Current, phase A | 16-bit integer / IEEE-754 float32 | A | R | `-1`: same as average current (point 9); `-2/-3`: available. |
| 23 | 301/302 | Current, phase B | 16-bit integer / IEEE-754 float32 | A | R | `-1`: unavailable (`0xFFFF`/NaN); `-2/-3`: available. |
| 24 | 303/304 | Current, phase C | 16-bit integer / IEEE-754 float32 | A | R | `-1/-2`: unavailable (`0xFFFF`/NaN); `-3`: available. |

## Demand measurements (points 25-30)

| Int | Float | Name | Data type | Units | Access | NV | Notes |
|---:|:---:|---|---|---|:---:|:---:|---|
| 25 | 305/306 | Present demand sub-interval | 16-bit integer / IEEE-754 float32 | kW | R | No | Currently accumulating sub-interval demand; changes continuously. |
| 26 | 307/308 | Present demand | 16-bit integer / IEEE-754 float32 | kW | R | No | Updated after every sub-interval; average of the previous N sub-intervals, where N is point 37. |
| 27 | 309/310 | Peak demand | 16-bit integer / IEEE-754 float32 | kW | R | Yes | Highest point-26 value observed; shown as MAX kW on the LCD when the communication board is present. |
| 28 | 311/312 | Present kVAR sub-interval | 16-bit integer / IEEE-754 float32 | kVAR | R | No | Currently accumulating sub-interval reactive demand; changes continuously. |
| 29 | 313/314 | Present kVAR | 16-bit integer / IEEE-754 float32 | kVAR | R | No | Updated after every sub-interval; average of the previous N sub-intervals, where N is point 37. |
| 30 | 315/316 | Peak kVAR | 16-bit integer / IEEE-754 float32 | kVAR | R | Yes | Highest reactive-demand value. The source note references point 28. |

## Counters and configuration (points 31-40)

| Int | Name | Data type | Units / range | Access | NV | Notes |
|---:|---|---|---|:---:|:---:|---|
| 31 | Count of kWh resets | 16-bit integer counter | 0-65535 | R | Yes | Cannot be reset; rolls over from 65535 to 0. |
| 32 | Count of peak-demand resets | 16-bit integer counter | 0-65535 | R | Yes | Cannot be reset; rolls over from 65535 to 0. |
| 33 | Count of peak-kVAR resets | 16-bit integer counter | 0-65535 | R | Yes | Cannot be reset; rolls over from 65535 to 0. |
| 34 | Count of elapsed sub-intervals | 16-bit integer counter | count | R | No | Use to distinguish an unchanged demand value from a new interval with steady load. The guide’s note refers to point 28. |
| 35 | Number of readings in present sub-interval | Unsigned 16-bit integer | readings | R | No | Increments every 200 ms (5 Hz); represents readings accumulated into point 25. Overflow behavior is described under operational notes. |
| 36 | Sub-interval length | 16-bit integer | readings at 5 Hz | R/W | Yes | Value is seconds × 5; e.g. `4500` = 15 minutes. Set to `0` for synchronization by communications or demand-reset input. |
| 37 | Number of sub-intervals per demand interval | 16-bit integer | 1-6 | R/W | Yes | Set to `1` for block demand. |
| 38 | System ID | 16-bit integer | ID | R | Yes | `15024` = basic meter; `15025` = enhanced model. |
| 39 | CT size | 16-bit integer | A | R | Yes | Reads the CT size, e.g. 100 or 300. |
| 40 | CT number | 16-bit integer | 1, 2, or 3 | R | Yes | Number of connected CTs. |

## Commands, status, timestamps, and identification (points 41-59)

| Int | Name | Data type / packing | Access | NV | Notes |
|---:|---|---|:---:|:---:|---|
| 41 | Command | 16-bit bit map | R/W | No | Bit 0 (`0x0001`): begin new demand sub-interval; bit 1 (`0x0002`): clear kWh accumulator; bit 2 (`0x0004`): reset peak demand; bit 3 (`0x0008`): reset peak kVAR. Write bits 4-15 as zero. |
| 42 | Phase-loss latching register | 16-bit bit map | R/W | Yes | Bit 0: phase A (unpredictable results on phase A); bit 1: phase B; bit 2: phase C. Write bits 3-15 as zero. User should clear this latching register. |
| 43 | Count of phase losses | 16-bit integer counter | R | Yes | Counts a loss on any phase; cannot be reset; rolls over from 65535 to 0. |
| 44 | Date/time: month and day | LSB: month 1-12; MSB: day 1-31 | R/W | Yes | Current clock. |
| 45 | Date/time: year and hour | LSB: year 0-199; MSB: hour 0-23 | R/W | Yes | Current clock. |
| 46 | Date/time: minutes and seconds | LSB: minute 0-59; MSB: second 0-59 | R/W | Yes | Current clock. |
| 47 | Phase-loss timestamp: month and day | LSB: month 1-12; MSB: day 1-31 | R | Yes | - |
| 48 | Phase-loss timestamp: year and hour | LSB: year 0-199; MSB: hour 0-23 | R | Yes | - |
| 49 | Phase-loss timestamp: minutes and seconds | LSB: minute 0-59; MSB: second 0-59 | R | Yes | - |
| 50 | Last-restart timestamp: month and day | LSB: month 1-12; MSB: day 1-31 | R | Yes | - |
| 51 | Last-restart timestamp: year and hour | LSB: year 0-199; MSB: hour 0-23 | R | Yes | - |
| 52 | Last-restart timestamp: minutes and seconds | LSB: minute 0-59; MSB: second 0-59 | R | Yes | - |
| 53 | Last-kWh-reset timestamp: month and day | LSB: month 1-12; MSB: day 1-31 | R | Yes | Source capitalization: “KWh”. |
| 54 | Last-kWh-reset timestamp: year and hour | LSB: year 0-199; MSB: hour 0-23 | R | Yes | - |
| 55 | Last-kWh-reset timestamp: minutes and seconds | LSB: minute 0-59; MSB: second 0-59 | R | Yes | - |
| 56 | Reset-system firmware version | 16-bit integer | R | Yes | Encoding is not specified in the guide. |
| 57 | Operating-system firmware version | 16-bit integer | R | Yes | Encoding is not specified in the guide. |
| 58 | Serial number, least-significant word | 16-bit integer (LSW) | R | Yes | Combine with point 59 for the full serial number. |
| 59 | Serial number, most-significant word | 16-bit integer (MSW) | R | Yes | Combine with point 58 for the full serial number. |

## Integer scaling

The guide provides equivalent multiplier and divisor tables for integer measured points. Use either:

```text
engineering_value = integer_value × multiplier
engineering_value = integer_value ÷ divisor
```

The values below are transcribed as printed. Float points already represent engineering values and do not require these factors.

### Multiplier table

| Point | Unit/description | 100A | 200A | 300/400A | 800A | 1600A | 2400A |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | kWh | 0.007813 | 0.015625 | 0.03125 | 0.0625 | 0.125 | 0.25 |
| 2 | kWh | 512 | 1024 | 2048 | 4096 | 8192 | 16384 |
| 3 | kW | 0.004 | 0.008 | 0.016 | 0.032 | 0.064 | 0.128 |
| 4 | kVAR | 0.004 | 0.008 | 0.016 | 0.032 | 0.064 | 0.128 |
| 5 | kVA | 0.004 | 0.008 | 0.016 | 0.032 | 0.064 | 0.128 |
| 6 | PF | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 |
| 7 | V_LL | 0.03125 | 0.03125 | 0.03125 | 0.03125 | 0.03125 | 0.03125 |
| 8 | V_LN | 0.015625 | 0.015625 | 0.015625 | 0.015625 | 0.015625 | 0.015625 |
| 9 | Amps | 0.003906 | 0.007813 | 0.015625 | 0.03125 | 0.0625 | 0.125 |
| 10 | kW_a | 0.001 | 0.002 | 0.004 | 0.008 | 0.016 | 0.032 |
| 11 | kW_b | 0.001 | 0.002 | 0.004 | 0.008 | 0.016 | 0.032 |
| 12 | kW_c | 0.001 | 0.002 | 0.004 | 0.008 | 0.016 | 0.032 |
| 13 | PF_a | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 |
| 14 | PF_b | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 |
| 15 | PF_c | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 | 3.05E-05 |
| 16 | V_ab | 0.03125 | 0.03125 | 0.03125 | 0.03125 | 0.03125 | 0.03125 |
| 17 | V_bc | 0.03125 | 0.03125 | 0.03125 | 0.03125 | 0.03125 | 0.03125 |
| 18 | V_ac | 0.03125 | 0.03125 | 0.03125 | 0.03125 | 0.03125 | 0.03125 |
| 19 | V_an | 0.015625 | 0.015625 | 0.015625 | 0.015625 | 0.015625 | 0.015625 |
| 20 | V_bn | 0.015625 | 0.015625 | 0.015625 | 0.015625 | 0.015625 | 0.015625 |
| 21 | V_cn | 0.015625 | 0.015625 | 0.015625 | 0.015625 | 0.015625 | 0.015625 |
| 22 | Amps_a | 0.003906 | 0.003906 | 0.003906 | 0.003906 | 0.003906 | 0.003906 |
| 23 | Amps_b | 0.003906 | 0.003906 | 0.003906 | 0.003906 | 0.003906 | 0.003906 |
| 24 | Amps_c | 0.003906 | 0.003906 | 0.003906 | 0.003906 | 0.003906 | 0.003906 |
| 25 | kWd | 0.004 | 0.008 | 0.016 | 0.032 | 0.064 | 0.128 |
| 26 | kWd | 0.004 | 0.008 | 0.016 | 0.032 | 0.064 | 0.128 |
| 27 | kWd | 0.004 | 0.008 | 0.016 | 0.032 | 0.064 | 0.128 |
| 28 | kVARd | 0.004 | 0.008 | 0.016 | 0.032 | 0.064 | 0.128 |
| 29 | kVARd | 0.004 | 0.008 | 0.016 | 0.032 | 0.064 | 0.128 |
| 30 | kVARd | 0.004 | 0.008 | 0.016 | 0.032 | 0.064 | 0.128 |

### Divisor table

| Point | Unit/description | 100A | 200A | 300/400A | 800A | 1600A | 2400A |
|---:|---|---:|---:|---:|---:|---:|---:|
| 1 | kWh | 128 | 64 | 32 | 16 | 8 | 4 |
| 2 | kWh | 1.953E-3 | 9.765E-4 | 4.8828E-4 | 2.4414E-4 | 1.2207E-4 | 6.1035E-5 |
| 3 | kW | 250 | 125 | 62.5 | 31.25 | 15.625 | 7.8125 |
| 4 | kVAR | 250 | 125 | 62.5 | 31.25 | 15.625 | 7.8125 |
| 5 | kVA | 250 | 125 | 62.5 | 31.25 | 15.625 | 7.8125 |
| 6 | PF | 32768 | 32768 | 32768 | 32768 | 32768 | 32768 |
| 7 | V_LL | 32 | 32 | 32 | 32 | 32 | 32 |
| 8 | V_LN | 64 | 64 | 64 | 64 | 64 | 64 |
| 9 | Amps | 256 | 128 | 64 | 32 | 16 | 8 |
| 10 | kW_a | 1000 | 500 | 250 | 125 | 62.5 | 32.25 |
| 11 | kW_b | 1000 | 500 | 250 | 125 | 62.5 | 32.25 |
| 12 | kW_c | 1000 | 500 | 250 | 125 | 62.5 | 32.25 |
| 13 | PF_a | 32768 | 32768 | 32768 | 32768 | 32768 | 32768 |
| 14 | PF_b | 32768 | 32768 | 32768 | 32768 | 32768 | 32768 |
| 15 | PF_c | 32768 | 32768 | 32768 | 32768 | 32768 | 32768 |
| 16 | V_ab | 32 | 32 | 32 | 32 | 32 | 32 |
| 17 | V_bc | 32 | 32 | 32 | 32 | 32 | 32 |
| 18 | V_ac | 32 | 32 | 32 | 32 | 32 | 32 |
| 19 | V_an | 64 | 64 | 64 | 64 | 64 | 64 |
| 20 | V_bn | 64 | 64 | 64 | 64 | 64 | 64 |
| 21 | V_cn | 64 | 64 | 64 | 64 | 64 | 64 |
| 22 | Amps_a | 256 | 128 | 64 | 32 | 16 | 8 |
| 23 | Amps_b | 256 | 128 | 64 | 32 | 16 | 8 |
| 24 | Amps_c | 256 | 128 | 64 | 32 | 16 | 8 |
| 25 | kWd | 250 | 125 | 62.5 | 31.25 | 15.625 | 7.8125 |
| 26 | kWd | 250 | 125 | 62.5 | 31.25 | 15.625 | 7.8125 |
| 27 | kWd | 250 | 125 | 62.5 | 31.25 | 15.625 | 7.8125 |
| 28 | kVARd | 250 | 125 | 62.5 | 31.25 | 15.625 | 7.8125 |
| 29 | kVARd | 250 | 125 | 62.5 | 31.25 | 15.625 | 7.8125 |
| 30 | kVARd | 250 | 125 | 62.5 | 31.25 | 15.625 | 7.8125 |

> Source-data caution: the guide prints `32.25` as the 2400A divisor for points 10-12, while the corresponding multiplier is `0.032` (whose reciprocal is `31.25`). The value above is intentionally preserved exactly as printed.

## Model applicability

The source says that a listed model suffix restricts a point to those models. An unavailable point reads `0xFFFF` in integer form and NaN in float form. The guide labels the variants only as `-1`, `-2`, and `-3` in the point map; this document does not expand those suffixes into full catalog numbers.

## Operational notes

### Floating-point and block reads

- Float values use the 32-bit IEEE real format.
- All float points are read-only. Write read/write values through their integer points.
- A Modbus block read may request at most 125 registers: 125 × 2 data bytes + 5 bytes overhead = 255 bytes.

### Demand calculation

- The meter samples kW and kVAR every 200 ms (5 Hz).
- Present sub-interval demand is the accumulated value divided by the number of samples and appears at points 25 (kW) and 28 (kVAR).
- A sub-interval ends when command-point bit 0 is written, when the hardware interval-reset signal is detected, or when the configured non-zero sub-interval length at point 36 is reached.
- The maximum legal sub-interval length is 65,535 readings (3 h 38 min 27.2 s). At overflow, the board ends the interval and starts the next one on the following reading. The guide expects normal intervals not to exceed one hour.
- Completed sub-interval averages enter a six-value FIFO. Point 37 selects how many of the newest values (1-6) are averaged for present demand. Point 34 increments, and a new maximum updates the peak value.

### Reset behavior

- Setting command-point bit 1 clears the kWh accumulator. Writes directly to the kWh points are ignored.
- Reset counters at points 31-33 and the phase-loss counter at point 43 cannot themselves be cleared.

## Verification notes

- Register-map pages 7-9 were checked row-by-row: integer points 1 through 59 are present with no gaps.
- Float address pairs were checked for points 1 through 30: 257/258 through 315/316, increasing by two addresses per point.
- Access and non-volatile flags were checked against the source columns.
- Both complete 30-row scaling tables on pages 10 and 11 were transcribed.
- Notes governing integer/float formats, model-specific unavailable values, block-read limits, demand computation, and reset behavior were checked against page 12.
- Apparent source inconsistencies or typographical errors were preserved or explicitly flagged rather than silently corrected.

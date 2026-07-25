# Veris 8100 ESPHome

ESPHome Modbus integration, validated register map, and Home Assistant configuration for Veris 8100 Series Energy Meters.

---

## Supported Hardware

### Veris H8167 Energy Meter

- H8167-xxxx-xx Series Energy Meter

### Veris H8163-CB Modbus Communications Board

#### Address DIP Switch

> _Documentation coming soon._

#### Communication Settings DIP Switch

> _Documentation coming soon._

#### Wiring

##### Power Tap

> _Documentation coming soon._

##### RS-485 Terminal Block

> _Documentation coming soon._

---

## Home Assistant

### Exposed Entities

The following sensor entities are exposed to Home Assistant.

### Energy

| Entity | Units | Description |
|---------|:-----:|-------------|
| Total Energy | kWh | Total accumulated real energy consumption |
| Total Real Power | kW | Total real (active) power |
| Total Reactive Power | kVAR | Total reactive power |
| Total Apparent Power | kVA | Total apparent power |
| Total Power Factor | — | Overall system power factor |

### Average Measurements

| Entity | Units | Description |
|---------|:-----:|-------------|
| Average Line Voltage | V | Average line-to-line voltage |
| Average Phase Voltage | V | Average line-to-neutral voltage |
| Average Current | A | Average current across all phases |

### Phase Voltages

| Entity | Units | Description |
|---------|:-----:|-------------|
| Phase A Voltage | V | L1 to Neutral |
| Phase B Voltage | V | L2 to Neutral |
| Phase C Voltage | V | L3 to Neutral |
| Phase A-B Voltage | V | L1 to L2 |
| Phase B-C Voltage | V | L2 to L3 |
| Phase A-C Voltage | V | L1 to L3 |

### Phase Currents

| Entity | Units | Description |
|---------|:-----:|-------------|
| Phase A Current | A | Current on Phase A (L1) |
| Phase B Current | A | Current on Phase B (L2) |
| Phase C Current | A | Current on Phase C (L3) |

### Phase Real Power

| Entity | Units | Description |
|---------|:-----:|-------------|
| Phase A Real Power | kW | Real power on Phase A |
| Phase B Real Power | kW | Real power on Phase B |
| Phase C Real Power | kW | Real power on Phase C |

### Phase Power Factor

| Entity | Units | Description |
|---------|:-----:|-------------|
| Phase A Power Factor | — | Power factor for Phase A |
| Phase B Power Factor | — | Power factor for Phase B |
| Phase C Power Factor | — | Power factor for Phase C |

### Demand

| Entity | Units | Description |
|---------|:-----:|-------------|
| Present Demand Sub-Interval | kW | Current sub-interval demand |
| Present Demand | kW | Current demand |
| Peak Demand | kW | Peak demand since last reset |
| Present Reactive Demand | kVAR | Current reactive demand |
| Peak Reactive Demand | kVAR | Peak reactive demand |

---

## Notes

- Supports both **single-phase/split-phase** and **three-phase** installations.
- On split-phase systems, **Phase C** entities will typically report zero or remain unused.
- Entity names use standard electrical terminology rather than vendor-specific names.
- Measurements are read directly from the Veris 8100 Series meter over **Modbus RTU (RS-485)**.

---

## ESPHome Configuration

The reference ESPHome configuration is located at:

```text
/src/esphome_esp32c3plus.yaml
```

---

## Project Roadmap

- [ ] Complete register validation
- [ ] Wiring guide with photos
- [ ] Power tap installation
- [ ] 3D printed mounting bracket
- [ ] Home Assistant Energy Dashboard configuration
- [ ] ESPHome package support
- [ ] Hardware BOM
- [ ] Installation guide
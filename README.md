<img src="images/logo.png" alt="NMT C Modbus Logo" width="120" align="left" style="margin-right:16px;"/>

### IMP NMT C Series
**Home Assistant Modbus TCP**

<br clear="left"/>

**YAML package to integrate IMP Pumps NMT C series circulation pumps into Home Assistant via Modbus TCP (NMTC module).**

<a href="README.de.md">Deutsche Version</a>

---

## Compatible Pumps

This package works with all IMP Pumps models equipped with the **NMTC module** (art. 7340055):

- NMT Smart C
- NMT Max C
- NMT Lan C
- NMT Max II C
- NMT Smart II C

The NMTC module provides the Modbus TCP/RTU interface. The Modbus register map is identical across all listed models.

## Features

- **10 sensors**: Head, flow, speed, power consumption, frequency, efficiency, actual setpoint, three temperatures (circuit, motor, liquid)
- **Status bits**: 4 binary sensors decoded from the status register (pump rotating, remote mode, error, fault active)
- **Control mode**: Two text sensors showing the current control mode in plain text (standard + alternative enumeration)
- **Error codes**: 3 error code sensors with human-readable text descriptions (20 known codes from the NMTC manual)
- **Computed values**: Flow in L/h (converted from native m³/h), error code summary
- **Dashboard card**: Ready-to-use Lovelace card with 6 gauges

## Entity Quality

All sensors are defined with correct and complete HA metadata: `unique_id`, `device_class`, `state_class`, `unit_of_measurement`, `scale`, `precision` and `input_type` are carefully set for each entity. This means long-term statistics, energy dashboard integration and history graphs work out of the box without manual configuration. All template sensors include `availability` templates to correctly show `unavailable` instead of misleading default values when the Modbus connection is lost.

## Requirements

- Home Assistant (any current version)
- IMP Pumps circulation pump with **NMTC module** (see compatible pumps above)
- Network connection between HA and the NMTC module (Ethernet)
- Default Modbus slave address: **245**

## Installation

1. Copy `imp_nmt_c.yaml` to `/config/packages/`
2. Ensure packages are enabled in `configuration.yaml`:
   ```yaml
   homeassistant:
     packages: !include_dir_named packages
   ```
3. Adjust the NMTC module IP address in the YAML:
   ```yaml
   host: 192.168.2.17  # ← CHANGE: IP of your NMTC module
   ```
4. Restart Home Assistant

> **German version:** All entity names, template texts and comments in German: `imp_nmt_c.de.yaml` and `dashboard_card.de.yaml`.

## Dashboard Card (optional)

<p align="center">
  <img src="images/dashboard_screenshot.png" alt="NMT Pump Dashboard"/>
</p>

The file `dashboard_card.yaml` contains a ready-to-use Lovelace card with gauges for head, power, speed, flow, setpoint and liquid temperature.

**Usage:** Paste the contents of `dashboard_card.yaml` as a manual card (YAML) in the dashboard editor.

### Required HACS Cards

| HACS Card | Purpose | HACS Search |
|---|---|---|
| [**Vertical Stack In Card**](https://github.com/ofekashery/vertical-stack-in-card) | Outer container without borders | `vertical-stack-in-card` |
| [**card-mod**](https://github.com/thomasloven/lovelace-card-mod) | CSS styling (remove borders, colors) | `card-mod` |

Without these cards the dashboard card will not render correctly. The Modbus YAML itself works independently.

## Register Overview

### Measurement Values (Read-Only, Register Block 301)

| Register | Sensor | Unit |
|---|---|---|
| 301 | Head | m |
| 302 | Flow | m³/h |
| 303 | Efficiency | % |
| 304 | Speed | rpm |
| 305 | Frequency | Hz |
| 308 | Actual Setpoint | % |
| 312/313 | Power (HI/LO) | W |
| 318 | Circuit Temperature | °C |
| 319 | Motor Temperature | °C |
| 322 | Liquid Temperature | °C |

### Status Registers (Read-Only, Register Block 201)

| Register | Sensor | Description |
|---|---|---|
| 201 | StatusReg | Bitfield (rotation, remote, error, near max/min speed) |
| 203 | ControlMode (Alt) | Alternative control mode enumeration |
| 205-207 | ErrorCode 1-3 | Error codes (0 = no error) |
| 208 | ControlMode | Current control mode (0..3) |

### Optional Registers (not available on all models)

| Register | Sensor | Unit |
|---|---|---|
| 327/328 | Operation Time | h |
| 329/330 | Total Powered Time | h |
| 332/333 | Total Energy | kWh |

### Control Registers (Read-Write) — not implemented

Register 101 (ControlReg), 104 (SetPoint) and 108 (ControlMode) exist but are intentionally not implemented. See the YAML comments for details.

## Entity Reference

See [entities.en.md](entities.en.md) for a complete mapping of registers to entity names, or [entities.de.md](entities.de.md) for the German version.

## Documentation

- [NMTC module manual v37 (PDF)](https://imp-pumps.com/wp-content/uploads/2020/03/NMTC_manual_v37.pdf) — official IMP Pumps documentation including Modbus register definitions (chapter 8)

## License

[MIT](LICENSE)

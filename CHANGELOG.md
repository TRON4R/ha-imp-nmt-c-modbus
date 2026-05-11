# Changelog

## v1.1.0 (2026-05-11)

- New automation `nmt_alarm_notification`: creates an HA notification when a fault becomes active.
  Trigger: aggregated fault status → 'on'. Message includes the active error codes in plain text.
- Header modernized: version stamp, repo and changelog links added.
- Explicit `scan_interval` values (previously HA default): measurements 30 s, temperatures 60 s,
  status/error code registers 30 s. Reduces Modbus bus traffic and is self-documenting.

## v1.0.0 (2026-04-09)

Initial release.

- 10 Modbus sensors (head, flow, efficiency, speed, frequency, setpoint, power, 3 temperatures)
- 6 status sensors (status register, alt control mode, 3 error codes, control mode)
- 4 template binary sensors (rotating, remote active, error status, fault active)
- 7 template sensors (2 control mode text, 3 error code text, error summary, flow L/h)
- 3 optional registers commented out (operation time, powered time, energy — not available on all models)
- Ready-to-use dashboard card with 6 gauges
- Bilingual: English (default) and German (.de.yaml)
- Entity reference tables (entities.en.md / entities.de.md)

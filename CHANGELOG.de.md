# Changelog

## v1.1.0 (2026-05-11)

- Neue Automation `nmt_alarm_notification`: Erzeugt HA-Notification bei aktivem Fehler.
  Trigger: aggregierter Störungsstatus → 'on'. Message enthält die aktiven Fehlercodes als Klartext.
- Header modernisiert: Version-Stamp, Repo- und Changelog-Link ergänzt.
- `scan_interval` explizit gesetzt (vorher HA-Default): Messwerte 30 s, Temperaturen 60 s,
  Status-/Fehlercode-Register 30 s. Reduziert Modbus-Bus-Traffic und ist selbst-dokumentierend.

## v1.0.0 (2026-04-09)

Erstveröffentlichung.

- 10 Modbus-Sensoren (Förderhöhe, Durchfluss, Effizienz, Drehzahl, Frequenz, Sollwert, Leistung, 3 Temperaturen)
- 6 Status-Sensoren (Statusregister, Alt. Betriebsmodus, 3 Fehlercodes, Betriebsmodus)
- 4 Template-Binärsensoren (rotiert, Fernsteuerung aktiv, Fehlerstatus, Störung aktiv)
- 7 Template-Sensoren (2 Betriebsmodus-Text, 3 Fehlercode-Text, Fehler-Zusammenfassung, Durchfluss L/h)
- 3 optionale Register auskommentiert (Betriebszeit, Einschaltzeit, Energie — nicht auf allen Modellen verfügbar)
- Fertige Dashboard-Karte mit 6 Gauge-Anzeigen
- Zweisprachig: Englisch (Standard) und Deutsch (.de.yaml)
- Entity-Referenztabellen (entities.en.md / entities.de.md)

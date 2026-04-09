# Entity-Referenz (Deutsch)

## Modbus-Sensoren

| Register | Handbuch-Name | Entity-Name | Einheit | Device Class |
|---|---|---|---|---|
| 301 | Head | NMT Pumpe Förderhöhe | m | distance |
| 302 | Flow | NMT Pumpe Durchfluss | m³/h | volume_flow_rate |
| 303 | Efficiency | NMT Pumpe Effizienz | % | — |
| 304 | Speed | NMT Pumpe Drehzahl | rpm | — |
| 305 | Frequency | NMT Pumpe Frequenz | Hz | frequency |
| 308 | ActualSetPoint | NMT Pumpe tats. Sollwert | % | — |
| 312/313 | PowerHI/LO | NMT Pumpe Stromverbrauch | W | power |
| 318 | CircuitTemp | NMT Pumpe Temperatur Elektronik | °C | temperature |
| 319 | MotorTemp | NMT Pumpe Temperatur Motor | °C | temperature |
| 322 | LiquidTemp | NMT Pumpe Temperatur Wasser | °C | temperature |

## Modbus-Status-Sensoren

| Register | Handbuch-Name | Entity-Name | Hinweise |
|---|---|---|---|
| 201 | StatusReg | NMT Pumpe Status Register Raw | Bitfeld, Dekodierung unten |
| 203 | ControlMode (Alt) | NMT Pumpe Alt. Betriebsmodus (Status) | Enum (0..6, 128) |
| 205 | ErrorCode1 | NMT Pumpe Fehlercode 1 | 0 = kein Fehler |
| 206 | ErrorCode2 | NMT Pumpe Fehlercode 2 | 0 = kein Fehler |
| 207 | ErrorCode3 | NMT Pumpe Fehlercode 3 | 0 = kein Fehler |
| 208 | ControlMode | NMT Pumpe Betriebsmodus (Status) | Enum (0..3) |

## Template-Binärsensoren (dekodiert aus StatusReg 201)

| Bit | Handbuch-Name | Entity-Name | Device Class |
|---|---|---|---|
| 6 | Rotation | NMT Pumpe rotiert | — |
| 8 | AccessMode | NMT Pumpe ModBus Fernsteuerung Aktiv | — |
| 10 | Error | NMT Pumpe Fehler Status | problem |
| — | (aggregiert) | NMT Pumpe aggregierter Störungsstatus | problem |

## Template-Sensoren

| Entity-Name | Quelle | Beschreibung |
|---|---|---|
| NMT Pumpe Alt. Betriebsmodus (Text) | Reg 203 | Betriebsmodus als Text (Alt. Enumeration) |
| NMT Pumpe Betriebsmodus (Text) | Reg 208 | Betriebsmodus als Text |
| NMT Pumpe Fehlercode 1 (Text) | Reg 205 | Fehlercode 1 mit Beschreibung |
| NMT Pumpe Fehlercode 2 (Text) | Reg 206 | Fehlercode 2 mit Beschreibung |
| NMT Pumpe Fehlercode 3 (Text) | Reg 207 | Fehlercode 3 mit Beschreibung |
| NMT Pumpe Fehler (Zusammenfassung) | Reg 205-207 | Aktive Fehlercodes (kommagetrennt) |
| NMT Pumpe Durchfluss L/h | Reg 302 | Durchfluss umgerechnet von m³/h in L/h |

## Optionale Register (nicht auf allen Modellen verfügbar)

| Register | Handbuch-Name | Entity-Name | Einheit |
|---|---|---|---|
| 327/328 | OperationTimeHI/LO | NMT Pumpe Betriebszeit | h |
| 329/330 | TotalPoweredTimeHI/LO | NMT Pumpe Einschaltzeit Modul | h |
| 332/333 | EnergyHI/LO | NMT Pumpe Energieverbrauch Gesamt | kWh |

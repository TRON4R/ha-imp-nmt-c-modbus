# Entity Reference (English)

## Modbus Sensors

| Register | Manual Name | Entity Name | Unit | Device Class |
|---|---|---|---|---|
| 301 | Head | NMT Pump Head | m | distance |
| 302 | Flow | NMT Pump Flow | m³/h | volume_flow_rate |
| 303 | Efficiency | NMT Pump Efficiency | % | — |
| 304 | Speed | NMT Pump Speed | rpm | — |
| 305 | Frequency | NMT Pump Frequency | Hz | frequency |
| 308 | ActualSetPoint | NMT Pump Actual Setpoint | % | — |
| 312/313 | PowerHI/LO | NMT Pump Power Consumption | W | power |
| 318 | CircuitTemp | NMT Pump Circuit Temperature | °C | temperature |
| 319 | MotorTemp | NMT Pump Motor Temperature | °C | temperature |
| 322 | LiquidTemp | NMT Pump Liquid Temperature | °C | temperature |

## Modbus Status Sensors

| Register | Manual Name | Entity Name | Notes |
|---|---|---|---|
| 201 | StatusReg | NMT Pump Status Register (Raw) | Bitfield, decoded below |
| 203 | ControlMode (Alt) | NMT Pump Alt Control Mode (Status) | Enum (0..6, 128) |
| 205 | ErrorCode1 | NMT Pump Error Code 1 | 0 = no error |
| 206 | ErrorCode2 | NMT Pump Error Code 2 | 0 = no error |
| 207 | ErrorCode3 | NMT Pump Error Code 3 | 0 = no error |
| 208 | ControlMode | NMT Pump Control Mode (Status) | Enum (0..3) |

## Template Binary Sensors (decoded from StatusReg 201)

| Bit | Manual Name | Entity Name | Device Class |
|---|---|---|---|
| 6 | Rotation | NMT Pump Rotating | — |
| 8 | AccessMode | NMT Pump Modbus Remote Active | — |
| 10 | Error | NMT Pump Error Status | problem |
| — | (aggregate) | NMT Pump Fault Active | problem |

## Template Sensors

| Entity Name | Source | Description |
|---|---|---|
| NMT Pump Alt Control Mode (Text) | Reg 203 | Control mode as text (Alt Enumeration) |
| NMT Pump Control Mode (Text) | Reg 208 | Control mode as text |
| NMT Pump Error Code 1 (Text) | Reg 205 | Error code 1 with description |
| NMT Pump Error Code 2 (Text) | Reg 206 | Error code 2 with description |
| NMT Pump Error Code 3 (Text) | Reg 207 | Error code 3 with description |
| NMT Pump Error Summary | Reg 205-207 | Active error codes (comma-separated) |
| NMT Pump Flow L/h | Reg 302 | Flow converted from m³/h to L/h |

## Optional Registers (not available on all models)

| Register | Manual Name | Entity Name | Unit |
|---|---|---|---|
| 327/328 | OperationTimeHI/LO | NMT Pump Operation Time | h |
| 329/330 | TotalPoweredTimeHI/LO | NMT Pump Total Powered Time | h |
| 332/333 | EnergyHI/LO | NMT Pump Total Energy | kWh |

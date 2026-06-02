# Register Mapping

The bridge fills the main SDM630 input registers used by the Solis inverter for grid metering.

All floats are written as two Modbus input registers in SDM630 byte/word order.

| Start register | Value |
| --- | --- |
| 0 | L1 voltage |
| 2 | L2 voltage |
| 4 | L3 voltage |
| 6 | L1 current |
| 8 | L2 current |
| 10 | L3 current |
| 12 | L1 active power |
| 14 | L2 active power |
| 16 | L3 active power |
| 18 | L1 apparent power |
| 20 | L2 apparent power |
| 22 | L3 apparent power |
| 30 | L1 power factor |
| 32 | L2 power factor |
| 34 | L3 power factor |
| 48 | Total current |
| 52 | Total active power |
| 56 | Total apparent power |
| 70 | Frequency |
| 342 | Total energy |

The current YAML uses Shelly RPC fields such as `a_act_power`, `b_act_power`, `c_act_power`, `total_act_power`, `a_voltage`, `a_current` and `total_act`.


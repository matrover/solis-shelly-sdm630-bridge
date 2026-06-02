# Registermapping

De bridge vult de belangrijkste SDM630 input registers die de Solis gebruikt voor netmeting.

Alle floats worden als twee Modbus input registers geschreven in SDM630 byte/word volgorde.

| Startregister | Waarde |
| --- | --- |
| 0 | L1 spanning |
| 2 | L2 spanning |
| 4 | L3 spanning |
| 6 | L1 stroom |
| 8 | L2 stroom |
| 10 | L3 stroom |
| 12 | L1 actief vermogen |
| 14 | L2 actief vermogen |
| 16 | L3 actief vermogen |
| 18 | L1 schijnbaar vermogen |
| 20 | L2 schijnbaar vermogen |
| 22 | L3 schijnbaar vermogen |
| 30 | L1 power factor |
| 32 | L2 power factor |
| 34 | L3 power factor |
| 48 | Totaal stroom |
| 52 | Totaal actief vermogen |
| 56 | Totaal schijnbaar vermogen |
| 70 | Frequentie |
| 342 | Totaal energie |

De huidige YAML gebruikt Shelly RPC velden zoals `a_act_power`, `b_act_power`, `c_act_power`, `total_act_power`, `a_voltage`, `a_current` en `total_act`.


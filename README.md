# Solis Shelly SDM630 Bridge

Gebruik een Shelly Pro 3EM als netmeter voor een Solis S6 omvormer die normaal een Eastron SDM630MCT via Modbus RTU verwacht.

De bridge draait op een KinCony ESP32-S3 Core Board. De ESP leest de Shelly via HTTP/RPC en gedraagt zich richting de Solis als een Eastron/SDM630 Modbus RTU slave op RS485.

![Systeemoverzicht](assets/system-overview.svg)

## Status

Getest met:

- Solis S6 omvormer met meterpoort voor Eastron/SDM630
- Shelly Pro 3EM / EM3 met RPC endpoints
- KinCony ESP32-S3 Core Board met onboard W5500 Ethernet en RS485
- ESPHome 2026.4.x

## Wat je nodig hebt

- KinCony ESP32-S3 Core Board
- 12 V voeding voor de KinCony
- Shelly Pro 3EM of compatibele Shelly Gen2/Gen3 energiemeter
- Netwerkkabel voor Ethernet
- RJ45-stekker of kabel naar de Solis meterpoort
- ESPHome Device Builder

## Aansluiten

Gebruik de onboard RS485 van de KinCony naar de Solis meterpoort.

![Aansluitschema](assets/wiring-kincony-solis.svg)

| KinCony onboard RS485 | Solis meter RJ45 | Functie |
| --- | --- | --- |
| 485A | Pin 1 | RS485 A |
| 485B | Pin 2 | RS485 B |
| GND | Alleen indien beschikbaar | Referentie, meestal niet nodig |

Als de Solis geen meter ziet: wissel A en B om. RS485-labels zijn helaas niet overal consequent.

## Snelle installatie

1. Reserveer via DHCP een vast IP voor de Shelly en eventueel voor de KinCony.
2. Kopieer `esphome/solis-sdm630-bridge.yaml` naar ESPHome.
3. Pas bovenin de YAML `shelly_host` aan naar het IP of hostname van jouw Shelly.
4. Flash de KinCony de eerste keer via USB.
5. Verbind KinCony RS485 met de Solis meterpoort.
6. Stel op de Solis de meter in als Eastron/SDM630, Modbus adres `1`, `9600 8N1`.
7. Controleer in ESPHome logs of de Shelly-data elke seconde binnenkomt.
8. Controleer op de Solis of meter/grid waarden zichtbaar zijn.

Meer detail staat in [docs/installatie.md](docs/installatie.md).

## ESPHome configuratie

De complete voorbeeldconfig staat hier:

- [esphome/solis-sdm630-bridge.yaml](esphome/solis-sdm630-bridge.yaml)

Belangrijke instellingen:

- Modbus slave adres: `1`
- Baudrate: `9600`
- UART: `GPIO16` TX en `GPIO15` RX voor de onboard RS485 van de KinCony
- DHCP: er staat geen static IP in de YAML
- Shelly polling: elke seconde via `/rpc/EM.GetStatus?id=0`

## Veiligheid

Werk niet aan bekabeling terwijl de omvormer of meterkast onder spanning staat. RS485 is laagspanning, maar de meter/CT-installatie zit in de buurt van netspanning. Laat de netspanningskant door een bevoegd persoon controleren.

## Documentatie

- [Installatiehandleiding](docs/installatie.md)
- [Troubleshooting](docs/troubleshooting.md)
- [Registermapping](docs/registermapping.md)
- [RJ45 pinout](assets/rj45-meter-pinout.svg)

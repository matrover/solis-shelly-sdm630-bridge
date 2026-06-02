# Troubleshooting

## ESPHome ziet de Shelly niet

Controleer:

- `shelly_host` in de YAML
- Shelly en KinCony zitten in hetzelfde routable netwerk
- De Shelly RPC URL werkt in een browser
- Geen firewall tussen ESP en Shelly

## OTA upload lukt niet via `.local`

Gebruik DHCP-reservations. Als mDNS faalt, voeg tijdelijk toe onder `ethernet`:

```yaml
  use_address: KINCONY_DHCP_IP
```

Gebruik hier het DHCP-adres van de KinCony. Dit is geen static IP-configuratie voor het device; ESPHome gebruikt het alleen om OTA/logs te vinden.

## Solis ziet geen meter

Controleer:

- Solis staat op Eastron/SDM630 meter
- Modbus adres is `1`
- Baudrate is `9600`
- KinCony 485A naar Solis RJ45 pin 1
- KinCony 485B naar Solis RJ45 pin 2
- Wissel A/B als er geen meter wordt gevonden

## Waarden hebben de verkeerde richting

Als import/export omgekeerd lijkt:

- Controleer de richting van de Shelly CT-klemmen
- Controleer de fasevolgorde
- Controleer in de Shelly app of vermogen positief/negatief logisch is

Pas de ESPHome-code pas aan nadat de Shelly zelf logisch meet.

## Home Assistant of SolisCloud loopt achter

De ESP leest de Shelly elke seconde. SolisCloud/Home Assistant integraties kunnen veel trager verversen. Gebruik voor live controle:

- ESPHome logs
- Solis display
- Webserver van de KinCony

## ESPHome logs via dashboard

Kies bij logs voor OTA/wireless. Bij API-gebruik moet ESPHome de configuratie en target `OTA` gebruiken.

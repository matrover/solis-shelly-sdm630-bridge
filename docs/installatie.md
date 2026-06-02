# Installatiehandleiding

Deze handleiding beschrijft de bewezen route: Shelly naar ESPHome via Ethernet, daarna ESPHome naar Solis via RS485.

## 1. Netwerk voorbereiden

Gebruik DHCP. Maak in je router DHCP-reservations voor:

- Shelly energiemeter
- KinCony ESP32-S3 Core Board

De ESPHome YAML bevat bewust geen static IP. Als mDNS later lastig doet bij OTA, kun je tijdelijk `use_address` gebruiken met het gereserveerde DHCP-adres.

## 2. Shelly controleren

Controleer in een browser of de Shelly RPC endpoints reageren:

```text
http://SHELLY_IP_OR_HOSTNAME/rpc/EM.GetStatus?id=0
http://SHELLY_IP_OR_HOSTNAME/rpc/EMData.GetStatus?id=0
```

De eerste moet velden bevatten zoals `a_act_power`, `b_act_power`, `c_act_power`, `total_act_power`, spanning en stroom.

## 3. ESPHome YAML plaatsen

Kopieer:

```text
esphome/solis-sdm630-bridge.yaml
```

naar ESPHome en wijzig bovenin:

```yaml
substitutions:
  shelly_host: shelly-pro-3em.local
```

naar het IP of hostname van jouw Shelly.

## 4. Flashen

Flash de KinCony de eerste keer via USB. Daarna kan OTA via Ethernet.

Controleer na het flashen:

- ESPHome API is online
- Webserver werkt op `http://KINCONY_DHCP_IP/`
- `Shelly EM Online` staat aan
- Shelly fasevermogens bewegen elke seconde

## 5. RS485 aansluiten

![Aansluitschema](../assets/wiring-kincony-solis.svg)

| KinCony | Solis RJ45 meterpoort |
| --- | --- |
| 485A | Pin 1 |
| 485B | Pin 2 |

Gebruik bij voorkeur een korte twisted pair kabel. GND is meestal niet nodig, maar kan worden aangesloten als beide apparaten daarvoor een laagspanningsreferentie aanbieden.

## 6. Solis instellen

Gebruik op de Solis de meterinstellingen die horen bij een Eastron SDM630/SDM630MCT:

- Meter type: Eastron / SDM630
- Protocol: Modbus RTU
- Adres: `1`
- Baudrate: `9600`
- Data: `8N1`

De exacte menunamen verschillen per Solis firmware.

## 7. Verificatie

In ESPHome logs moet je elke seconde vergelijkbare regels zien:

```text
Shelly Phase A Power
Shelly Phase B Power
Shelly Phase C Power
Shelly Total Active Power
```

Op de Solis moet je live meter/grid waarden zien. In Home Assistant of SolisCloud kunnen die waarden vertraagd of periodiek worden ververst; het Solis-scherm is de snelste controle.

# Troubleshooting

## ESPHome Cannot Reach the Shelly

Check:

- `shelly_host` in the YAML
- Shelly and KinCony are in the same routable network
- The Shelly RPC URL works in a browser
- No firewall blocks traffic between ESP and Shelly

## OTA Upload Does Not Work Through `.local`

Use DHCP reservations. If mDNS fails, temporarily add this under `ethernet`:

```yaml
  use_address: KINCONY_DHCP_IP
```

Use the DHCP address of the KinCony. This is not a static IP configuration for the device; ESPHome only uses it to find the device for OTA and logs.

## Solis Does Not Detect a Meter

Check:

- Solis is configured for an Eastron/SDM630 meter
- Modbus address is `1`
- Baudrate is `9600`
- KinCony 485A goes to Solis RJ45 pin 1
- KinCony 485B goes to Solis RJ45 pin 2
- If using the original Solis meter cable, verify which wires go to RJ45 pin 1 and pin 2
- Swap A/B if no meter is detected

## Values Have the Wrong Direction

If import/export appears reversed:

- Check the direction of the Shelly CT clamps
- Check phase order
- Check in the Shelly app whether positive/negative power makes sense

Only change the ESPHome code after the Shelly itself measures logically.

## Home Assistant or SolisCloud Lags Behind

The ESP reads the Shelly every second. SolisCloud/Home Assistant integrations may refresh much more slowly. For live checks, use:

- ESPHome logs
- Solis display
- KinCony web server

## ESPHome Logs Through the Dashboard

Choose OTA/wireless when opening logs. When using the ESPHome API directly, the log request must include the configuration and target `OTA`.

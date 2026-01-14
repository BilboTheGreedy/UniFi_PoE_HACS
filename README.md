# UniFi PoE Control for Home Assistant

[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://github.com/hacs/integration)

Control PoE ports on UniFi devices (Cloud Gateway Fiber, UDM, switches) from Home Assistant.

## Features

- **Restart PoE Button** - Power cycle a PoE port (~2 second cycle)
- **PoE Toggle Switch** - Enable/disable PoE on a port
- **Auto-discovery** - Finds all PoE-capable ports on your network
- **Multiple devices** - Supports UDM, Cloud Gateway Fiber, and UniFi switches

## Installation

### HACS (Recommended)

1. Open HACS in Home Assistant
2. Click the 3-dot menu → **Custom repositories**
3. Add: `https://github.com/BilboTheGreedy/UniFi_PoE_HACS`
4. Category: **Integration**
5. Click **Add**
6. Search for "UniFi PoE Control" and install
7. Restart Home Assistant

### Manual

Copy `custom_components/unifi_poe` to your Home Assistant `config/custom_components/` directory.

## Configuration

1. Go to **Settings → Devices & Services → Add Integration**
2. Search for "**UniFi PoE Control**"
3. Enter your UniFi controller details:
   - **Host**: Controller IP (e.g., `10.1.10.1`)
   - **API Key**: Create in UniFi Console → Settings → Admins & Users → API Keys
   - **Port**: `443` (default)
   - **Site**: `default` (default)
4. Select the PoE port you want to control

## Entities

After setup, you'll have:

| Entity | Type | Description |
|--------|------|-------------|
| `button.<port_name>_restart_poe` | Button | Power cycles the PoE port |
| `switch.<port_name>_poe_enabled` | Switch | Toggle PoE on/off |

## Use Cases

- Restart a PoE-powered device (like a cellular modem/FWA) when connectivity issues are detected
- Automate power cycling of PoE devices on a schedule
- Integrate with other Home Assistant automations

## Example Automation

```yaml
automation:
  - alias: "Restart Telia FWA on connection loss"
    trigger:
      - platform: state
        entity_id: binary_sensor.internet_connection
        to: "off"
        for:
          minutes: 5
    action:
      - service: button.press
        target:
          entity_id: button.telia_restart_poe
```

## License

MIT License

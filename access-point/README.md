# Access Point Configuration

## TP-Link EAP720

SecureNet uses the TP-Link EAP720 WiFi 7 access point in **Stand Alone Mode** (no cloud dependency).

### Why No Configuration File?

The EAP720 configuration backup is encrypted and contains sensitive credentials:

- Admin login credentials
- SSID passwords for all networks
- Management interface settings

Publishing this file would provide no verification value while exposing customer-specific secrets.

### Configuration Overview

The access point is configured with 6 SSIDs mapped to VLANs:

| SSID | VLAN | Network | Purpose |
|------|------|---------|---------|
| Home-Admin | Native (untagged) | 192.168.1.0/24 | Primary trusted devices |
| Home-IoT | 20 | 192.168.20.0/24 | Cameras, sensors, smart plugs |
| Home-Smart | 30 | 192.168.30.0/24 | TVs, speakers, media devices |
| Home-Guest | 40 | 192.168.40.0/24 | Visitor WiFi |
| Home-Kids | 50 | 192.168.50.0/24 | Children's devices |
| Home-SafeNet | 60 | 10.60.60.0/24 | VPN-tunneled traffic |

### Security Settings

- WPA2/WPA3 mixed mode
- 802.1Q VLAN tagging on trunk port
- Rogue AP detection enabled
- Management interface accessible only from LAN1

### Complete Documentation

For full access point configuration details, see the [AI Whitepaper](https://github.com/opensourcesecurity-inc/aiw) Part 15: Access Point Configuration.

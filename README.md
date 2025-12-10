# SecureNet OS

**Professionally configured OPNsense for home network security.**

[![OPNsense Version](https://img.shields.io/badge/OPNsense-25.7-blue)](https://opnsense.org/)
[![License](https://img.shields.io/badge/License-BSD%202--Clause-orange)](LICENSE)
[![Download Config](https://img.shields.io/github/v/release/opensourcesecurity-inc/securenet?label=Download&color=ff6b35)](https://github.com/opensourcesecurity-inc/securenet/releases/latest)

---

## What Is SecureNet?

SecureNet is OPNsense—a proven, open-source firewall trusted by millions—professionally configured for home network security. This repository contains the complete configuration files used in SecureNet deployments.

**You can verify every claim. You can replicate every configuration.**

---

## Security Stack

| Layer | Protection | Count |
|-------|------------|-------|
| IDS/IPS | Suricata threat signatures | 165,340 |
| DNS Filtering | Blocked malicious domains | 834,427 |
| IP Blocking | Malicious IP addresses | 45,577 |
| Network Isolation | Separate VLANs | 8 |

---

## Network Architecture

SecureNet implements 8 isolated networks:

| Network | Subnet | Purpose |
|---------|--------|---------|
| LAN1 (Admin) | 192.168.1.0/24 | Primary trusted devices |
| LAN2 (Backup) | 192.168.2.0/24 | Hardware failover |
| IoT VLAN | 192.168.20.0/24 | Cameras, sensors, doorbells |
| Smart VLAN | 192.168.30.0/24 | TVs, speakers, appliances |
| Guest VLAN | 192.168.40.0/24 | Visitor WiFi |
| Kids VLAN | 192.168.50.0/24 | Filtered family devices |
| SafeNet VLAN | 10.60.60.0/24 | VPN tunnel (WiFi) |
| SafeNet Port | 10.70.70.0/24 | VPN tunnel (wired) |

---

## Repository Structure

```
securenet/
├── README.md
├── LICENSE
├── opnsense/
│   ├── config.xml              # Main OPNsense configuration (sanitized)
│   ├── firewall/
│   │   ├── rules.md            # Firewall rule documentation
│   │   └── aliases.md          # Alias definitions
│   ├── vlans/
│   │   └── vlan-config.md      # VLAN assignments and tagging
│   ├── suricata/
│   │   └── suricata-config.md  # IDS/IPS configuration
│   ├── unbound/
│   │   └── dns-config.md       # DNS resolver and blocklists
│   └── wireguard/
│       └── vpn-config.md       # SafeNet tunnel configuration
└── access-point/
    └── eap720-config.md        # TP-Link EAP720 SSID/VLAN mapping
```

> ⚠️ **Coming Soon:** Configuration files will be published prior to launch (January 27, 2026). README structure shown above reflects planned organization.

---

## Hardware Requirements

| Component | Specification |
|-----------|---------------|
| Firewall | Protectli V1410 or VP2430 |
| Access Point | TP-Link EAP720 (WiFi 7, VLAN support) |
| Firmware | Coreboot (open-source BIOS) |

### Performance (Lab Validated)

| Hardware | Throughput | Full Security Stack |
|----------|------------|---------------------|
| V1410 | ~1.2 Gbps | IDS/IPS + DNS filtering enabled |
| VP2430 | ~1.7 Gbps | IDS/IPS + DNS filtering enabled |

See [Security Performance Lab](https://github.com/opensourcesecurity-inc/spl) for methodology and raw data.

---

## Can I Build This Myself?

**Yes.** That's the point of this repository.

SecureNet's configuration is published here. OPNsense is free and open source. You can absolutely replicate it yourself.

### Realistic Time Investment

| Experience Level | Initial Build | Ongoing Maintenance |
|------------------|---------------|---------------------|
| Experienced OPNsense user | 12-15 hours | 2-4 hours/month |
| First-time firewall builder | 25-35 hours | 4-6 hours/month |

### What You Won't Have

- SafeNet VPN service (server infrastructure)
- Security Performance Lab validation
- Professional onboarding consultation
- Pre-tested update validation
- Hardware failure coordination

**If you want to learn networking, we encourage it.** The open-source community is excellent. But SecureNet is for people who want the result without the project.

---

## Version Pinning

SecureNet configurations are tied to specific OPNsense versions:

| SecureNet Version | OPNsense Version | Status |
|-------------------|------------------|--------|
| v1.0 | 25.7.x | Current (Launch) |

We do not auto-update. Each OPNsense upgrade is tested in the [Security Performance Lab](https://github.com/opensourcesecurity-inc/spl) before release.

---

## Related Repositories

| Repository | Description |
|------------|-------------|
| [aiw](https://github.com/opensourcesecurity-inc/aiw) | AI Whitepaper - complete technical documentation |
| [safenet](https://github.com/opensourcesecurity-inc/safenet) | VPN server configuration |
| [spl](https://github.com/opensourcesecurity-inc/spl) | Security Performance Lab data |
| [oss-blocklist](https://github.com/opensourcesecurity-inc/oss-blocklist) | IP blocklist aggregation |

---

## License

This project is licensed under the [BSD 2-Clause License](LICENSE), consistent with OPNsense licensing.

---

## About Open Source Security

Open Source Security, Inc. provides enterprise-grade home network security through professionally configured OPNsense firewalls on Protectli hardware.

🌐 [opensourcesecurity.net](https://opensourcesecurity.net)

**10% of consultation revenue is donated to OPNsense development.**

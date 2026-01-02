# SecureNet OS

**Professionally configured OPNsense for home network security.**

[![OPNsense Version](https://img.shields.io/badge/OPNsense-Rolling%20Stable-blue)](https://opnsense.org/)
[![License](https://img.shields.io/badge/License-BSD%202--Clause-orange)](LICENSE)
[![Download Config](https://img.shields.io/github/v/release/opensourcesecurity-inc/securenet?label=Download&color=ff6b35)](https://github.com/opensourcesecurity-inc/securenet/releases/latest)

---

## What Is SecureNet?

SecureNet is OPNsense, a proven open-source firewall platform, professionally configured for home network security. This repository contains the complete configuration files used in SecureNet deployments.

Every rule, policy, and architectural decision is published.

**You can verify every claim. You can replicate every configuration.**

---

## Security Stack

| Layer | Protection | Scope |
|-------|------------|-------|
| IDS and IPS | Suricata threat detection | Continuously updated rule sets |
| DNS Filtering | Malicious domain blocking | Large curated blocklists |
| IP Blocking | Known malicious IP ranges | Aggregated threat intelligence feeds |
| Network Isolation | Segmented network design | 8 isolated network segments |

---

## Network Architecture

SecureNet implements **8 isolated network segments**, each with explicit trust boundaries and firewall policies.

| Segment | Subnet | Purpose |
|---------|--------|---------|
| LAN1 (Admin) | 192.168.1.0/24 | Primary trusted devices |
| LAN2 (Backup) | 192.168.2.0/24 | Hardware failover |
| IoT Segment | 192.168.20.0/24 | Cameras, sensors, doorbells |
| Smart Segment | 192.168.30.0/24 | TVs, speakers, appliances |
| Guest Segment | 192.168.40.0/24 | Visitor WiFi |
| Kids Segment | 192.168.50.0/24 | Filtered family devices |
| SafeNet WiFi | 10.60.60.0/24 | VPN tunnel over wireless |
| SafeNet Wired | 10.70.70.0/24 | VPN tunnel over Ethernet |

Each segment is isolated by default and permitted traffic is explicitly defined.

---

## OPNsense Version Strategy

SecureNet follows a **rolling stable** OPNsense version model.

All new SecureNet customers are required to run the **latest supported OPNsense release**. This ensures compatibility with core components such as Zenarmor and allows SecureNet to continuously validate security and performance against current upstream releases.

### Update Process

1. New OPNsense releases are first deployed and tested on internal and home SecureNet environments.
2. Early validation continues with a limited set of active SecureNet deployments.
3. After a minimum validation period, typically 30 days, broader customer upgrade guidance is published.

This approach trades long-term version pinning for active validation and faster access to security improvements, while maintaining controlled rollout and documented upgrade paths.

---

## Relationship to SafeNet

SecureNet **requires SafeNet** for VPN-enabled segments.

SafeNet operates as an **upstream egress and privacy service**, not as a local firewall control. All SecureNet security enforcement occurs locally before traffic enters the SafeNet tunnel.

- SecureNet remains the security authority
- SafeNet provides encrypted egress and IP privacy
- Traffic never bypasses SecureNet controls

For SafeNet implementation details, see the SafeNet repository.

---

## Repository Structure

```text
securenet/
├── README.md
├── LICENSE
├── opnsense/
│   ├── config.xml              # Main OPNsense configuration (sanitized)
│   ├── firewall/
│   │   ├── rules.md            # Firewall rule documentation
│   │   └── aliases.md          # Alias definitions
│   ├── segments/
│   │   └── segment-config.md   # Network segmentation design
│   ├── suricata/
│   │   └── suricata-config.md  # IDS and IPS configuration
│   ├── unbound/
│   │   └── dns-config.md       # DNS resolver and blocklists
│   └── wireguard/
│       └── vpn-config.md       # SafeNet tunnel configuration
└── access-point/
    └── eap720-config.md        # TP-Link EAP720 SSID and segment mapping
```

> Note: Some configuration files are staged and published as SecureNet approaches launch readiness.

---

## Hardware Requirements

| Component | Specification |
|-----------|---------------|
| Firewall | Protectli V1410 or VP2430 |
| Access Point | TP-Link EAP720 with VLAN support |
| Firmware | Coreboot (open-source BIOS) |

---

## Performance Validation

Performance is validated in the Security Performance Lab with the full security stack enabled.

| Hardware | Approximate Throughput | Security Features Enabled |
|----------|------------------------|---------------------------|
| V1410 | ~1.2 Gbps | IDS and IPS, DNS filtering |
| VP2430 | ~1.7 Gbps | IDS and IPS, DNS filtering |

Methodology and raw data are published in the Security Performance Lab repository.

---

## Can I Build This Myself?

**Yes.** That is the point of this repository.

OPNsense is free and open source. SecureNet configurations are published here. You can replicate this setup yourself.

### Realistic Time Investment

| Experience Level | Initial Build | Ongoing Maintenance |
|------------------|---------------|---------------------|
| Experienced OPNsense user | 12 to 15 hours | 2 to 4 hours per month |
| First-time firewall builder | 25 to 35 hours | 4 to 6 hours per month |

### What You Will Not Have

- SafeNet VPN server infrastructure
- Security Performance Lab validation
- Professional onboarding consultation
- Pre-tested update validation
- Hardware failure coordination

**If you want to learn networking, we encourage it.** SecureNet is for people who want the result without the project.

---

## Related Repositories

| Repository | Description |
|------------|-------------|
| [aiw](https://github.com/opensourcesecurity-inc/aiw) | AI Whitepaper and technical documentation |
| [safenet](https://github.com/opensourcesecurity-inc/safenet) | SafeNet VPN server configuration |
| [spl](https://github.com/opensourcesecurity-inc/spl) | Security Performance Lab data |
| [oss-blocklist](https://github.com/opensourcesecurity-inc/oss-blocklist) | Threat intelligence aggregation |

---

## License

This project is licensed under the BSD 2-Clause License, consistent with OPNsense licensing.

---

## About Open Source Security

Open Source Security, Inc. provides enterprise-grade home network security through professionally configured OPNsense firewalls on Protectli hardware.

Ten percent of consultation revenue is donated to OPNsense development.

🌐 https://opensourcesecurity.net

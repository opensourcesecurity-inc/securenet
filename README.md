# SecureNet OS

**Professionally configured OPNsense for home network security.**

[![OPNsense Version](https://img.shields.io/badge/OPNsense-26.1-blue)](https://opnsense.org/)
[![License](https://img.shields.io/badge/License-BSD%202--Clause-orange)](/LICENSE)

---

## What Is SecureNet?

SecureNet is OPNsense, a proven open-source firewall platform, professionally configured for home network security. This repository contains annotated configuration excerpts used in SecureNet deployments.

Every rule, policy, and architectural decision is published.

**You can verify every claim. You can understand every configuration.**

---

## Repository Philosophy

This repository exists for **verification, not cloning**.

We publish real configuration excerpts with detailed annotations so security professionals, curious customers, and potential partners can verify our claims. These are not importable configuration files—they are documentation of our implementation.

**Building it yourself?** Start with [OPNsense](https://opnsense.org/download/) and reference the [AI Whitepaper](https://github.com/opensourcesecurity-inc/aiw) for complete configuration guidance.

---

## Security Stack

| Layer | Protection | Scope |
|-------|------------|-------|
| IDS/IPS | Suricata threat detection | Continuously updated rulesets |
| DNS Filtering | Malicious domain blocking | 1M+ curated blocklist |
| IP Blocking | Known malicious IP ranges | Aggregated threat intelligence |
| Network Isolation | Segmented network design | 8 isolated network segments |

---

## Network Architecture

SecureNet implements **8 isolated network segments**, each with explicit trust boundaries and firewall policies.

| Segment | Subnet | Purpose |
|---------|--------|---------|
| LAN1 (Admin) | 192.168.1.0/24 | Primary trusted devices |
| LAN2 (Backup) | 192.168.2.0/24 | Hardware failover |
| IoT | 192.168.20.0/24 | Cameras, sensors, doorbells |
| Smart | 192.168.30.0/24 | TVs, speakers, appliances |
| Guest | 192.168.40.0/24 | Visitor WiFi |
| Kids | 192.168.50.0/24 | Filtered family devices |
| SafeNet WiFi | 10.60.60.0/24 | VPN tunnel (wireless) |
| SafeNet Wired | 10.70.70.0/24 | VPN tunnel (Ethernet) |

Each segment is isolated by default. Permitted traffic is explicitly defined.

---

## Repository Structure

```
securenet/
├── README.md
├── LICENSE
├── opnsense/
│   ├── firewall/
│   │   ├── firewall-rules.xml      # Firewall rules with 3-rule isolation pattern
│   │   └── firewall-aliases.xml    # Network aliases (RFC1918, blocklists)
│   ├── network/
│   │   ├── interfaces.xml          # Interface assignments and subnets
│   │   ├── vlans.xml               # VLAN definitions and tagging
│   │   ├── dhcpd.xml               # DHCP configuration per segment
│   │   └── gateways.xml            # Gateway definitions for policy routing
│   ├── services/
│   │   ├── suricata.xml            # IDS/IPS configuration and rulesets
│   │   ├── unbound.xml             # DNS resolver with DoT and blocklists
│   │   └── monit.xml               # Hardware monitoring and alerting
│   └── vpn/
│       └── wireguard.xml           # SafeNet VPN tunnel configuration
└── access-point/
    └── README.md                   # EAP720 configuration overview
```

### What's Included

Each XML file contains:
- **Real configuration structure** extracted from OPNsense
- **Detailed annotations** explaining every setting
- **Architecture documentation** in the header comments
- **Redacted sensitive values** (keys, passwords, IPs marked as `[REDACTED]`)

### What's NOT Included

- Importable configuration files
- Private keys or credentials
- Customer-specific settings
- Complete config.xml that could be directly deployed

---

## Key Configuration Highlights

### The 3-Rule Isolation Pattern

Untrusted VLANs (IoT, Smart, Guest, Kids) use a consistent isolation pattern:

1. **ALLOW** gateway access (DHCP, DNS to firewall)
2. **BLOCK** all RFC1918 private ranges (prevents lateral movement)
3. **ALLOW** internet (only public IPs reachable after rule 2)

See `opnsense/firewall/firewall-rules.xml` for implementation.

### Policy-Based VPN Routing

SafeNet traffic is selectively routed through WireGuard:

- Admin and isolated VLANs → Direct internet (WAN gateway)
- SafeNet interfaces → VPN tunnel (SafeNet_GW gateway)

The critical `disableroutes=1` setting prevents WireGuard from hijacking all traffic.

See `opnsense/vpn/wireguard.xml` and `opnsense/network/gateways.xml` for implementation.

### DNS Privacy

- DNS-over-TLS to Quad9 and Cloudflare (port 853)
- DNSSEC validation enabled
- 1M+ domains blocked via curated blocklist
- SafeNet traffic uses VPN provider's DNS (queries also tunneled)

See `opnsense/services/unbound.xml` for implementation.

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

| Hardware | Approximate Throughput | Security Features |
|----------|------------------------|-------------------|
| V1410 | ~1.2 Gbps | IDS/IPS, DNS filtering, blocklists |
| VP2430 | ~1.7 Gbps | IDS/IPS, DNS filtering, blocklists |

Methodology and data published in the [Security Performance Lab repository](https://github.com/opensourcesecurity-inc/spl).

---

## Can I Build This Myself?

**Yes.** That is the point of publishing this.

OPNsense is free and open source. These configuration excerpts document exactly how SecureNet is built. You can replicate this setup yourself.

### Realistic Time Investment

| Experience Level | Initial Build | Ongoing Maintenance |
|------------------|---------------|---------------------|
| Experienced OPNsense user | 12-15 hours | 2-4 hours/month |
| First-time firewall builder | 25-35 hours | 4-6 hours/month |

### What DIY Won't Include

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
| [aiw](https://github.com/opensourcesecurity-inc/aiw) | AI Whitepaper - Complete technical documentation |
| [safenet](https://github.com/opensourcesecurity-inc/safenet) | SafeNet VPN server configuration |
| [spl](https://github.com/opensourcesecurity-inc/spl) | Security Performance Lab methodology and data |
| [oss-blocklist](https://github.com/opensourcesecurity-inc/oss-blocklist) | Curated threat intelligence feeds |

---

## License

This project is licensed under the BSD 2-Clause License, consistent with OPNsense licensing.

---

## About Open Source Security

Open Source Security, Inc. provides enterprise-grade home network security through professionally configured OPNsense firewalls on Protectli hardware.

Ten percent of consultation revenue is donated to OPNsense development.

🌐 [opensourcesecurity.net](https://opensourcesecurity.net)

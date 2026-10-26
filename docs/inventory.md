# Inventory and Configuration Reference

**Last documented:** 2026-10-26. Re-check dynamic states before relying on this sheet.

## Confirmed network settings

| Parameter | Value |
| --- | --- |
| Router / default gateway | `192.168.1.254` |
| IPv4 network | `192.168.1.0/24` |
| Netmask | `255.255.255.0` |
| DHCP server | AT&T gateway (enabled) |
| DHCP pool | `192.168.1.64`–`192.168.1.253` |

## Hosts and guests

| Name | Role | IPv4 | OS / software | Resources | Status |
| --- | --- | --- | --- | --- | --- |
| Home | OptiPlex hypervisor | `192.168.1.20` | Proxmox VE 9.2.2 | ~8 GB RAM, ~1.8 TB HDD | Active at last verification |
| Raspberry Pi | Original DNS | `192.168.1.179` | Pi-hole | Unknown | Operational at last verification |
| VM 101 (`pihole-dns`) | New DNS | `192.168.1.21` | Ubuntu Server + Docker + Pi-hole | Originally planned 1.5 GB RAM, 16 GB disk; verify actual | Active/healthy at last verification |
| VM 100 (`ubuntu-server`) | General Linux VM | `192.168.1.183` | Ubuntu Server | Originally 2 GB RAM, 32 GB disk | Shut Down at last verification |

## Physical network hardware reserved for later

- TP-Link TL-R600VPN, hardware V4 — not in use
- Zyxel GS1200-8 managed switch — not in use

## Change record template

| Date | Device | Change | Reason | Validation | Rollback |
| --- | --- | --- | --- | --- | --- |
| YYYY-MM-DD | Example | Example | Example | Example | Example |

## Outstanding facts to verify

- [x] Raspberry Pi DHCP reservation for `.179`
- [ ] Exact installed RAM model/capacity and whether upgrades are supported
- [x] VM 100 current state
- [x] Latest VM 101 configuration and backup status
- [x] Whether the AT&T gateway can advertise custom client DNS servers
- [ ] Teleporter migration completion

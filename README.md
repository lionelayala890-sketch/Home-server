# Home Lab | Proxmox, Pi-hole, Jellyfin & Media Storage

> Personal home server and cybersecurity learning lab. This repository documents architecture, operating procedures, configuration decisions, troubleshooting, and future improvements. Public documentation uses placeholders for private-network data; keep exact home IPs, routes, hostnames, and credentials in private notes.

## Overview

This homelab uses a Dell OptiPlex 7040 running Proxmox VE to host virtual machines and network services. Current reported workloads include Jellyfin and a media-ripping container, with Tailscale providing private remote access and subnet routing. Exact local addressing and route prefixes are intentionally omitted from this public repository.

## Latest Verified Infrastructure Updates — November 4, 2026

These owner-provided updates supersede older or conflicting information in this document. The statuses below are reported by the owner; they have not been independently checked against the live Proxmox or Tailscale configuration.

### Proxmox guests and services

| Guest | Current role / status |
| --- | --- |
| VM 100 | Ubuntu Server; shut down. Do not describe it as an active Pi-hole server. |
| VM 103 | Shut down; no active workload reported. |
| CT 104 | Media ripper. |
| CT 102 | Jellyfin media server; operational. |
| Tailscale gateway | Operational. |

### Hardware

- No RAM upgrade has been installed.
- No SSD/NVMe upgrade has been installed.
- The existing hardware configuration remains in use.

### Tailscale and remote access

- Tailscale subnet routing is reported operational.
- Proxmox and other home-server services are reported accessible remotely through Tailscale.
- Advertised subnet routes are reported approved.
- No route CIDRs, keys, auth tokens, or device-specific access details are published here. Keep access narrowly scoped and do not expose management services through public port forwarding.

## Network architecture (logical, redacted)

```mermaid
flowchart TB
    LAN["Trusted home LAN<br/>private subnet omitted"]
    HOST["Proxmox host<br/>management address omitted"]
    VM100["VM 100<br/>Ubuntu Server — shut down"]
    VM103["VM 103<br/>shut down"]
    CT104["CT 104<br/>media ripper"]
    CT102["CT 102<br/>Jellyfin — operational"]
    TS["Tailscale gateway<br/>subnet routing operational"]
    REMOTE["Authorized remote devices"]
    LAN --- HOST
    HOST --- VM100
    HOST --- VM103
    HOST --- CT104
    HOST --- CT102
    REMOTE -. "private remote access" .-> TS
    TS -. "approved subnet routes; ranges omitted" .-> LAN
```

This is a high-level, owner-reported logical diagram, not a live configuration export. It intentionally excludes private addresses, route ranges, device names, and credentials.

## Hardware inventory

| Equipment | Role | Status |
| --- | --- | --- |
| Dell OptiPlex 7040 | Proxmox host | Existing configuration remains in use |
| Raspberry Pi | Previously documented DNS device | Current role/status not re-verified in latest update |
| ISP router and local network equipment | Gateway / LAN | Exact model, addresses, and configuration kept private |

No RAM or SSD/NVMe upgrade has been installed, per the November 4, 2026 update.

## Security and operations notes

- Do not forward Proxmox management, SSH, Jellyfin administration, DNS, or other management services directly to the public internet.
- Use Tailscale access controls to limit which users and devices can reach the subnet and services; revoke devices that are no longer trusted.
- Keep Tailscale auth keys, node keys, API credentials, recovery material, and client configuration private. Do not commit route CIDRs or sensitive access policy details to this public repository.
- Keep vulnerable lab systems isolated from the family LAN and production services.
- Maintain and test backups independently of the live server and shared media storage.
- Treat the status in this document as owner-reported; verify live state before making operational changes.

## Documentation index

- [Hardware and network inventory](docs/inventory.md)
- [Service runbook](docs/runbook.md)
- [Backup and restore plan](docs/backups.md)
- [Change log](docs/changelog.md)

## Public repository safety

This repository is public. Do not add exact private IP addresses, subnet route ranges, internal hostnames, public IPs, service URLs, credentials, Tailscale keys/tokens, VPN profiles, or backup archives. If any secret was previously committed, revoke or rotate it; deleting it from the latest revision does not remove it from Git history.

## License

Documentation is for personal educational use. Add a license if you intend to permit reuse.

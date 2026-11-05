# Inventory and Configuration Reference

**Last updated:** 2026-11-04. 

> Public repo note: exact local IPs, subnet ranges, internal hostnames, management URLs, and Tailscale route details are intentionally omitted.

## Latest verified guest and service inventory — 2026-11-04

| Guest / component | Role | Current status |
| --- | --- | --- |
| VM 100 | Ubuntu Server | Shut down. Not an active Pi-hole server. |
| VM 103 | Not specified | Shut down. No active workload reported. |
| CT 104 | Media ripper | Operational |
| CT 102 | Jellyfin media server | Operational |
| CT 105 | Tailscale gateway | Remote-access and subnet-routing gateway | Operational |

### Hardware

- No RAM upgrade has been installed.
- No SSD/NVMe upgrade has been installed.
- Existing hardware configuration remains in use.

### Tailscale and remote access

- Subnet routing is reported operational.
- Proxmox and other home-server services are reported accessible remotely through Tailscale.
- Advertised subnet routes are approved.
- Exact route prefixes and device/access details are omitted from this public inventory. Keep auth keys, node keys, API credentials, and client profiles private.

## Earlier network details

Earlier revisions recorded exact private-network addresses and equipment information. Those values have been removed from this public copy.

## Change record template

| Date | Device | Change | Reason | Validation | Rollback |
| --- | --- | --- | --- | --- | --- |
| YYYY-MM-DD | Example | Example | Example | Example | Example |

## Facts to verify during future maintenance

- Confirm current VM and container states in Proxmox before changes; VM 100 and VM 103 are reported shut down as of November 4, 2026.
- Confirm Jellyfin operation and media-ripper workflow after maintenance.
- Confirm Tailscale gateway health, approved route status, access controls, and device authorization without recording secrets here.
- Record actual backup scope, schedule, destination, and restore-test results; do not publish backup archives or credentials.
- Reassess storage/RAM upgrade needs only after inspecting the current hardware. No such upgrades are currently reported installed.

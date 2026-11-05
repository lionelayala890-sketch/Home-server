# Change Log

| Date | Change | Outcome / verification | Next action |
| --- | --- | --- | --- |
| 2026-10 | Installed Proxmox VE 9.2.2 on Dell OptiPlex 7040 | Historical note; exact management address removed from public copy | Continue maintenance and backups |
| 2026-10 | Created Ubuntu VM 101 and deployed Docker Pi-hole | Historical documentation; current state should not be inferred from this entry | Verify current DNS role privately if needed |
| 2026-10 | Identified Ubuntu VM 100 | Current owner-reported status updated below: Ubuntu Server, shut down | Verify before changing its state |

Add entries whenever updating packages, changing services, modifying VM/container configurations, or changing remote access. Record sanitized details only.

## 2026-10-28 — Documentation refresh (historical)

- Added owner-reported Jellyfin, media-ripping, and shared movie-storage roles, plus backup and hardware-upgrade planning.
- Those historical workload IDs and statuses have been superseded by the November 4 update below where they conflict.

## 2026-11-04 — Latest owner-reported infrastructure status

- VM 100: Ubuntu Server installed; shut down. It is not to be described as an active Pi-hole server.
- VM 103: shut down.
- CT 104: media ripper.
- CT 102: Jellyfin media server; operational.
- Tailscale gateway: operational; subnet routing operational, Proxmox and other home-server services accessible remotely, and advertised subnet routes approved.
- No RAM or SSD/NVMe upgrades have been installed; existing hardware configuration remains in use.
- These are owner-provided updates and were not independently validated against the live infrastructure.
- Public documentation intentionally omits exact IP addresses, route prefixes, device/access identifiers, and Tailscale credentials.

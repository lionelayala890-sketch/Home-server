# Change Log

| Date | Change | Outcome / verification | Next action |
| --- | --- | --- | --- |
| 2026-10 | Installed Proxmox VE 9.2.2 on Dell OptiPlex 7040 | Web interface confirmed reachable at `.20` | Backups and maintenance |
| 2026-10 | Created Ubuntu VM 101, deployed Docker Pi-hole | Dashboard accessible at `.21`; Docker container previously healthy | Verify migration settings and DNS cutover |
| 2026-10 | Identified Ubuntu VM 100 by router MAC address | VM previously at `.183` | Confirm retained/stopped/deleted status |

Add entries whenever updating packages, changing IPs, changing DNS, or modifying VM configurations.

## 2026-10-28 — Documentation refresh

- Added owner-reported Jellyfin LXC, MakeMKV media-ripping VM, and shared movie-storage roles alongside Pi-hole.
- Added logical media workflow, operational validation, backup scope and restore planning, SSD/RAM upgrade planning, and proposed VPN checks.
- Preserved previous setup notes and completion records as historical information; flagged conflicting migration notes and unspecified settings as unverified or proposed.
- Documentation only: no live configuration inspected, hardware changed, backup job installed, VPN deployed, or restore test performed.

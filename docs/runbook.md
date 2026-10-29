# Operations Runbook

## Access

| Service | Trusted LAN URL | Notes |
| --- | --- | --- |
| Proxmox | `https://192.168.1.20:8006` | Log in with authorized Proxmox account and 2FA |
| New Pi-hole | `http://192.168.1.21/admin/` | Dedicated VM 101 |
| Raspberry Pi Pi-hole | `http://192.168.1.179/admin/` | Existing installation |

## Validate new Pi-hole

From Windows PowerShell:

```powershell
nslookup google.com 192.168.1.21
Test-NetConnection 192.168.1.21 -Port 80
```

Inside VM 101:

```bash
cd /opt/pihole
sudo docker compose ps
sudo docker compose logs --tail=50
```

## Common faults

**Dashboard not opening:** Verify VM is on, `ip -br addr` confirms `.21`, Compose publishes `192.168.1.21:80`, and Windows port 80 test succeeds. Check logs.

**DNS port 53 conflict:** Inspect `sudo ss -lntup | grep ':53'`; avoid disabling Ubuntu resolver indiscriminately. If Docker uses IP-specific binds, ensure they target the VM's assigned IP.

**Pi-hole unhealthy:** Inspect Compose logs; check persistent `/etc/pihole` directory, gravity updates, permissions, and upstream DNS.

**Loss of family DNS:** Restore original Raspberry Pi connectivity and confirm `nslookup google.com 192.168.1.179`. Avoid changing gateway DHCP until new server is validated.

## Controlled change procedure

1. Record current settings and back up affected service.
2. State expected behavior and rollback plan.
3. Apply one change at a time.
4. Test reachability, DNS, and blocking as appropriate.
5. Record outcome in [change log](changelog.md).

## Maintenance cadence

- Weekly: check container health, host storage capacity, and package updates.
- Monthly: review VM backups and Pi-hole lists; check restore options.
- After any significant change: update documentation and test DNS on both servers.

## Media validation — 2026-10-28

These are proposed checks, not completed tests. Obtain current IDs, addresses, and paths before using them.

1. Confirm Jellyfin LXC and MakeMKV VM identities, running state, resources, and startup settings; do not assign VM 100's identity without checking.
2. Trace shared storage to the MakeMKV output and Jellyfin library. Confirm both reach the same dataset, sufficient free space, and that a missing mount cannot silently redirect writes to a guest root disk.
3. Verify optical-drive access and a small test write from the ripping VM. Inspect permissions from both guests; LXC UID/GID mappings may affect access.
4. Complete a test rip, check its output, scan Jellyfin's library, and play a sample from a trusted LAN client. Hardware transcoding remains unverified.
5. After a controlled restart, confirm storage is available before ripping/library scans. Plan household DNS availability during maintenance using the Raspberry Pi only if it is still operational.

**Missing movies:** Check storage availability, library path, and read permissions inside the LXC before rescanning or changing the library.

**Ripping failure or guest disk fills:** Stop the job; check optical-drive attachment, output mount, write permissions, and capacity. Verify where files landed before cleaning up.

## SSD / RAM change checklist

- [ ] Verify compatible hardware, installed modules, connections, target capacity, and current guest/disk allocations.
- [ ] Record sanitized storage mappings and a rollback plan.
- [ ] Validate backups and recovery; plan DNS availability during downtime.
- [ ] After the hardware change, check detected memory/storage and guest boot.
- [ ] Validate movie mounts, Pi-hole DNS, a test rip, and Jellyfin playback.
- [ ] Record actual installed capacity and results; retain recovery options until checks pass.

## Proposed VPN acceptance checks

VPN deployment, product, and endpoint are unverified.

- Define required remote services and restrict access to those destinations.
- Test from outside the LAN; verify intended routing, remote DNS behavior, and required service access.
- Confirm management and DNS ports are not directly exposed to the public internet.
- Test client revocation and recovery if the endpoint or Proxmox host is unavailable.
- Keep keys, tokens, client profiles, and recovery material private; document sanitized decisions and outcomes only.

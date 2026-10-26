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

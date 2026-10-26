# Backup and Restore Strategy

## Recovery objectives

- Keep a separately backed-up copy of Pi-hole configuration using **Settings → Teleporter**.
- Back up Proxmox VM 101, ideally also any active application VMs, to storage on a **different physical disk** than the OptiPlex's 1.8 TB HDD.
- Preserve Proxmox host/network configuration notes in this repository (without secrets).
- Test restoration; a successful backup task alone is not sufficient proof.

## Suggested plan

| Backup | Interval | Destination | Recovery test |
| --- | --- | --- | --- |
| Pi-hole Teleporter export | After major settings changes | Encrypted offline/private storage | Verify archive and test import in isolated instance |
| VM 101 Proxmox backup | Nightly | External disk or separate NAS | Periodic restore to a different VM ID |
| Other VMs | Nightly if data changes | External disk or separate NAS | Test restoration periodically |

> Backups written to `local` on the same internal HDD do not protect from that HDD failing.

## Restore checklist

- [ ] Identify last known-good backup
- [ ] Confirm destination capacity and VM ID availability
- [ ] Restore VM without overwriting running original
- [ ] Prevent conflicting DHCP/DNS advertising during validation
- [ ] Validate VM boot, IP address, dashboard and DNS response
- [ ] Record result in change log

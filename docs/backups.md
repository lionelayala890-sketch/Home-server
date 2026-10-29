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

## Media homelab backup plan — 2026-10-28

This extends the suggested plan above. Destinations, schedules, retention, completed jobs, and restore tests remain **unverified**; no operational backup is claimed by this update.

| Scope | Proposed coverage | Required recovery validation |
| --- | --- | --- |
| Pi-hole | Teleporter exports and guest backups | Isolated import/restore and DNS test |
| Jellyfin LXC | Guest configuration, database, metadata, and required application state | Consistent backup method; isolated restore with library paths and sample playback |
| MakeMKV VM | Guest OS and settings needed to resume ripping | Optical-drive reattachment and successful test rip |
| Shared movies | Separate file-level backup or explicitly verified storage backup | Verify each external disk, bind mount, or network share is included; guest backup success alone does not prove movie coverage |
| Proxmox host | Sanitized recovery notes here; sensitive configuration backups privately | Reconstruct storage/network and restore guests |

### Proposed implementation order

1. Inventory guest disks and all movie mounts/shares. Map each dataset to a backup job.
2. Choose a separate physical disk or NAS and, where feasible, an additional offline/off-site copy. A copy on the same HDD does not protect against its failure.
3. Select retention and schedules based on change rate and capacity. Nightly guest jobs above are suggestions; movie-backup frequency and acceptable data loss/recovery time remain undecided.
4. Confirm destination availability and free space, review failed jobs, and protect private archives with appropriate access controls.
5. Restore under unused guest IDs on an isolated network. Avoid conflicting DHCP/DNS advertising. Verify Pi-hole DNS, Jellyfin state and playback, MakeMKV drive access, and sample movie-file integrity.
6. Record test date, scope, outcome, and remaining gaps in the change log without secrets.

Before SSD migration or RAM work, create and validate recoverable copies. Shared storage is a working library, not itself a backup. Recheck mount coverage after migration and preserve original data until validation succeeds.

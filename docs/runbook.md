# Operations Runbook

> Public repo note: keep actual management URLs, private IP addresses, subnet route prefixes, internal hostnames, and service-specific access details in secure private notes. This public runbook describes checks generically.

## Latest owner-reported status — 2026-11-04

- VM 100: Ubuntu Server; shut down (not an active Pi-hole server).
- VM 103: shut down.
- CT 104: media ripper.
- CT 102: Jellyfin media server; operational.
- Tailscale gateway and subnet routing: operational; Proxmox and other home-server services are reportedly accessible remotely; advertised routes are approved.
- No RAM or SSD/NVMe upgrades have been installed; existing hardware remains in use.

These statuses are owner-reported and were not independently checked against the live system.

## Access and remote-access safety

- Access Proxmox and home services through authorized trusted-LAN or Tailscale clients only; keep live URLs and IPs in private notes.
- Do not expose Proxmox management, SSH, DNS, or administrative dashboards through public port forwarding.
- Review Tailscale device authorization, access controls, and advertised route approval when making access changes. Limit access to the users/devices and destinations required.
- Keep auth keys, node keys, API credentials, client profiles, and recovery material private. Never commit them to this repository.

## Validate services

Use private values for `PRIVATE_DNS_IP` and `PRIVATE_PIHOLE_IP` in your local operational copy; do not replace these placeholders with real addresses in the public repository.

```powershell
nslookup example.com PRIVATE_DNS_IP
Test-NetConnection PRIVATE_PIHOLE_IP -Port 80
```

Inside the relevant Ubuntu guest, if applicable:

```bash
ip -br addr
sudo docker compose ps
sudo docker compose logs --tail=50
```

## Proxmox guest checks

Before a maintenance operation, inspect the current guest list and verify the target by its ID and role. Per the latest update, VM 100 and VM 103 are shut down, CT 104 is the media ripper, and CT 102 is Jellyfin. Do not assume an older VM/container mapping is current.

After planned maintenance, check that CT 102 starts and serves Jellyfin, CT 104 can access its intended media workflow, and remote access still works through authorized Tailscale devices. Do not publish private route ranges or service addresses in test records.

## Controlled change procedure

1. Record current settings privately and back up the affected service.
2. State expected behavior and rollback plan.
3. Apply one change at a time.
4. Test reachability, service behavior, and relevant access controls.
5. Record a sanitized outcome in [change log](changelog.md).

## Maintenance and recovery

- Review service health, host storage capacity, and package updates regularly.
- Review VM/container backups and test restores; shared media storage is not itself a backup.
- After significant changes, verify Jellyfin, the media-ripping workflow, Tailscale route approval, and access policy.
- No RAM or SSD/NVMe upgrade is currently reported installed. Confirm hardware state before planning or documenting upgrades.

## Proposed VPN/Tailscale acceptance checks

Tailscale is reported operational; these are ongoing checks, not a claim that every control has been independently audited.

- Confirm only intended users and devices are authorized.
- Confirm advertised routes remain approved and restricted to intended access.
- Test remote access from an authorized client and verify unintended services are not reachable.
- Test device revocation and recovery if the gateway or Proxmox host is unavailable.
- Keep keys, tokens, client profiles, and route-specific configuration private; document sanitized decisions only.

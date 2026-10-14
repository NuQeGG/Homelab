# Operations and maintenance

These are the checks I use to keep the lab and its documentation aligned.

## Read-only checks

Run these in the relevant Proxmox node's shell:

```bash
# Proxmox host version, separate from the guests' OS versions
pveversion

# Guests hosted on this node
pct list
qm list

# Storage availability
pvesm status

# Reported host memory
free -h
```

These checks provide an inventory and resource view. A running guest still needs an application-level check.

## After an application or OS update

1. Confirm the guest is running and its service has started.
2. Open the application and test its main function.
3. Verify storage access, permissions, and integrations.
4. Check the client that matters: public web access, the iPad, or the TV.
5. Update the documentation if placement, data paths, or access methods changed.

For the media stack, use a representative movie or episode to check playback, subtitles, and processing. For a website, check both page display and the content admin workflow. For the dashboard, inspect the API widgets as well as the page itself.

## Diagnosing a broken dependency

Work through the relevant layers: Proxmox host, guest, application process, storage access, integration/API, and client connection path. The missing Bazarr mount and outdated Jellyfin dashboard widget were examples where a service appeared available but a dependency failed.

For Docker-based applications, distinguish the LXC guest from the Docker application inside it. A successful `pct list` does not confirm Docker health, and a healthy web endpoint does not confirm access to the media library.

## Inventory changes

When a guest is added, moved, deleted, or replaced:

- Update [service-inventory.md](service-inventory.md).
- Refresh the dashboard's generated guest mappings.
- Review affected tunnel routes, storage dependencies, and private access notes.

VM IDs can be reused. Check the current name and node before using a command copied from an old setup guide.

## Updating this repository

Keep current behaviour separate from plans. Record the date of an inventory or successful test, and avoid describing an old screenshot as live state. Keep exact versions in dated operational records when they matter to an issue, rather than treating them as permanent architecture facts.

[Proxmox VE documentation](https://pve.proxmox.com/pve-docs/) · [Back to overview](../README.md)

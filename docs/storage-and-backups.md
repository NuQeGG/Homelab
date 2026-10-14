# Storage and backups

## Current storage entries

The Proxmox inventory on 14 October 2026 shows the following storage names. These are **Proxmox storage entries**, not a verified list of individual physical disks or their capacities.

| Node | Storage entries shown |
| --- | --- |
| `NuQe` | `SSDLenovo1`, `local`, `local-lvm` |
| `NuQe1G` | `HDDLenovo2`, `local`, `local-lvm` |
| `NuQeGG` | `HDDWhite1`, `HDDWhite2`, `SSDWhite1`, `backup-ssd`, `local`, `local-lvm` |

The physical device mapping, storage types, capacities, and actual usage still need a fresh inventory. Names alone do not establish redundancy or free space.

## Shared media storage

Earlier setup work records a mergerfs media pool on `NuQeGG`, presented to relevant services at `/mnt/media`. Media applications need consistent paths and suitable permissions to see the same library.

FileFlows was initially configured with read-only media input and separate writable temporary/output locations while testing. Later processing settings changed as the workflow developed. The current mount modes and replacement behaviour should be recorded from the active configuration before using the original test setup as a recovery guide.

A Proxmox guest disk and a host bind-mounted media directory have different backup requirements. Restoring a container does not, by itself, establish that its externally mounted library has also been restored.

## Current backup status

**Backups are not currently in use.** The `backup-ssd` entry exists, but it does not represent an active scheduled backup or a tested restore process.

An old Lenovo gaming laptop with an i5, 8 GB DDR3, and approximately 500 GB storage was considered for Proxmox Backup Server. That remains a planning option; PBS is not documented as deployed.

## Proposed backup scope

The first priority is data that is difficult to recreate:

| Workload | Data to account for |
| --- | --- |
| Websites | PHP source, editable content, assets, and private admin configuration |
| Dashboard | Homepage configuration, secrets, and Speedtest Tracker data |
| Vaultwarden | Application data, database, attachments, and a tested application recovery procedure |
| Media applications | Settings, databases, and integrations; media files handled explicitly |
| RomM | Application data and the library, including any externally mounted storage |
| Desktop | Useful user files, project files, and application settings |
| Infrastructure | Proxmox configuration notes, mount definitions, and private tunnel configuration |

This is a proposed scope, rather than a list of completed backup jobs. Storage planning should use the amount of included data and its rate of change, rather than the total advertised capacity of every server disk.

## First recovery milestone

1. Record storage types, guest disks, mount points, and application data locations.
2. Choose a backup destination and retention policy based on the included data.
3. Create a backup of a small, noncritical guest.
4. Restore it to an unused guest ID on an isolated network and verify its application and data.
5. Extend coverage and record a successful restore date for each important workload.

For LXC backups, additional storage-backed mount points require attention to their backup setting. Bind mounts and device mounts need a separate data protection method. See the [official Proxmox backup documentation](https://github.com/proxmox/pve-docs/blob/master/vzdump.adoc) and [container documentation](https://pve.proxmox.com/pve-docs/chapter-pct.html).

[Proxmox Backup Server documentation](https://pbs.proxmox.com/docs/) · [Back to overview](../README.md)

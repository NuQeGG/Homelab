# Storage

## Storage used by the lab

These Proxmox storage entries were recorded on 14 October 2026. They describe the storage used by the workloads below, rather than individual physical disks or their capacities.

| Node | Storage entries |
| --- | --- |
| `NuQe` | `SSDLenovo1`, `local`, `local-lvm` |
| `NuQe1G` | `HDDLenovo2`, `local`, `local-lvm` |
| `NuQeGG` | `HDDWhite1`, `HDDWhite2`, `SSDWhite1`, `local`, `local-lvm` |

I still need to record the physical disk mapping, storage types, capacities, and current usage.

## Shared media storage

The media setup uses a mergerfs pool on `NuQeGG`, presented to the relevant services at `/mnt/media`. The applications need consistent paths and suitable permissions to access the same library.

FileFlows was initially configured with read-only media input and separate writable temporary/output locations while testing. The processing settings changed as the workflow developed, so I still need to record the current mount modes and file replacement behaviour.

## Guest and application paths

Host, LXC, and Docker paths can differ. When troubleshooting library access, I check the path at each layer and confirm that the actual service account can read or write it.

The [media stack guide](projects/media-stack.md) covers the shared media paths. The [RomM guide](projects/romm.md) lists the mounts inside its streaming container.

[Back to overview](../README.md)

# NuQe Homelab

My homelab is where I turn an interest in IT support, hardware, and Linux into practical experience. I run a three-node Proxmox VE cluster for media services, web hosting, remote access, and everyday applications. This repository documents how the pieces fit together, what I have learned, and what still needs improving.

**Inventory reviewed: 14 October 2026.** The current setup has **19 LXC containers and 2 virtual machines** across `NuQe`, `NuQe1G`, and `NuQeGG` in `NuQeCLUSTER`. My Debian systems are updated to Debian 13; the Bambu Studio desktop remains Ubuntu. Application updates were completed as of this review. Exact package versions are kept out of this overview because they change frequently.

## At a glance

| Node | Main role | Guests |
| --- | --- | ---: |
| `NuQe` | RomM and its streaming companion | 1 VM + 1 LXC |
| `NuQe1G` | Websites, dashboard, network utilities, and a remote desktop | 1 VM + 6 LXC |
| `NuQeGG` | Media streaming, automation, and processing | 12 LXC |

```mermaid
flowchart TB
    P["Proxmox VE · NuQeCLUSTER"]
    P --> N["NuQe"]
    P --> W["NuQe1G"]
    P --> M["NuQeGG"]
    N --> R["RomM VM + Selkies streaming LXC"]
    W --> WEB["CV and PC websites"]
    W --> UTIL["Homepage · Pi-hole · Tailscale · Vaultwarden"]
    W --> DESK["Ubuntu desktop · Bambu Studio"]
    M --> MEDIA["Jellyfin · Seerr · Radarr · Sonarr"]
    M --> TOOLS["Prowlarr · Bazarr · FileFlows · download tools"]
    M --> TUNNEL["Cloudflare Tunnel"]
```

The diagram shows workload placement, rather than physical network links or every service dependency.

## Documentation

| Guide | What it covers |
| --- | --- |
| [Proxmox setup](docs/proxmox-setup.md) | Cluster roles, LXC/VM choices, and workload separation |
| [Hardware](docs/hardware.md) | Reused computers, GPU, switching, and hardware details to refresh |
| [Service inventory](docs/service-inventory.md) | All 21 current guests, their IDs, and their purposes |
| [Networking](docs/network-setup.md) | Local network, Cloudflare Tunnel, Tailscale, and public IP constraints |
| [Storage and backups](docs/storage-and-backups.md) | Storage locations, shared media, and the backup work still ahead |
| [Media stack](docs/projects/media-stack.md) | Jellyfin, media management, subtitles, and GPU processing |
| [Web hosting](docs/projects/web-services.md) | Two PHP websites hosted in separate Debian containers |
| [Dashboard](docs/projects/dashboard.md) | Homepage, Proxmox metrics, Pi-hole, and speed tests |
| [RomM](docs/projects/romm.md) | Library management and the Selkies streaming companion |
| [Remote desktop](docs/projects/remote-desktop.md) | Ubuntu and Bambu Studio accessed from an iPad |
| [Operations](docs/operations.md) | Inventory checks, maintenance, and verification after changes |
| [Lessons and roadmap](docs/lessons-and-roadmap.md) | Practical findings, retired experiments, and future work |

## What I practise here

- Linux administration and troubleshooting across hosts, containers, and applications.
- Choosing between lightweight LXC services and full virtual machines.
- Hosting websites with Nginx, PHP, and editable content.
- Connecting services through shared storage, API integrations, and tunnels.
- Configuring GPU access for media workloads and checking actual playback behaviour.
- Writing scripts, checking changes, and keeping useful recovery notes.

## Current limits

I do not currently use backups, even though a storage entry named `backup-ssd` exists. A backup and restore process is a priority, rather than a completed feature. The Minecraft server was deleted because I do not have a public IP for direct hosting; VM 119 now runs the Bambu Studio desktop.

This is an evolving home environment. A cluster and separate guests help organise workloads, but I am not claiming high availability, automatic failover, or a tested disaster recovery solution.

## Public documentation

This repository contains architecture, service roles, and useful operating notes. Credentials, private connection details, complete application configurations, and unfiltered logs stay outside it.

[My CV website](https://cv.nuqehosting.uk/) · [My PC website](https://pc.nuqehosting.uk/) · [GitHub profile](https://github.com/NuQeGG)

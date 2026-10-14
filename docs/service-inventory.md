# Service inventory

I checked this inventory on **14 October 2026**. All listed guests were running at the time.

## NuQe

| ID | Guest name | Type | Purpose |
| ---: | --- | --- | --- |
| 115 | `RomM` | VM | ROM library management |
| 117 | `romm-stream` | LXC | LinuxServer Webstation/Selkies in Docker, with Intel graphics mapped through `/dev/dri` |

## NuQe1G

| ID | Guest name | Type | Purpose |
| ---: | --- | --- | --- |
| 107 | `Tailscale` | LXC | Private remote connectivity |
| 108 | `CVWeb` | LXC | Danish CV website and its content admin panel |
| 110 | `PCWeb` | LXC | PC, setup, and social links website |
| 111 | `Dashboard` | LXC | Homepage dashboard and Speedtest Tracker |
| 113 | `pihole` | LXC | DNS filtering and dashboard statistics |
| 114 | `Vaultwarden` | LXC | Self-hosted password management |
| 119 | `bambu-desktop` | VM | Ubuntu desktop for Bambu Studio access from an iPad |

## NuQeGG

| ID | Guest name | Type | Purpose |
| ---: | --- | --- | --- |
| 100 | `Jellyfin` | LXC | Media streaming and playback |
| 101 | `Cloudflare` | LXC | Cloudflare Tunnel connectivity |
| 102 | `radarr` | LXC | Movie library management |
| 103 | `sonarr` | LXC | Series library management |
| 104 | `prowlarr` | LXC | Indexer integration |
| 105 | `Seerr` | LXC | Media requests |
| 106 | `Gluetun` | LXC | Download environment containing Gluetun and qBittorrent |
| 109 | `Bazarr` | LXC | Subtitle management |
| 112 | `Fileflows` | LXC | Media processing and encoding |
| 116 | `Doplarr` | LXC | Discord-based request integration |
| 118 | `maintainerr` | LXC | Media library maintenance |
| 120 | `flaresolverr` | LXC | Companion integration used by the indexer stack |

## Guests versus applications

The table lists Proxmox guests. Some guests contain multiple applications, so it is not a complete count of processes or Docker containers. qBittorrent runs inside CT 106 alongside Gluetun and therefore has no separate Proxmox guest. This placement was confirmed on 14 October 2026; the exact application deployment and network attachment still need configuration-level documentation.

Vaultwarden, Doplarr, Maintainerr, and FlareSolverr are present in the current inventory. I still need to document their detailed policies and integrations from the actual configurations.

[Back to overview](../README.md)

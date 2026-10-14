# Hardware

The homelab reuses small Lenovo computers and an older gaming PC. The small systems handle general services, while the gaming PC provides more capacity and an NVIDIA GPU for the media stack.

## Documented machines

| Node | Platform | Previously documented specification | Current role |
| --- | --- | --- | --- |
| `NuQe` | Lenovo ThinkCentre M910q | Intel Core i5-7500T, 8 GB RAM | RomM and `romm-stream` |
| `NuQe1G` | Lenovo ThinkCentre M910q | Intel Core i5-7500T, 8 GB RAM | Web hosting, dashboard, utilities, Ubuntu desktop |
| `NuQeGG` | Reused gaming PC | Intel Core i5-8400, 16 GB RAM, NVIDIA GTX 1060 6 GB | Media services and processing |

These specifications come from the earlier repository and setup notes. The current screenshot confirms the three nodes and their guests, but does not show CPU models or installed RAM. Recheck the figures after hardware upgrades before using them for capacity planning.

## Networking equipment

The documented switch is a **TP-Link TL-SG108S**, an eight-port gigabit switch. An ISP-provided router handles the existing connection. A Philips Hue Bridge has also been mentioned as equipment to accommodate in the rack, rather than as a Proxmox guest.

## GPU use

`NuQe` exposes Intel integrated graphics to CT 117. Diagnostics identify vendor `0x8086`, device `0x5912`, and driver `i915`. The LXC's `/dev/dri` is also mapped into Docker container `romm-webstation`, which runs the Selkies streaming environment. Device exposure is verified; the encoder active during a stream has not yet been measured.

The GTX 1060 is used by the media environment. Setup notes record NVIDIA device access in the FileFlows LXC and Docker environment, and later Jellyfin testing showed successful transcoding with GPU access.

GPU visibility, selecting an encoder, and successfully processing a file are separate checks. I verify the application output and playback rather than treating a successful device listing as proof that every job uses hardware acceleration. Concurrent Jellyfin and FileFlows work also shares the same physical GPU.

## Physical organisation

A modular HomeRacker build has been explored to organise the Lenovo systems, switch, and Hue Bridge using printed parts. It remains a hardware project; this documentation does not assume that the rack has been assembled. The gaming tower is intended to sit separately.

## Details to record next

- Current CPU and installed memory for each node.
- Physical disk models and capacities, mapped to Proxmox storage entries.
- Guest resource allocations and remaining host capacity.
- Completed rack layout, airflow, and temperatures under load.

[Back to overview](../README.md)

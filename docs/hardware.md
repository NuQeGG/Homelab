# Hardware

The homelab reuses small Lenovo computers and an older gaming PC. The small systems handle general services, while the gaming PC provides more capacity and an NVIDIA GPU for the media stack.

## Documented machines

| Node | Platform | Previously documented specification | Current role |
| --- | --- | --- | --- |
| `NuQe` | Lenovo ThinkCentre M910q | Intel Core i5-7500T, 8 GB RAM | RomM and `romm-stream` |
| `NuQe1G` | Lenovo ThinkCentre M910q | Intel Core i5-7500T, 8 GB RAM | Web hosting, dashboard, utilities, Ubuntu desktop |
| `NuQeGG` | Reused gaming PC | Intel Core i5-8400, 16 GB RAM, NVIDIA GTX 1060 6 GB | Media services and processing |

These are the specifications I previously recorded. I still need to recheck the installed RAM and CPU models against the current machines.

## Networking equipment

I use a **TP-Link TL-SG108S**, an eight-port gigabit switch, with the ISP-provided router. The planned rack layout also needs room for a Philips Hue Bridge.

## GPU use

`NuQe` exposes Intel integrated graphics to CT 117. Diagnostics identify vendor `0x8086`, device `0x5912`, and driver `i915`. The LXC's `/dev/dri` is also mapped into Docker container `romm-webstation`, which runs the Selkies streaming environment. Device exposure is verified; the encoder active during a stream has not yet been measured.

The GTX 1060 is used by the media environment. Setup notes record NVIDIA device access in the FileFlows LXC and Docker environment, and later Jellyfin testing showed successful transcoding with GPU access.

GPU visibility, selecting an encoder, and successfully processing a file are separate checks. I verify the application output and playback rather than treating a successful device listing as proof that every job uses hardware acceleration. Concurrent Jellyfin and FileFlows work also shares the same physical GPU.

## Physical organisation

I have been planning a modular HomeRacker build with printed parts for the Lenovo systems, switch, and Hue Bridge. It is still a project in progress, with the gaming tower intended to sit separately.

<img width="900" alt="Hardware image from the original documentation" src="https://github.com/user-attachments/assets/1f9c63d1-9806-4487-8ca7-9a4a8c7b0e4c" />

## Details to record next

- Current CPU and installed memory for each node.
- Physical disk models and capacities, mapped to Proxmox storage entries.
- Guest resource allocations and remaining host capacity.
- Completed rack layout, airflow, and temperatures under load.

[Back to overview](../README.md)

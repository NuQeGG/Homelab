# Proxmox setup

## Cluster layout

The environment is organised as `NuQeCLUSTER`, with three Proxmox VE nodes. On 14 October 2026, the current inventory contains 21 guests: 19 LXC containers and 2 QEMU virtual machines.

| Node | Workload group | Deployment approach |
| --- | --- | --- |
| `NuQe` | RomM and its streaming companion | One VM and one LXC |
| `NuQe1G` | Websites, dashboard, Pi-hole, Tailscale, Vaultwarden, Bambu Studio | Six LXC containers and one Ubuntu VM |
| `NuQeGG` | Media applications and Cloudflare connectivity | Twelve LXC containers; Docker used within selected guests |

The [service inventory](service-inventory.md) is the reference for guest names and IDs. Placement describes where services run today, rather than a guarantee that guests can migrate freely between nodes.

## Why use LXC and VMs together?

Most services are small Linux applications. Separate LXC containers make their roles easier to identify and maintain without allocating a complete desktop operating system to each application.

Full VMs are used for RomM and the Ubuntu desktop. The desktop needs a graphical environment and Bambu Studio, while the RomM VM follows its existing deployment. Docker is an application deployment layer inside selected guests; a Docker container is not an additional Proxmox guest.

The public websites run Nginx and PHP in their own Debian LXCs. Earlier documentation described them as Docker deployments; the website setup notes show the direct PHP/LXC arrangement instead.

## Operating systems and updates

My Debian systems have been updated to Debian 13 as of 14 October 2026. `bambu-desktop` remains an Ubuntu desktop. Applications were updated for this review, but a software version should be checked on the relevant host or application before troubleshooting a version-specific issue.

The Proxmox host version is tracked separately from guest operating systems. A Debian guest upgrade does not establish the installed Proxmox VE release or host kernel.

## Workload separation

The gaming PC carries the media stack and GPU processing. The Lenovo nodes carry web services, utilities, RomM, and the desktop. This keeps service ownership clear and makes changes easier to target.

That separation has practical limits: services on one physical machine share its CPU, memory, storage, and failure domain. The media applications also depend on the availability and permissions of their shared files.

## Availability and recovery

The cluster provides a unified way to manage the environment. High availability, shared storage for automatic relocation, and tested recovery are not documented as implemented. There is currently no active backup process.

The maintenance checklist is to check available host memory and storage before creating a guest, assign an unused guest ID, and record the application's storage and access requirements. Deleting or replacing a guest also calls for an inventory and dashboard mapping update.

[Official Proxmox VE documentation](https://pve.proxmox.com/pve-docs/) · [Storage and backups](storage-and-backups.md) · [Back to overview](../README.md)

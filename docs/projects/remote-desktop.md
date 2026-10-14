# Ubuntu desktop for Bambu Studio

## Purpose

`bambu-desktop`, VM 119 on `NuQe1G`, provides an Ubuntu desktop so my fiancée can use the desktop version of Bambu Studio from her iPad Pro. It is an everyday use for the homelab alongside the infrastructure projects.

The desktop works over the home network. It remains Ubuntu after the Debian systems were updated to Debian 13.

## Deployment

The original setup used an Ubuntu 24.04 cloud image, XFCE, and XRDP, with Bambu Studio installed in the guest. Its initial allocation was 2 virtual cores, 4 GiB RAM, and a 64 GiB disk. Those are deployment starting values; current allocations should be checked in Proxmox before treating them as capacity figures.

The user reported that the desktop works well. A later update prepared a native Firefox installation and an authenticated SMB file share for transferring files from the iPad. The share's current deployment should be confirmed before describing it as an available feature.

## Access and files

The iPad displays the desktop through an RDP client. An SMB share was the proposed route for STL and 3MF transfers using the iPad Files app. Sharing files and displaying a remote desktop are separate functions; a working RDP session does not establish that file transfer has been configured.

The desktop's addresses, account details, and any file-sharing credentials stay in private notes.

## Practical learning

- Deploying a desktop VM from a cloud image.
- Configuring a graphical session and remote access.
- Troubleshooting application packaging in a remote Linux desktop.
- Separating client access, guest resources, and file transfer requirements.

## Maintenance

After a guest update, verify login from the iPad and launch Bambu Studio using a representative project. Record changes to resource allocations and preserve user project files when implementing backups.

[XRDP project](https://github.com/neutrinolabs/xrdp) · [Back to overview](../../README.md)

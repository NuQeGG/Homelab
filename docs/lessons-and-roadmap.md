# Lessons and roadmap

## Lessons from running the lab

### A running container does not guarantee a working application

Bazarr's missing media mount prevented useful library access even though its web interface was available. Checking the actual service account's file access was more useful than only checking whether the guest was running.

### Integrations have their own compatibility requirements

Jellyfin's dashboard widget broke after an application update. Testing the endpoints separated an API compatibility problem from a credential problem, and updating the widget version resolved it.

### GPU access and output quality need separate verification

Seeing the NVIDIA device is one step. Successful processing, the selected encoder, retained audio/subtitle streams, and playback on a TV require their own checks. Dark-scene blockiness led to a higher FileFlows quality setting; brightness flicker still needed playback investigation.

### Hardware limits shape the workload

The compact Lenovo systems are useful for lightweight services. A desktop, game server, or several busy applications need resource planning alongside the existing guests. Idle-server ideas do not remove the need to size for simultaneous use.

### Public web hosting and game hosting have different access needs

Cloudflare Tunnel supports the website access path in this lab. It did not solve the Minecraft connection experiment. The Minecraft server has been deleted because there is no public IP for direct hosting.

### A storage name is not a backup process

`backup-ssd` is present, but backups are not currently used. A recovery plan needs included data, jobs, retention, and a successful restore test.

## Next priorities

| Priority | Work | Current position |
| --- | --- | --- |
| 1 | Backups and recovery | No active backup process; define scope and perform the first restore test |
| 2 | Inventory detail | Record current RAM, disks, guest allocations, storage mappings, and application data locations |
| 3 | Media quality | Test the affected TV playback and document the final processing configuration |
| 4 | Dashboard accuracy | Ensure the generated inventory reflects the current guests, especially VM 119 |
| 5 | RomM documentation | Webstation image digest, Intel graphics mapping, and Docker mounts recorded; document the VM/library integration, clients, and active encoder |
| 6 | Physical organisation | Continue the planned HomeRacker build and measure temperatures |
| Future | Networking | Explore a dedicated firewall/router, managed switching, and VLANs |

## Paused or exploratory projects

- **Minecraft:** deleted; game hosting is paused because of the public IP constraint.
- **Counter-Strike:** discussed as a future game-hosting workload; not in the current guest inventory.
- **TeamSpeak:** an earlier idea; no current guest is documented.
- **Proxmox Backup Server:** an old laptop was considered; not deployed as a confirmed backup solution.
- **pfSense/Cisco/UniFi:** networking directions to explore, rather than the present topology.

[Back to overview](../README.md)

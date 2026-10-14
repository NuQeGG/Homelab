# Lessons and roadmap

## Lessons from running the lab

### A running container does not guarantee a working application

Bazarr's missing media mount prevented useful library access even though its web interface was available. Checking the actual service account's file access was more useful than only checking whether the guest was running.

### Integrations have their own compatibility requirements

Jellyfin's dashboard widget broke after an application update. Testing the endpoints separated an API compatibility problem from a credential problem, and updating the widget version resolved it.

### GPU access and output quality need separate verification

Seeing the NVIDIA device is one step. Successful processing, the selected encoder, retained audio/subtitle streams, and playback on a TV require their own checks. Dark-scene blockiness led to a higher FileFlows quality setting; brightness flicker still needed playback investigation.

### Hardware limits shape the workload

The compact Lenovo systems are useful for lightweight services. A desktop or several busy applications need resource planning alongside the existing guests, especially when they are used at the same time.

## Next priorities

| Priority | Work | Current position |
| --- | --- | --- |
| 1 | Inventory detail | Record current RAM, disks, guest allocations, storage mappings, and application data locations |
| 2 | Media quality | Test the affected TV playback and document the final processing configuration |
| 3 | Dashboard accuracy | Keep the generated inventory aligned with the current guests |
| 4 | RomM documentation | Webstation image digest, Intel graphics mapping, and Docker mounts recorded; document the VM/library integration, clients, and active encoder |
| 5 | Physical organisation | Continue the planned HomeRacker build and measure temperatures |
| Future | Networking | Explore a dedicated firewall/router, managed switching, and VLANs |

## Paused or exploratory projects

- **Counter-Strike:** discussed as a future game-hosting workload; not in the current guest inventory.
- **TeamSpeak:** an earlier idea; no current guest is documented.
- **pfSense/Cisco/UniFi:** networking directions to explore, rather than the present topology.

[Back to overview](../README.md)

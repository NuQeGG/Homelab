# RomM and streaming companion

## Current placement

| Guest | Type | Node | Purpose |
| --- | --- | --- | --- |
| 115, `RomM` | VM | `NuQe` | ROM library management |
| 117, `romm-stream` | LXC | `NuQe` | Selkies desktop/game streaming companion |

Both guests are present and running in the 14 October 2026 inventory. Earlier repository text called this Lenovo available for future use; it now has an established workload.

## Scope

The project combines library management with a separate streaming companion. I use CT 117 for streaming games associated with the VM. It runs LinuxServer Webstation with Selkies and a mapped Intel graphics device. The exact connection to the RomM VM, client access path, and configured stream transport still need recording.

## Verified streaming environment

Read-only diagnostics from CT 117 on 14 October 2026 establish:

| Component | Observed configuration |
| --- | --- |
| LXC operating system | Debian GNU/Linux 13 (trixie), reported full version 13.7 |
| Application deployment | Docker, with `romm-webstation` running |
| Application image | `lscr.io/linuxserver/webstation`, pinned by the digest recorded below |
| Streaming software | A running `selkies` process |
| Supporting processes | `labwc`, `pulseaudio`, `nginx`, and `webstation-brok` as shown in the process list |
| Graphics devices exposed to the LXC | `/dev/dri/card0` and `/dev/dri/renderD128` |
| GPU vendor/device IDs | Intel `0x8086`, device `0x5912` |
| Host graphics driver visible through sysfs | `i915` |
| Docker device mapping | `/dev/dri` in the LXC mapped to `/dev/dri` in `romm-webstation`, permissions `rwm` |

The verified image reference is:

```text
lscr.io/linuxserver/webstation@sha256:b1a81346740cdea6d538573b20e17ff496947cdac65ff495182400a47c43be00
```

This records the deployed image content rather than an assumed `latest` tag or an unverified application version.

[LinuxServer Webstation](https://docs.linuxserver.io/images/docker-webstation/) uses the [Selkies streaming platform](https://docs.linuxserver.io/selkies/) to deliver a desktop or application to a browser. The deployed image and process inventory identify this stack in the lab; the specific configured transport and encoder have not yet been checked.

The Intel vendor ID and `i915` driver confirm Intel graphics, and Docker inspection confirms the `/dev/dri` mapping into the application container. This is the Lenovo's integrated graphics setup, separate from the NVIDIA media GPU on `NuQeGG`. Device exposure is confirmed; the actual encoder and use of hardware acceleration during a stream still require a runtime check.

## Persistent mounts

Docker inspection confirms these mounts. The source paths are **inside CT 117**, which is Docker's host; their underlying storage on the Proxmox node has not yet been mapped.

| Source in CT 117 | Destination in `romm-webstation` | Role |
| --- | --- | --- |
| `/opt/romm-stream/config` | `/config` | Persistent application configuration |
| `/opt/romm-stream/custom-cont-init.d` | `/custom-cont-init.d` | Custom container initialisation files |
| `/opt/romm-stream/library` | `/romm/library` | Game library presented to the streaming application |

The image reference, deployment definition, configuration, custom initialisation files, and library data should be accounted for in a future backup plan. The mount listing does not establish how the library is shared with VM 115.

Earlier troubleshooting explored PlayStation 2 and PlayStation 3 support and missing browser play controls. A platform being recognised in the library does not establish that browser emulation or streaming for that platform is configured and working.

## What to record next

- RomM deployment and persistent application data locations.
- Library storage and how it is exposed to each guest.
- The deployment definition, access path, and how the library is shared with VM 115.
- The encoder used during a stream and a representative playback test.
- Supported clients and one successfully tested playback example.
- Configuration and library backup requirements.

There is no active backup process at present. Application data and externally mounted library files must both be accounted for in a recovery plan.

[RomM project](https://github.com/rommapp/romm) · [Service inventory](../service-inventory.md) · [Back to overview](../../README.md)

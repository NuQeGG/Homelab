# Network setup

## Local network

The documented physical setup uses an ISP router and a TP-Link TL-SG108S gigabit switch. The three Proxmox nodes connect to the local network, with guests attached through Proxmox networking.

Each node shows a network entry named `localnetwork` in the current inventory. The screenshot does not establish its underlying bridge definition, VLAN tagging, or firewall rules. Those details should come from the actual network configuration.

Managed switching, VLAN separation, and a dedicated pfSense router are future ideas. The current documentation does not claim those features are deployed.

## Public websites

The two documented websites are:

- [cv.nuqehosting.uk](https://cv.nuqehosting.uk/): personal CV.
- [pc.nuqehosting.uk](https://pc.nuqehosting.uk/): PC setup and social links.

The websites use Cloudflare Tunnel to reach their local web services. The tunnel guest is CT 101 on `NuQeGG`, while the websites are CTs 108 and 110 on `NuQe1G`. This creates a dependency across nodes: a working website guest alone does not prove its public access path is available.

Cloudflare Tunnel establishes outbound connectivity from the local environment, which supports this web hosting arrangement without direct inbound access to a public IP. See [Cloudflare's connection model](https://developers.cloudflare.com/tunnel/configuration/). The exact hostname routes and access policies belong in private operational notes.

## Private access

Tailscale runs in CT 107. It is part of the private access setup. Subnet routes, exit-node use, and device access policies should be recorded from the live configuration rather than inferred from the guest name.

Pi-hole runs in CT 113, with DNS statistics available on the dashboard. The exact router/client DNS assignment and any fallback resolvers still need documenting.

## Game hosting constraint

I do not have a public IP for direct game hosting. A Minecraft server was tested locally and an external tunnel was investigated, but that server has since been deleted. Public websites working through Cloudflare Tunnel do not establish a working Minecraft or Counter-Strike connection path.

Game hosting is paused until there is a suitable connection method and enough reason to maintain it.

## Access boundaries

Public portfolio websites and private management tools serve different purposes. Proxmox, the dashboard, remote desktop, and application admin interfaces should have their actual access controls recorded and checked. This page describes the architecture without asserting that a particular protection has already been configured.

[Cloudflare Tunnel documentation](https://developers.cloudflare.com/cloudflare-one/networks/connectors/cloudflare-tunnel/) · [Tailscale documentation](https://tailscale.com/kb) · [Back to overview](../README.md)

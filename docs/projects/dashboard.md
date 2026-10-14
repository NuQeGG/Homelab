# Homelab dashboard

## Deployment

`Dashboard`, CT 111 on `NuQe1G`, hosts Homepage and Speedtest Tracker using Docker Compose. The documented application directory is `/opt/nuqe-dashboard`.

The dashboard brings together website links, media applications, Proxmox nodes and guests, Pi-hole statistics, internet speed results, and everyday links. The design uses a dark navy theme, with a clock and weather information.

## Monitoring

I have Proxmox CPU/RAM metrics and guest status working alongside the Pi-hole and Speedtest widgets. The Proxmox integration uses a dedicated monitoring account and a privilege-separated API token with read-only `PVEAuditor` access. I also supplied the Proxmox root CA for certificate trust.

Live measurements and service discovery are separate. Metrics update during use, but the guest cards were generated from an inventory at setup time. New, deleted, renamed, or moved guests require the saved mapping to be refreshed.

## An upgrade lesson

A Jellyfin upgrade left Homepage displaying an API error. Checks showed that the saved credential worked against the newer endpoints, while the old endpoints returned 404. Updating the Jellyfin widget version resolved the reported dashboard problem.

This was an integration compatibility issue, rather than evidence that Jellyfin itself was down or that its API key needed replacement.

## Limits

The native guest metrics provide a current operational view. They are not documented as a historical metrics database or an alerting system. An available dashboard also does not establish that its dependent applications are healthy end to end.

## Maintenance and data

Keep service URLs and API credentials in the private configuration. After changing the inventory, verify each node and guest mapping, then inspect the relevant widgets.

[Homepage Proxmox integration](https://gethomepage.dev/configs/proxmox/) · [Homepage Jellyfin widget](https://gethomepage.dev/widgets/services/jellyfin/) · [Back to overview](../../README.md)

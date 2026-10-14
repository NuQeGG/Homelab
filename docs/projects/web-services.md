# Web services

I host two websites on my own infrastructure. Both run in separate Debian LXC containers on `NuQe1G`, using Nginx and PHP. Cloudflare Tunnel provides the public access path through CT 101 on `NuQeGG`.

| Website | Guest | Documented application directory | Purpose |
| --- | ---: | --- | --- |
| [cv.nuqehosting.uk](https://cv.nuqehosting.uk/) | 108, `CVWeb` | `/var/www/cv` | Danish CV and a short overview of homelab projects |
| [pc.nuqehosting.uk](https://pc.nuqehosting.uk/) | 110, `PCWeb` | `/var/www/nuqe` | PC setup, settings, and social links |

## CV website

The CV uses a Linux desktop-inspired interface called `nuqeOS`, including a boot sequence, theme switching, and expandable folders for experience and projects. Its content remains in Danish.

The PHP page reads editable content from `content.json`. The existing admin panel is used to maintain the text and project entries. The detailed English documentation lives in this repository; the CV provides short descriptions with links to the relevant guides.

## PC website

The PC website presents setup information and social links in a separate interface. Its trident logo acts as a home button, with a loading animation based on supplied artwork. It has its own PHP admin interface and content arrangement.

The two sites do not share a single admin data file, so changes should target the correct guest and application directory.

## Hosting and maintenance

Nginx and PHP run directly in the website guests. I use Docker for other applications in the lab.

Before changing a template or admin implementation, preserve the current content and application files. For ordinary text updates, the admin panel provides the existing workflow.

After an update, check both the local web service and the public URL. A public failure can come from Nginx/PHP, application content, the tunnel route, DNS, or connectivity between the two nodes.

[Networking](../network-setup.md) · [Storage](../storage.md) · [Back to overview](../../README.md)

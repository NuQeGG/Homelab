# Proxmox Setup
<img width="749" height="893" alt="image" src="https://github.com/user-attachments/assets/8947fddc-5bc2-4456-99e6-c7cf44324543" />

## Overview

The homelab is currently built around Proxmox with multiple hosts for service separation and future scalability.

---

## Main Host

Primary virtualization node running media stack and heavier workloads.

### Workloads

* Docker containers
* Media automation
* Download stack

---

## Secondary Host

Used for web hosting and lightweight services.

### Workloads

* Docker containers
* Static websites
* Tailscale access

---

## Container Strategy

Most services are currently deployed inside containers for easy management and low overhead.

---

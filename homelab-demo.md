# Homelab Inventory

> Exported 3/16/2026, 7:42:26 PM — 14 devices

---

# proxmox-01

- **Type:** server
- **Status:** online
- **IP Address:** 10.0.1.10
- **System:** Dell OptiPlex 7080 Micro
- **OS:** Proxmox VE 8.2
- **CPU:** Intel Core i7-10700T / 8 cores
- **RAM:** 64GB DDR4 2933MHz
- **Location:** Network Closet - Shelf 2

## Storage

| Type / Device | Size | Notes |
|---------------|------|-------|
| Samsung 970 EVO Plus NVMe | 500GB | Boot drive |
| Samsung 980 Pro NVMe | 2TB | VM storage |
| WD Red Plus | 4TB | Backup storage |

## Running on this host

- **docker-vm** (vm) — 10.0.1.20
- **media-vm** (vm) — 10.0.1.21
- **pihole-lxc** (container) — 10.0.1.53
- **grafana-lxc** (container) — 10.0.1.30
- **homeassistant-lxc** (container) — 10.0.1.40

## Notes

Primary hypervisor. Runs all VMs and LXC containers.
Backups run nightly at 2:00 AM to NAS via PBS.

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: pxmx000001*

# docker-vm

- **Type:** vm
- **Status:** online
- **IP Address:** 10.0.1.20
- **System:** —
- **OS:** Ubuntu Server 24.04 LTS
- **CPU:** 4 vCPU
- **RAM:** 16GB
- **Location:** —
- **Host:** proxmox-01

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| Nginx Proxy Manager | 81 | Reverse proxy for all services | https://nginxproxymanager.com/ |
| Portainer | 9443 | Container management | https://www.portainer.io/ |
| Uptime Kuma | 3001 | Service monitoring | https://github.com/louislam/uptime-kuma |
| Vaultwarden | 8222 | Password manager | https://github.com/dani-garcia/vaultwarden |
| Homarr | 7575 | Dashboard | https://homarr.dev |
| Watchtower | — | Auto-update containers | https://containrrr.dev/watchtower/ |
| Dozzle | 9999 | Log viewer | https://dozzle.dev/ |
| Paperless-ngx | 8000 | Document management | https://docs.paperless-ngx.com/ |
| Nextcloud | 8080 | Cloud storage | https://nextcloud.com/ |

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: dkrvm00001 | ParentID: pxmx000001*

# media-vm

- **Type:** vm
- **Status:** online
- **IP Address:** 10.0.1.21
- **System:** —
- **OS:** Ubuntu Server 24.04 LTS
- **CPU:** 4 vCPU
- **RAM:** 8GB
- **Location:** —
- **Host:** proxmox-01

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| Plex | 32400 | Media server | https://www.plex.tv/ |
| Radarr | 7878 | Movie management | https://radarr.video/ |
| Sonarr | 8989 | TV show management | https://sonarr.tv/ |
| Prowlarr | 9696 | Indexer management | https://prowlarr.com/ |
| qBittorrent | 8080 | Torrent client via Gluetun VPN | — |
| Tautulli | 8181 | Plex monitoring | https://tautulli.com/ |
| Overseerr | 5055 | Media requests | https://overseerr.dev/ |

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: mdavm00001 | ParentID: pxmx000001*

# pihole-lxc

- **Type:** container
- **Status:** online
- **IP Address:** 10.0.1.53
- **System:** —
- **OS:** Debian 12
- **CPU:** 1 vCPU
- **RAM:** 512MB
- **Location:** —
- **Host:** proxmox-01

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| Pi-hole | 80 | DNS filtering & ad blocking | https://pi-hole.net/ |

## Notes

Primary DNS for the network. Backup DNS is Cloudflare 1.1.1.1.

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: pihole0001 | ParentID: pxmx000001*

# grafana-lxc

- **Type:** container
- **Status:** online
- **IP Address:** 10.0.1.30
- **System:** —
- **OS:** Debian 12
- **CPU:** 2 vCPU
- **RAM:** 2GB
- **Location:** —
- **Host:** proxmox-01

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| Grafana | 3000 | Dashboards & visualization | https://grafana.com/ |
| Prometheus | 9090 | Metrics collection | https://prometheus.io/ |
| Node Exporter | 9100 | Host metrics | https://github.com/prometheus/node_exporter |

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: grafna0001 | ParentID: pxmx000001*

# homeassistant-lxc

- **Type:** container
- **Status:** online
- **IP Address:** 10.0.1.40
- **System:** —
- **OS:** Debian 12
- **CPU:** 2 vCPU
- **RAM:** 4GB
- **Location:** —
- **Host:** proxmox-01

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| Home Assistant | 8123 | Smart home automation | https://www.home-assistant.io/ |
| Mosquitto | 1883 | MQTT broker | https://mosquitto.org/ |
| Z-Wave JS | 3000 | Z-Wave controller | https://zwave-js.github.io/zwave-js-ui/ |

## Notes

Controls 47 devices across Zigbee, Z-Wave, and WiFi.
ConBee II USB stick for Zigbee.
Zooz ZST39 for Z-Wave.

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: haoslxc001 | ParentID: pxmx000001*

# nas-01

- **Type:** storage
- **Status:** online
- **IP Address:** 10.0.1.50
- **System:** Synology DS920+
- **OS:** DSM 7.2
- **CPU:** Intel Celeron J4125 / 4 cores
- **RAM:** 8GB DDR4
- **Location:** Network Closet - Shelf 1

## Storage

| Type / Device | Size | Notes |
|---------------|------|-------|
| WD Red Plus CMR | 8TB x2 | SHR-1 Storage Pool |
| WD Red Plus CMR | 8TB x2 | SHR-1 Storage Pool |
| Samsung 970 EVO Plus NVMe | 500GB x2 | SSD Cache (R/W) |

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| SMB/NFS Shares | 445 | Network file shares | — |
| Synology Photos | — | Photo backup & management | https://www.synology.com/en-us/dsm/feature/photos |
| Hyper Backup | — | Offsite backup to Backblaze B2 | — |
| Tailscale | — | VPN access | https://tailscale.com/ |

## Notes

~22TB usable storage after SHR-1 parity.
UPS connected via USB for graceful shutdown.

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: trnas00001*

# pfsense-fw

- **Type:** network
- **Status:** online
- **IP Address:** 10.0.1.1
- **System:** Protectli Vault FW4B
- **OS:** pfSense CE 2.7.2
- **CPU:** Intel Celeron J3160 / 4 cores
- **RAM:** 8GB DDR3L
- **Location:** Network Closet - Shelf 3

## Storage

| Type / Device | Size | Notes |
|---------------|------|-------|
| mSATA SSD | 120GB | Boot / OS drive |

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| Firewall | — | Stateful packet filtering | https://www.pfsense.org/ |
| OpenVPN | 1194 | Remote access VPN | — |
| HAProxy | 443 | SSL termination & load balancing | — |
| pfBlockerNG | — | IP/DNS blocklists | — |

## Notes

ISP: Comcast 1 Gig
4 Intel NICs: WAN, LAN, IoT VLAN, Guest VLAN

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: pfsns00001*

# core-switch

- **Type:** network
- **Status:** online
- **IP Address:** 10.0.1.2
- **System:** TP-Link TL-SG1024DE
- **OS:** —
- **CPU:** —
- **RAM:** —
- **Location:** Network Closet - Shelf 3

## Notes

24-port managed gigabit switch
VLAN trunking to pfSense
VLAN 10: LAN, VLAN 20: IoT, VLAN 30: Guest

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: tplnk00001*

# unifi-ap

- **Type:** network
- **Status:** online
- **IP Address:** 10.0.1.3
- **System:** Ubiquiti UniFi U6-Pro
- **OS:** —
- **CPU:** —
- **RAM:** —
- **Location:** Living Room - Ceiling Mount

## Notes

Broadcasts 3 SSIDs: Home, IoT, Guest
Powered via PoE from core switch

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: ubiqap0001*

# ups-01

- **Type:** other
- **Status:** online
- **IP Address:** —
- **System:** APC Back-UPS Pro 1500VA (BR1500MS2)
- **OS:** —
- **CPU:** —
- **RAM:** —
- **Location:** Network Closet - Floor

## Notes

1500VA / 900W Pure Sine Wave
Connected via USB to NAS for graceful shutdown
Powers: Proxmox, NAS, pfSense, Switch
Runtime at load: ~18 minutes

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: cybrups001*

# rpi-node-01

- **Type:** server
- **Status:** online
- **IP Address:** 10.0.1.101
- **System:** Raspberry Pi 4 Model B 4GB
- **OS:** Raspberry Pi OS Lite (64-bit)
- **CPU:** Broadcom BCM2711 / 4 cores
- **RAM:** 4GB LPDDR4
- **Location:** Desk - Pi Cluster Stack

## Storage

| Type / Device | Size | Notes |
|---------------|------|-------|
| Samsung EVO Plus microSD | 64GB | Boot drive |

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| K3s | 6443 | Kubernetes control plane | https://k3s.io/ |
| Node Exporter | 9100 | Prometheus metrics | https://github.com/prometheus/node_exporter |

## Notes

K3s control plane node. Runs cluster services.
PoE powered via PoE+ HAT.

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: rpi4node01*

# rpi-node-02

- **Type:** server
- **Status:** online
- **IP Address:** 10.0.1.102
- **System:** Raspberry Pi 4 Model B 4GB
- **OS:** Raspberry Pi OS Lite (64-bit)
- **CPU:** Broadcom BCM2711 / 4 cores
- **RAM:** 4GB LPDDR4
- **Location:** Desk - Pi Cluster Stack

## Storage

| Type / Device | Size | Notes |
|---------------|------|-------|
| Samsung EVO Plus microSD | 64GB | Boot drive |

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| K3s | 6443 | Kubernetes worker node | https://k3s.io/ |
| Node Exporter | 9100 | Prometheus metrics | https://github.com/prometheus/node_exporter |

## Notes

K3s worker node. Handles workload scheduling.
PoE powered via PoE+ HAT.

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: rpi4node02*

# rpi-node-03

- **Type:** server
- **Status:** offline
- **IP Address:** 10.0.1.103
- **System:** Raspberry Pi 4 Model B 4GB
- **OS:** Raspberry Pi OS Lite (64-bit)
- **CPU:** Broadcom BCM2711 / 4 cores
- **RAM:** 4GB LPDDR4
- **Location:** Desk - Pi Cluster Stack

## Storage

| Type / Device | Size | Notes |
|---------------|------|-------|
| Samsung EVO Plus microSD | 64GB | Boot drive |

## Services

| Service | Port | Notes | URL |
|---------|------|-------|-----|
| K3s | 6443 | Kubernetes worker node | https://k3s.io/ |
| Node Exporter | 9100 | Prometheus metrics | https://github.com/prometheus/node_exporter |

## Notes

K3s worker node. Currently offline for maintenance.
Replacing microSD with USB SSD boot.

---
*Created: 2026-03-16T19:42:26.663Z | Updated: 2026-03-16T19:42:26.663Z | ID: rpi4node03*


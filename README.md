# jellyfin-setup
Self-hosted media server using Docker

# Homelab Media Server & Automation Stack

A containerized, self-hosted media server and automation infrastructure running on Proxmox, featuring integrated content discovery, monitoring, and security hardening through VPN encryption.

## 🎯 Project Overview

This project demonstrates proficiency in:
- **Virtualization & Hypervisors** — Proxmox for resource isolation and VM management
- **Infrastructure Automation** — Containerized microservices architecture
- **Systems Security** — VPN integration across all services
- **Observability & Monitoring** — Real-time system and service health tracking
- **CI/CD Principles** — Automated content workflows and dependency management

Built to understand enterprise infrastructure patterns applied to a personal lab environment.

---

## 🏗️ Architecture Overview
┌─────────────────────────────────────┐
│      Mini PC with Proxmox Host      │
│           (2TB Storage)             │
├─────────────────────────────────────┤
│         Docker Containers           │
│  ┌─────────────────────────────────┐│
│  │  Media Stack:                   ││
│  │  • Jellyfin (Media Server)      ││
│  │  • Jellyseerr (Request UI)      ││
│  │  • Radarr (Movie Automation)    ││
│  │  • Sonarr (TV Show Automation)  ││
│  │  • Prowlarr (Indexer Hub)       ││
│  │  • qBittorrent (Download Mgmt)  ││
│  │                                 ││
│  │  Infrastructure:                ││
│  │  • Beszel (Monitoring/Logs)     ││
│  │  • Media Node (Content Delivery)││
│  │  • VPN Client (All Traffic)     ││
│  └─────────────────────────────────┘│
└─────────────────────────────────────┘
│
↓
[ VPN Tunnel ]
│
↓
External Access
---

## 📦 Services & Components

### Media Server & Distribution
- **Jellyfin** — Open-source media server; streams movies, TV shows, music across devices
- **Jellyseerr** — Web UI for requesting media; integrates with Radarr/Sonarr for automatic procurement

### Content Automation (*arr Stack)
- **Radarr** — Automated movie discovery, downloading, and library management
- **Sonarr** — Automated TV show tracking, downloading, and episode management
- **Prowlarr** — Indexer aggregator/proxy; unified interface for torrent/usenet sources
- **qBittorrent** — Download client; handles torrent management across *arr services

### Monitoring & Infrastructure
- **Beszel** — Real-time system monitoring, logging, and observability
- **Media Node** — Dedicated service node for content processing and delivery
- **VPN Client** — All container traffic routed through VPN for privacy and security

---

## 🖥️ Hardware Specifications

| Component | Spec |
|-----------|------|
| **Device** | Mini PC |
| **Storage** | 2TB (upgraded) |
| **Hypervisor** | Proxmox |
| **Containerization** | Docker |

---

## 🚀 Deployment Architecture

### Infrastructure Decisions
1. **Proxmox** — Lightweight hypervisor for efficient resource allocation across multiple containers
2. **Docker Containerization** — Service isolation, easy scaling, reproducible deployments
3. **VPN Integration** — All egress traffic encrypted; privacy-first infrastructure
4. **Distributed Services** — Separate concerns (media, automation, monitoring, delivery)

### Network Flow
User Request → Jellyseerr (UI) → Radarr/Sonarr (Automation) → qBittorrent (Download)
↓
[ VPN Tunnel ]
↓
[ Indexers / Content Sources ]

Monitoring: Beszel → System Health → Alerts & Logging
---

## 📋 Setup & Deployment

### Prerequisites
- Proxmox installed and configured
- 2TB+ storage (media + container overhead)
- VPN account/credentials for client setup
- Docker & Docker Compose in VM(s)

### Key Configuration Steps

1. **Proxmox VM Setup**
   - Create VM(s) with sufficient CPU/RAM allocation
   - Configure storage pools for media directory

2. **VPN Configuration**
   - Install VPN client in container/host
   - Route container traffic through VPN tunnel
   - Verify leak protection (DNS, IPv4/IPv6)

3. **Service Deployment**
   ```bash
   docker-compose up -d
   4. Service Configuration  • Jellyfin: Add media libraries and user profiles
  • Radarr/Sonarr: Configure indexers (via Prowlarr), quality profiles, download paths
  • Jellyseerr: Link to Radarr/Sonarr, enable notifications
  • qBittorrent: Set download paths, connection limits, ratio enforcement

5. Monitoring Setup  • Beszel: Configure agents on media node(s)
  • Set up logging and alert thresholds


🔐 Security & Privacy Considerations

✅ Implemented:

• VPN encryption for all external traffic
• Container isolation via Proxmox
• No exposed ports (internal access via VPN)
• Service-to-service authentication where applicable
⚠️ Best Practices Applied:

• Regular updates for all containers and base images
• Least-privilege user accounts within containers
• Firewall rules for internal communication only
• Monitoring for suspicious activity (Beszel logs)

📊 Performance & Monitoring

Beszel Integration:

• Real-time CPU, RAM, disk I/O monitoring
• Container health checks
• Alerting for service failures
• Historical performance trending
Optimization Strategies:

• Proxmox resource limits to prevent resource starvation
• Container CPU/memory caps for stable performance
• Disk I/O tuning for media library scanning

💡 Key Learnings & Skills Demonstrated

✅ Virtualization — Proxmox hypervisor management, VM lifecycle
✅ Containerization — Docker orchestration, service dependencies, networking
✅ Automation — *arr stack workflows, intelligent content procurement
✅ Observability — Monitoring, logging, alerting, system health
✅ Security — VPN integration, encryption, network isolation
✅ Infrastructure as Code — Docker Compose for reproducible deployments
✅ Troubleshooting — Log analysis, service debugging, performance optimization


🔄 Operational Workflows

Adding New Media

1. User requests via Jellyseerr
2. Radarr/Sonarr detects request
3. Prowlarr finds indexers
4. qBittorrent downloads content
5. Sonarr/Radarr organizes library
6. Jellyfin automatically indexes new content
7. Beszel logs activity and performance
System Maintenance

• Weekly: Review Beszel logs for errors/warnings
• Monthly: Update container images
• As-needed: Adjust Radarr/Sonarr quality profiles based on content availability

📈 Future Enhancements

• [ ] High availability setup (multi-node failover)
• [ ] Advanced monitoring dashboards (Grafana integration)
• [ ] Automated backup/disaster recovery strategy
• [ ] API integrations for additional indexers
• [ ] Performance tuning for 4K transcoding
• [ ] User authentication and permission layers

📚 Resources & References

• Jellyfin Documentation
• Proxmox Documentation
• Radarr/Sonarr Wiki
• Prowlarr Setup Guide
• Beszel Documentation
• Docker Compose Reference
• Setup Guide Reference

📝 License

This project is provided as-is for educational and personal use.


Built by: Eric Newell
Last Updated: February 2026
Questions? Open an issue or reach out.

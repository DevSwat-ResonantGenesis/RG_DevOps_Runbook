# RG DevOps Runbook

> **Internal documentation for the [ResonantGenesis](https://dev-swat.com) platform** — infrastructure, deployment, and operational guides.

[![Status: Production](https://img.shields.io/badge/Status-Production-brightgreen.svg)]()
[![Containers: 37](https://img.shields.io/badge/Containers-37-blue.svg)]()
[![Repos: 57](https://img.shields.io/badge/Repos-57-purple.svg)]()
[![Frontend: 17 Micro-Apps](https://img.shields.io/badge/Frontend-17%20Micro--Apps-orange.svg)]()
[![License: RG Source Available](https://img.shields.io/badge/License-RG%20Source%20Available-blue.svg)](LICENSE.txt)

Complete infrastructure documentation, deployment procedures, service catalog, database topology, and operational guides for the ResonantGenesis platform.

## Documents

| Document | Audience | Description |
|----------|----------|-------------|
| [SERVICE_CATALOG.md](SERVICE_CATALOG.md) | DevOps + Dev | All 37 containers — 100% standalone, zero monolith |
| [INFRASTRUCTURE.md](INFRASTRUCTURE.md) | DevOps | Server specs, Nginx, Docker, networking, SSL, firewall |
| [DATABASE.md](DATABASE.md) | DevOps + Dev | Database topology, connection strings, managed vs local DBs |
| [REPOSITORIES.md](REPOSITORIES.md) | Dev | All 57 GitHub repos — backend + frontend micro-apps |
| [API_CATALOG.md](API_CATALOG.md) | Dev | Complete backend API route inventory + frontend coverage map |
| [DEPLOYMENT.md](DEPLOYMENT.md) | DevOps | Step-by-step deploy procedures for every service type |
| [GATEWAY_ROUTES.md](GATEWAY_ROUTES.md) | Dev | Complete gateway proxy routing map |
| [VOLUME_MOUNTS.md](VOLUME_MOUNTS.md) | DevOps | Shared modules — rg_llm, rg_tool_registry volume mounts |
| [TROUBLESHOOTING.md](TROUBLESHOOTING.md) | DevOps | Common issues, debugging, log access, health checks |

## Quick Reference

- **Server**: `134.199.221.149` (DigitalOcean droplet, Ubuntu 24.04, 4 vCPU, 8GB RAM, 232GB disk)
- **SSH**: `ssh deploy@134.199.221.149` or `ssh deploy@dev-swat.com`
- **Domain**: `dev-swat.com` (Cloudflare DNS → DigitalOcean)
- **Nginx**: port 80/443 → gateway at `localhost:8001`
- **Gateway**: port 8001 → all backend services
- **Docker Compose**: `/home/deploy/genesis2026_production_backend/docker-compose.unified.yml`
- **Env file**: `/home/deploy/genesis2026_production_backend/.env.production`

## Architecture Overview

```
Internet
  │
  ▼
Cloudflare DNS (dev-swat.com)
  │
  ▼
DigitalOcean Droplet (134.199.221.149)
  │
  ├── Nginx (port 80/443, SSL termination)
  │     ├── / → /var/www/frontend/ (static React build)
  │     ├── /api/v1/* → gateway:8001
  │     ├── /ws/* → gateway:8001 (WebSocket upgrade)
  │     └── /resonant-chat/* → gateway:8001
  │
  ├── Gateway (port 8001 external, 8000 internal)
  │     ├── All 36 services (build from /home/deploy/RG_*)
  │     └── Shared modules (rg_llm, rg_tool_registry, platform_tools via volume mounts)
  │
  ├── PostgreSQL (DigitalOcean Managed — external)
  │     ├── resonant-db (main — 15 databases)
  │     └── ml-registry-db (ML service)
  │
  ├── Redis (shared_redis container, port 6379)
  │
  └── Frontend
        ├── Production: /var/www/frontend/ (monolith build)
        └── Next-gen: 17 RGF_* micro-apps (Module Federation)
```

---

**Organization**: [DevSwat-ResonantGenesis](https://github.com/DevSwat-ResonantGenesis)
**Platform**: [dev-swat.com](https://dev-swat.com)

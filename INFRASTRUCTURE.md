# Infrastructure

> Server specifications, networking, SSL, Docker setup, and system configuration.

## Server

| Property | Value |
|----------|-------|
| **Provider** | DigitalOcean |
| **Type** | Droplet |
| **IP** | `134.199.221.149` |
| **Domain** | `dev-swat.com` |
| **OS** | Ubuntu 24.04.3 LTS |
| **CPU** | 4 vCPU |
| **RAM** | 8 GB |
| **Disk** | 232 GB (41% used as of 2026-03-20) |
| **SSH User** | `deploy` |
| **SSH Access** | `ssh deploy@134.199.221.149` or `ssh deploy@dev-swat.com` |

## DNS

- **Registrar**: Cloudflare
- **Records**: `dev-swat.com` → `134.199.221.149` (A record)
- **Proxy**: Cloudflare proxy enabled (orange cloud)

## Nginx

- **Config**: `/etc/nginx/sites-enabled/dev-swat.com`
- **SSL**: Let's Encrypt / Cloudflare (terminated at Cloudflare + Nginx)
- **Ports**: 80 (redirect to 443), 443 (HTTPS)

### Key Nginx Locations

```
/                          → /var/www/frontend/ (static React build)
/api/v1/*                  → proxy_pass http://localhost:8001 (gateway)
/ws/*                      → proxy_pass http://localhost:8001 (WebSocket upgrade)
/resonant-chat/*           → proxy_pass http://localhost:8001
/state-physics/*           → proxy_pass http://localhost:8001
/hash-sphere/*             → proxy_pass http://localhost:8001
/crypto/*                  → proxy_pass http://localhost:8001
/agent-engine/*            → proxy_pass http://localhost:8001
/workflow/*                → proxy_pass http://localhost:8001
/marketplace/*             → proxy_pass http://localhost:8001
/public/*                  → proxy_pass http://localhost:8001
/agents/*                  → proxy_pass http://localhost:8001
/blockchain/*              → proxy_pass http://localhost:8001
/code/*                    → proxy_pass http://localhost:8001
/ml/*                      → proxy_pass http://localhost:8001
/downloads/*               → /var/www/downloads/ (IDE binaries)
```

### Critical Nginx Settings for SSE

```nginx
location ^~ /api/v1/ {
    proxy_http_version 1.1;          # MUST be 1.1 for SSE/chunked
    proxy_set_header Connection "";   # Required for keep-alive
    proxy_buffering off;              # Required for streaming
    proxy_cache off;
    proxy_read_timeout 300s;
    proxy_send_timeout 300s;
    proxy_pass http://localhost:8001;
}
```

> **WARNING**: If `proxy_http_version` is not 1.1, SSE streaming (IDE completions, agentic chat) will fail silently — responses will be truncated.

## Docker

- **Version**: Docker Compose v2 (Compose plugin)
- **Compose file**: `/home/deploy/genesis2026_production_backend/docker-compose.unified.yml`
- **Env file**: `/home/deploy/genesis2026_production_backend/.env.production`
- **Network**: `app-network` (bridge) — all containers communicate via container names
- **Total containers**: 37 (as of 2026-03-20)

### Docker Commands

```bash
# View all running containers
sudo docker ps --format 'table {{.Names}}\t{{.Status}}\t{{.Ports}}'

# View logs for a service
sudo docker logs -f --tail 100 <container_name>

# Restart a service
sudo docker compose -f docker-compose.unified.yml restart <service_name>

# Rebuild and restart a service
sudo docker compose -f docker-compose.unified.yml build <service_name>
sudo docker compose -f docker-compose.unified.yml up -d <service_name>

# Shell into a container
sudo docker exec -it <container_name> /bin/bash

# View resource usage
sudo docker stats --no-stream
```

## Directory Structure on Server

```
/home/deploy/
├── genesis2026_production_backend/   # Monolith repo (GitHub: louienemesh/genesis2026_production_backend_2)
│   ├── docker-compose.unified.yml    # Main compose file for ALL services
│   ├── .env.production               # Environment variables (secrets)
│   ├── gateway/                      # API gateway
│   ├── auth_service/                 # Authentication
│   ├── chat_service/                 # Resonant Chat + IDE completions
│   ├── memory_service/               # Memory/Hash Sphere
│   ├── agent_engine_service/         # Agent planner/executor
│   ├── user_service/                 # User profiles
│   ├── billing_service/              # Stripe billing
│   ├── cognitive_service/            # Cognitive pipelines
│   ├── workflow_service/             # Workflow orchestration
│   ├── ml_service/                   # ML registry
│   ├── storage_service/              # File storage
│   ├── ed_service/                   # Education
│   ├── marketplace_service/          # Marketplace
│   ├── notification_service/         # Notifications
│   ├── blockchain_service/           # Blockchain identity
│   ├── crypto_service/               # Cryptography
│   ├── llm_service/                  # Legacy LLM (being replaced)
│   ├── build_service/                # Build proxy
│   ├── code_execution_service/       # Code execution
│   ├── sandbox_runner_service/       # Sandbox runner
│   ├── v8_api_service/               # V8 JS execution
│   ├── openclaw_service/             # Legal docs
│   ├── discord_bridge/               # Discord bot
│   └── node/                         # Blockchain node
│
├── RG_Registered_Users_Agentic_Chat/ # Standalone (DevSwat GitHub)
├── RG_Public-Guest-Agentic_Chat/     # Standalone (DevSwat GitHub)
├── RG_AST_analysis/                  # Standalone (DevSwat GitHub)
├── RG_Internal_Invarients_SIM/       # Standalone (DevSwat GitHub)
├── RG_Users_Invarients_SIM/          # Standalone (DevSwat GitHub)
├── RG_IDE_Platform/                  # Standalone (DevSwat GitHub)
├── RG_Rabbit/                        # Standalone (DevSwat GitHub)
├── RG_UnifiedLLMClient/              # Shared module (volume-mounted)
├── RG_Unified_Tool_Registry/         # Shared module (volume-mounted)
│
├── genesis2026_frontend/             # Frontend (GitHub: louienemesh)
│   └── (old deployment, may not be current)
├── genesis2026_frontend_production_2/# Frontend working dir (builds from GitHub)
│
└── .ssh/
    ├── config                        # SSH config with github-devswat alias
    └── github_devswat_deploy_key     # Deploy key for DevSwat-ResonantGenesis org
```

## SSH Configuration (Server)

```
# /home/deploy/.ssh/config
Host github-devswat
    HostName github.com
    User git
    IdentityFile ~/.ssh/github_devswat_deploy_key
    IdentitiesOnly yes
```

This allows the server to clone from DevSwat-ResonantGenesis GitHub repos using:
```bash
git clone git@github-devswat:DevSwat-ResonantGenesis/<repo>.git
```

## Firewall

Only these ports are open:
- **22** — SSH
- **80** — HTTP (redirects to 443)
- **443** — HTTPS
- **8081** — Blockchain node (direct access)

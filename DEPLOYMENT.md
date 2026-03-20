# Deployment Procedures

> Step-by-step deploy guides for every service type.

## 1. Deploy a Standalone Service (DevSwat repos)

These are services cloned from `DevSwat-ResonantGenesis` GitHub into `/home/deploy/RG_*`.

```bash
# SSH into server
ssh deploy@134.199.221.149

# Pull latest code
cd /home/deploy/<RG_REPO_NAME>
git pull origin main

# Rebuild and restart
cd /home/deploy/genesis2026_production_backend
sudo docker compose -f docker-compose.unified.yml build <service_name>
sudo docker compose -f docker-compose.unified.yml up -d <service_name>

# Verify health
sudo docker ps --format '{{.Names}} {{.Status}}' | grep <service_name>
sudo docker logs -f --tail 50 <container_name>
```

### Service Name Mapping

| Repo | docker-compose service | Container name |
|------|----------------------|----------------|
| `RG_Registered_Users_Agentic_Chat` | `rg_agentic_chat` | `rg_agentic_chat` |
| `RG_Public-Guest-Agentic_Chat` | `rg_public_guest_chat` | `rg_public_guest_chat` |
| `RG_AST_analysis` | `rg_ast_analysis` | `rg_ast_analysis` |
| `RG_Internal_Invarients_SIM` | `rg_internal_invarients_sim` | `rg_internal_invarients_sim` |
| `RG_Users_Invarients_SIM` | `rg_users_invarients_sim` | `rg_users_invarients_sim` |
| `RG_IDE_Platform` | `ide_platform_service` | `ide_platform_service` |
| `RG_Axtention_IDE` | `ide_agent_service` | `ide_agent_service` |
| `RG_Rabbit` (api) | `rabbit_api_service` | `rabbit_api_service` |

## 2. Deploy a Monolith Service

These build from `./service_name` inside `genesis2026_production_backend`.

```bash
ssh deploy@134.199.221.149
cd /home/deploy/genesis2026_production_backend

# Pull latest
git fetch origin && git reset --hard origin/main

# Rebuild specific service
sudo docker compose -f docker-compose.unified.yml build <service_name>
sudo docker compose -f docker-compose.unified.yml up -d <service_name>

# Verify
sudo docker ps --format '{{.Names}} {{.Status}}' | grep <service_name>
```

> **WARNING**: `git pull` on the server may overwrite manual docker-compose changes (like the `rg_agentic_chat` service block if it's not committed to git). Always check the diff before pulling.

## 3. Deploy Shared Modules (rg_llm, rg_tool_registry)

These are volume-mounted — no container rebuild needed, just restart consumers.

```bash
ssh deploy@134.199.221.149

# Update rg_llm
cd /home/deploy/RG_UnifiedLLMClient && git pull origin main

# Restart all containers that use it
cd /home/deploy/genesis2026_production_backend
sudo docker compose -f docker-compose.unified.yml restart agent_engine_service chat_service rg_agentic_chat rg_public_guest_chat

# Update rg_tool_registry
cd /home/deploy/RG_Unified_Tool_Registry && git pull origin main
sudo docker compose -f docker-compose.unified.yml restart agent_engine_service rg_agentic_chat
```

## 4. Deploy Frontend

```bash
# LOCAL: push to GitHub
cd /Users/louie/CascadeProjects/genesis2026_frontend
git push github main    # MUST use 'github' remote, NOT 'origin'

# SERVER:
ssh deploy@134.199.221.149
cd /home/deploy/genesis2026_frontend_production_2
git fetch origin && git reset --hard origin/main
npm run build
sudo rsync -a --delete dist/ /var/www/frontend/
sudo nginx -s reload
```

> **Critical**: The local `origin` remote points to a bare repo on the server, NOT the working directory. Always push to the `github` remote so the server can pull from GitHub.

## 5. Deploy Everything (Full Redeploy)

```bash
ssh deploy@134.199.221.149
cd /home/deploy/genesis2026_production_backend

# Pull all standalone repos
for repo in RG_Registered_Users_Agentic_Chat RG_Public-Guest-Agentic_Chat RG_AST_analysis RG_Internal_Invarients_SIM RG_Users_Invarients_SIM RG_IDE_Platform RG_Axtention_IDE RG_Rabbit RG_UnifiedLLMClient RG_Unified_Tool_Registry; do
  echo "Pulling $repo..."
  cd /home/deploy/$repo && git pull origin main
done

# Pull monolith
cd /home/deploy/genesis2026_production_backend
git fetch origin && git reset --hard origin/main

# Rebuild everything
sudo docker compose -f docker-compose.unified.yml build
sudo docker compose -f docker-compose.unified.yml up -d

# Verify all healthy
sudo docker ps --format 'table {{.Names}}\t{{.Status}}' | sort
```

## 6. Database Migrations

```bash
# Auth service
sudo docker exec auth_service alembic upgrade head

# Chat service
sudo docker exec chat_service alembic upgrade head

# Rabbit API
sudo docker exec rabbit_api_service alembic upgrade head

# Agent engine
sudo docker exec agent_engine_service alembic upgrade head
```

## 7. Rollback

```bash
# Rollback a standalone service to previous commit
cd /home/deploy/<RG_REPO>
git log --oneline -5          # Find the commit to rollback to
git reset --hard <commit_sha>

# Rebuild
cd /home/deploy/genesis2026_production_backend
sudo docker compose -f docker-compose.unified.yml build <service_name>
sudo docker compose -f docker-compose.unified.yml up -d <service_name>
```

## 8. Add a New Standalone Service

When extracting a new service from the monolith:

1. Create the GitHub repo on DevSwat-ResonantGenesis
2. Clone locally, copy service files, add README/LICENSE/.gitignore
3. Push to GitHub
4. Clone on server: `cd /home/deploy && git clone git@github-devswat:DevSwat-ResonantGenesis/<repo>.git`
5. Update `docker-compose.unified.yml` build context from `./old_name` to `/home/deploy/<repo>`
6. Rebuild: `sudo docker compose -f docker-compose.unified.yml build <service> && sudo docker compose -f docker-compose.unified.yml up -d <service>`
7. Verify health
8. Delete old directory from monolith (local + server)
9. Commit docker-compose change to git

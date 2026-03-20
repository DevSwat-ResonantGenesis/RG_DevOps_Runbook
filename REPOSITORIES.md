# Repositories

> All GitHub repos across the DevSwat-ResonantGenesis org and louienemesh account (as of 2026-03-20).
>
> **Monolith fully decomposed** — ALL 37 containers now build from standalone `/home/deploy/RG_*` repos. Zero monolith build contexts remain.

## DevSwat-ResonantGenesis Organization (40 repos)

### Core Platform Services (8 repos) — Final extraction, 2026-03-20

| Repo | Container | Port | Server Path |
|------|-----------|------|-------------|
| [`RG_Gateway`](https://github.com/DevSwat-ResonantGenesis/RG_Gateway) | `gateway` | 8001→8000 | `/home/deploy/RG_Gateway` |
| [`RG_Auth`](https://github.com/DevSwat-ResonantGenesis/RG_Auth) | `auth_service` | 8000 | `/home/deploy/RG_Auth` |
| [`RG_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Chat) | `chat_service` | 8000 | `/home/deploy/RG_Chat` |
| [`RG_Memory`](https://github.com/DevSwat-ResonantGenesis/RG_Memory) | `memory_service` | 8000 | `/home/deploy/RG_Memory` |
| [`RG_Agent_Engine`](https://github.com/DevSwat-ResonantGenesis/RG_Agent_Engine) | `agent_engine_service` | 8000 | `/home/deploy/RG_Agent_Engine` |
| [`RG_User_Service`](https://github.com/DevSwat-ResonantGenesis/RG_User_Service) | `user_service` | 8000 | `/home/deploy/RG_User_Service` |
| [`RG_Billing`](https://github.com/DevSwat-ResonantGenesis/RG_Billing) | `billing_service` | 8000 | `/home/deploy/RG_Billing` |
| [`RG_LLM_Service`](https://github.com/DevSwat-ResonantGenesis/RG_LLM_Service) | `llm_service` | 8000 | `/home/deploy/RG_LLM_Service` |

### Chat & AI Services (2 repos)

| Repo | Container | Port | Server Path |
|------|-----------|------|-------------|
| [`RG_Registered_Users_Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Registered_Users_Agentic_Chat) | `rg_agentic_chat` | 8000 | `/home/deploy/RG_Registered_Users_Agentic_Chat` |
| [`RG_Public-Guest-Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Public-Guest-Agentic_Chat) | `rg_public_guest_chat` | 8010 | `/home/deploy/RG_Public-Guest-Agentic_Chat` |

### Analysis & Governance (2 repos)

| Repo | Container | Port | Server Path |
|------|-----------|------|-------------|
| [`RG_AST_analysis`](https://github.com/DevSwat-ResonantGenesis/RG_AST_analysis) | `rg_ast_analysis` | 8000 | `/home/deploy/RG_AST_analysis` |
| [`RG_Internal_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Internal_Invarients_SIM) | `rg_internal_invarients_sim` | 8093 | `/home/deploy/RG_Internal_Invarients_SIM` |
| [`RG_Users_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Users_Invarients_SIM) | `rg_users_invarients_sim` | 8091 | `/home/deploy/RG_Users_Invarients_SIM` |

### IDE & Platform (1 repo)

| Repo | Container | Port | Server Path |
|------|-----------|------|-------------|
| [`RG_IDE_Platform`](https://github.com/DevSwat-ResonantGenesis/RG_IDE_Platform) | `ide_service` | 8080 | `/home/deploy/RG_IDE_Platform` |

### Rabbit Community Platform (1 repo, 5 containers)

| Repo | Container | Port | Server Path |
|------|-----------|------|-------------|
| [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) | `rabbit_api_service` + 4 stubs | 8000 | `/home/deploy/RG_Rabbit` |

### Business & Data Services (10 repos)

| Repo | Container | Port | Server Path |
|------|-----------|------|-------------|
| [`RG_Cognitive`](https://github.com/DevSwat-ResonantGenesis/RG_Cognitive) | `cognitive_service` | 8000 | `/home/deploy/RG_Cognitive` |
| [`RG_Workflow`](https://github.com/DevSwat-ResonantGenesis/RG_Workflow) | `workflow_service` | 8000 | `/home/deploy/RG_Workflow` |
| [`RG_ML_Service`](https://github.com/DevSwat-ResonantGenesis/RG_ML_Service) | `ml_service` | 8000 | `/home/deploy/RG_ML_Service` |
| [`RG_Storage`](https://github.com/DevSwat-ResonantGenesis/RG_Storage) | `storage_service` | 8000 | `/home/deploy/RG_Storage` |
| [`RG_Ed_Service`](https://github.com/DevSwat-ResonantGenesis/RG_Ed_Service) | `ed_service` | 8000 | `/home/deploy/RG_Ed_Service` |
| [`RG_Marketplace`](https://github.com/DevSwat-ResonantGenesis/RG_Marketplace) | `marketplace_service` | 8000 | `/home/deploy/RG_Marketplace` |
| [`RG_Notifications`](https://github.com/DevSwat-ResonantGenesis/RG_Notifications) | `notification_service` | 8000 | `/home/deploy/RG_Notifications` |
| [`RG_Crypto`](https://github.com/DevSwat-ResonantGenesis/RG_Crypto) | `crypto_service` | 8000 | `/home/deploy/RG_Crypto` |
| [`RG_User_Memory`](https://github.com/DevSwat-ResonantGenesis/RG_User_Memory) | `user_memory_service` | 8094 | `/home/deploy/RG_User_Memory` |
| [`RG_Blockchain`](https://github.com/DevSwat-ResonantGenesis/RG_Blockchain) | `blockchain_service` | 8000 | `/home/deploy/RG_Blockchain` |

### Infrastructure & Utility Services (7 repos)

| Repo | Container | Port | Server Path |
|------|-----------|------|-------------|
| [`RG_Blockchain_Node`](https://github.com/DevSwat-ResonantGenesis/RG_Blockchain_Node) | `blockchain_node` | 8081 | `/home/deploy/RG_Blockchain_Node` |
| [`RG_Build_Service`](https://github.com/DevSwat-ResonantGenesis/RG_Build_Service) | `build_service` | 8003 | `/home/deploy/RG_Build_Service` |
| [`RG_Code_Execution`](https://github.com/DevSwat-ResonantGenesis/RG_Code_Execution) | `code_execution_service` | 8002 | `/home/deploy/RG_Code_Execution` |
| [`RG_Sandbox_Runner`](https://github.com/DevSwat-ResonantGenesis/RG_Sandbox_Runner) | `sandbox_runner_service` | 9001 | `/home/deploy/RG_Sandbox_Runner` |
| [`RG_V8_API`](https://github.com/DevSwat-ResonantGenesis/RG_V8_API) | `v8_api_service` | 8080 | `/home/deploy/RG_V8_API` |
| [`RG_OpenClaw`](https://github.com/DevSwat-ResonantGenesis/RG_OpenClaw) | `openclaw_service` | 8000 | `/home/deploy/RG_OpenClaw` |
| [`RG_Discord_Bridge`](https://github.com/DevSwat-ResonantGenesis/RG_Discord_Bridge) | `discord_bridge` | — | `/home/deploy/RG_Discord_Bridge` |

### Shared Modules (3 repos, volume-mounted)

| Repo | Volume Mount | Server Path |
|------|-------------|-------------|
| [`RG_UnifiedLLMClient`](https://github.com/DevSwat-ResonantGenesis/RG_UnifiedLLMClient) | `/app/rg_llm:ro` | `/home/deploy/RG_UnifiedLLMClient` |
| [`RG_Unified_Tool_Registry-Observability_Module`](https://github.com/DevSwat-ResonantGenesis/RG_Unified_Tool_Registry-Observability_Module) | `/app/rg_tool_registry:ro` | `/home/deploy/RG_Unified_Tool_Registry` |
| [`RG_Platform_Tools`](https://github.com/DevSwat-ResonantGenesis/RG_Platform_Tools) | `/app/platform_tools:ro` | `/home/deploy/RG_Platform_Tools` |

### Non-Service Repos (6 repos)

| Repo | Type |
|------|------|
| [`RG_IDE`](https://github.com/DevSwat-ResonantGenesis/RG_IDE) | VS Code fork (Electron desktop app) |
| [`RG_Axtention_IDE`](https://github.com/DevSwat-ResonantGenesis/RG_Axtention_IDE) | VS Code extension (source of truth) |
| [`RG_Platform_Orchestration`](https://github.com/DevSwat-ResonantGenesis/RG_Platform_Orchestration) | docker-compose, Nginx, deploy scripts, infrastructure config |
| [`RG_DevOps_Runbook`](https://github.com/DevSwat-ResonantGenesis/RG_DevOps_Runbook) | This repo — infrastructure documentation |
| [`.github`](https://github.com/DevSwat-ResonantGenesis/.github) | Org profile README |

## louienemesh Account (2 repos — legacy)

| Repo | Purpose | Server Path |
|------|---------|-------------|
| [`genesis2026_production_backend_2`](https://github.com/louienemesh/genesis2026_production_backend_2) | **DEPRECATED** — all services extracted to RG_* repos. Kept for git history. | `/home/deploy/genesis2026_production_backend` (orchestration only) |
| [`genesis2026_frontend_production_2`](https://github.com/louienemesh/genesis2026_frontend_production_2) | React frontend (Vite build) | `/home/deploy/genesis2026_frontend_production_2` |

## Monolith Status: FULLY DECOMPOSED

**Zero monolith build contexts remain.** All 37 containers build from `/home/deploy/RG_*` paths. The old `genesis2026_production_backend` directory on the server now only holds `docker-compose.unified.yml` and `.env.production` as orchestration files. The canonical orchestration repo is `RG_Platform_Orchestration`.

## Source of Truth Rules

1. **RG_Axtention_IDE** is the source of truth for the VS Code extension. Changes go there first, then sync to `RG_IDE/extensions/resonant-ai/`.
2. **All RG_* repos** are the source of truth for their services. Never edit service code elsewhere.
3. **RG_Platform_Orchestration** is the source of truth for docker-compose.unified.yml, nginx config, and deploy scripts.
4. **Frontend**: Always `git push github main` (not origin) so the server can pull from GitHub.

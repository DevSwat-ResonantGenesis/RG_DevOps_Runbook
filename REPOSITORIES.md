# Repositories

> All GitHub repos across the DevSwat-ResonantGenesis org and louienemesh account (as of 2026-03-20).

## DevSwat-ResonantGenesis Organization (29 repos)

### Standalone Deployed Services — Original Extractions (8 repos)

| Repo | Container | Port | Server Path |
|------|-----------|------|-------------|
| [`RG_Registered_Users_Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Registered_Users_Agentic_Chat) | `rg_agentic_chat` | 8000 | `/home/deploy/RG_Registered_Users_Agentic_Chat` |
| [`RG_Public-Guest-Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Public-Guest-Agentic_Chat) | `rg_public_guest_chat` | 8010 | `/home/deploy/RG_Public-Guest-Agentic_Chat` |
| [`RG_AST_analysis`](https://github.com/DevSwat-ResonantGenesis/RG_AST_analysis) | `rg_ast_analysis` | 8000 | `/home/deploy/RG_AST_analysis` |
| [`RG_Internal_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Internal_Invarients_SIM) | `rg_internal_invarients_sim` | 8093 | `/home/deploy/RG_Internal_Invarients_SIM` |
| [`RG_Users_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Users_Invarients_SIM) | `rg_users_invarients_sim` | 8091 | `/home/deploy/RG_Users_Invarients_SIM` |
| [`RG_IDE_Platform`](https://github.com/DevSwat-ResonantGenesis/RG_IDE_Platform) | `ide_service` | 8080 | `/home/deploy/RG_IDE_Platform` |
| [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) | `rabbit_api_service` + 4 stubs | 8000 | `/home/deploy/RG_Rabbit` |
| [`RG_Axtention_IDE`](https://github.com/DevSwat-ResonantGenesis/RG_Axtention_IDE) | N/A (VS Code extension) | N/A | N/A (client-side) |

### Standalone Deployed Services — Batch Extraction (16 repos, 2026-03-20)

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
| [`RG_Build_Service`](https://github.com/DevSwat-ResonantGenesis/RG_Build_Service) | `build_service` | 8003 | `/home/deploy/RG_Build_Service` |
| [`RG_Code_Execution`](https://github.com/DevSwat-ResonantGenesis/RG_Code_Execution) | `code_execution_service` | 8002 | `/home/deploy/RG_Code_Execution` |
| [`RG_Sandbox_Runner`](https://github.com/DevSwat-ResonantGenesis/RG_Sandbox_Runner) | `sandbox_runner_service` | 9001 | `/home/deploy/RG_Sandbox_Runner` |
| [`RG_V8_API`](https://github.com/DevSwat-ResonantGenesis/RG_V8_API) | `v8_api_service` | 8080 | `/home/deploy/RG_V8_API` |
| [`RG_OpenClaw`](https://github.com/DevSwat-ResonantGenesis/RG_OpenClaw) | `openclaw_service` | 8000 | `/home/deploy/RG_OpenClaw` |
| [`RG_Discord_Bridge`](https://github.com/DevSwat-ResonantGenesis/RG_Discord_Bridge) | `discord_bridge` | — | `/home/deploy/RG_Discord_Bridge` |

### Shared Modules (2 repos)

| Repo | Volume Mount | Server Path |
|------|-------------|-------------|
| [`RG_UnifiedLLMClient`](https://github.com/DevSwat-ResonantGenesis/RG_UnifiedLLMClient) | `/app/rg_llm:ro` | `/home/deploy/RG_UnifiedLLMClient` |
| [`RG_Unified_Tool_Registry-Observability_Module`](https://github.com/DevSwat-ResonantGenesis/RG_Unified_Tool_Registry-Observability_Module) | `/app/rg_tool_registry:ro` | `/home/deploy/RG_Unified_Tool_Registry` |

### Non-Service Repos (3 repos)

| Repo | Type |
|------|------|
| [`RG_IDE`](https://github.com/DevSwat-ResonantGenesis/RG_IDE) | VS Code fork (Electron desktop app). Source of truth for extension is `RG_Axtention_IDE`. |
| [`.github`](https://github.com/DevSwat-ResonantGenesis/.github) | Org profile README |
| [`RG_DevOps_Runbook`](https://github.com/DevSwat-ResonantGenesis/RG_DevOps_Runbook) | This repo — infrastructure documentation |

## louienemesh Account (2 repos)

| Repo | Purpose | Server Path |
|------|---------|-------------|
| [`genesis2026_production_backend_2`](https://github.com/louienemesh/genesis2026_production_backend_2) | Monolith backbone — 9 core services + docker-compose | `/home/deploy/genesis2026_production_backend` |
| [`genesis2026_frontend_production_2`](https://github.com/louienemesh/genesis2026_frontend_production_2) | React frontend (Vite build) | `/home/deploy/genesis2026_frontend_production_2` |

## What Remains in the Monolith

Only **9 core/coupled services** still build from `genesis2026_production_backend` (relative `./` paths):

`gateway`, `auth_service`, `chat_service`, `memory_service`, `agent_engine_service`, `user_service`, `billing_service`, `llm_service`, `node` (blockchain_node)

Plus support directories: `shared/`, `shared_libs/`, `platform_tools/`, `agents/`, `config/`, `contracts/`, `deploy/`, `docker/`, `governance/`, `nginx/`, `scripts/`, `cascade_control_plane/`, `performance_tests/`, `rg_tool_registry/`

## Source of Truth Rules

1. **RG_Axtention_IDE** is the source of truth for the VS Code extension. Changes go there first, then sync to `RG_IDE/extensions/resonant-ai/`.
2. **Standalone repos** (RG_*) are the source of truth for their services. Never edit service code in the monolith.
3. **docker-compose.unified.yml** lives in the monolith but references external build contexts for standalone services.
4. **Frontend**: Always `git push github main` (not origin) so the server can pull from GitHub.

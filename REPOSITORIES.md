# Repositories

> All GitHub repos across the DevSwat-ResonantGenesis org and louienemesh account.

## DevSwat-ResonantGenesis Organization (13 repos)

### Standalone Deployed Services (8 repos)

| Repo | Visibility | Container | Port | Server Path |
|------|-----------|-----------|------|-------------|
| [`RG_Registered_Users_Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Registered_Users_Agentic_Chat) | Private | `rg_agentic_chat` | 8000 | `/home/deploy/RG_Registered_Users_Agentic_Chat` |
| [`RG_Public-Guest-Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Public-Guest-Agentic_Chat) | Public | `rg_public_guest_chat` | 8010 | `/home/deploy/RG_Public-Guest-Agentic_Chat` |
| [`RG_AST_analysis`](https://github.com/DevSwat-ResonantGenesis/RG_AST_analysis) | Private | `rg_ast_analysis` | 8000 | `/home/deploy/RG_AST_analysis` |
| [`RG_Internal_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Internal_Invarients_SIM) | Private | `rg_internal_invarients_sim` | 8093 | `/home/deploy/RG_Internal_Invarients_SIM` |
| [`RG_Users_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Users_Invarients_SIM) | Private | `rg_users_invarients_sim` | 8091 | `/home/deploy/RG_Users_Invarients_SIM` |
| [`RG_IDE_Platform`](https://github.com/DevSwat-ResonantGenesis/RG_IDE_Platform) | Private | `ide_service` | 8080 | `/home/deploy/RG_IDE_Platform` |
| [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) | Public | `rabbit_api_service` + 4 stubs | 8000 | `/home/deploy/RG_Rabbit` |
| [`RG_Axtention_IDE`](https://github.com/DevSwat-ResonantGenesis/RG_Axtention_IDE) | Private | N/A (VS Code extension) | N/A | N/A (client-side) |

### Shared Modules (2 repos)

| Repo | Visibility | Volume Mount | Server Path |
|------|-----------|-------------|-------------|
| [`RG_UnifiedLLMClient`](https://github.com/DevSwat-ResonantGenesis/RG_UnifiedLLMClient) | Private | `/app/rg_llm:ro` | `/home/deploy/RG_UnifiedLLMClient` |
| [`RG_Unified_Tool_Registry-Observability_Module`](https://github.com/DevSwat-ResonantGenesis/RG_Unified_Tool_Registry-Observability_Module) | Private | `/app/rg_tool_registry:ro` | `/home/deploy/RG_Unified_Tool_Registry` |

### Non-Service Repos (3 repos)

| Repo | Visibility | Type |
|------|-----------|------|
| [`RG_IDE`](https://github.com/DevSwat-ResonantGenesis/RG_IDE) | Public | VS Code fork (Electron desktop app). Source of truth for extension is `RG_Axtention_IDE`. |
| [`.github`](https://github.com/DevSwat-ResonantGenesis/.github) | Public | Org profile README |
| [`RG_DevOps_Runbook`](https://github.com/DevSwat-ResonantGenesis/RG_DevOps_Runbook) | Private | This repo — infrastructure docs |

## louienemesh Account (2 repos)

| Repo | Purpose | Server Path |
|------|---------|-------------|
| [`genesis2026_production_backend_2`](https://github.com/louienemesh/genesis2026_production_backend_2) | Monolith backend — 14+ services + gateway | `/home/deploy/genesis2026_production_backend` |
| [`genesis2026_frontend_production_2`](https://github.com/louienemesh/genesis2026_frontend_production_2) | React frontend (Vite build) | `/home/deploy/genesis2026_frontend_production_2` |

## What Remains in the Monolith

Services still building from `genesis2026_production_backend` (relative `./` paths):

`gateway`, `auth_service`, `chat_service`, `memory_service`, `agent_engine_service`, `user_service`, `billing_service`, `cognitive_service`, `workflow_service`, `ml_service`, `storage_service`, `ed_service`, `marketplace_service`, `notification_service`, `blockchain_service`, `crypto_service`, `llm_service`, `build_service`, `code_execution_service`, `sandbox_runner_service`, `v8_api_service`, `openclaw_service`, `discord_bridge`, `node` (blockchain)

## Source of Truth Rules

1. **RG_Axtention_IDE** is the source of truth for the VS Code extension. Changes go there first, then sync to `RG_IDE/extensions/resonant-ai/`.
2. **Standalone repos** (RG_*) are the source of truth for their services. Never edit service code in the monolith.
3. **docker-compose.unified.yml** lives in the monolith but references external build contexts for standalone services.
4. **Frontend**: Always `git push github main` (not origin) so the server can pull from GitHub.

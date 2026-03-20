# Service Catalog

> Complete list of all 37 Docker containers running on production (as of 2026-03-20).

## Standalone Services (24) — Built from `/home/deploy/RG_*`

All extracted from the monolith into their own GitHub repos under [DevSwat-ResonantGenesis](https://github.com/DevSwat-ResonantGenesis).

### Chat & AI Services

| Container | Port | Build Context | GitHub Repo |
|-----------|------|---------------|-------------|
| `rg_agentic_chat` | 8000 | `/home/deploy/RG_Registered_Users_Agentic_Chat` | [`RG_Registered_Users_Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Registered_Users_Agentic_Chat) |
| `rg_public_guest_chat` | 8010 | `/home/deploy/RG_Public-Guest-Agentic_Chat` | [`RG_Public-Guest-Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Public-Guest-Agentic_Chat) |

### Analysis & Governance

| Container | Port | Build Context | GitHub Repo |
|-----------|------|---------------|-------------|
| `rg_ast_analysis` | 8000 | `/home/deploy/RG_AST_analysis` | [`RG_AST_analysis`](https://github.com/DevSwat-ResonantGenesis/RG_AST_analysis) |
| `rg_internal_invarients_sim` | 8093 | `/home/deploy/RG_Internal_Invarients_SIM` | [`RG_Internal_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Internal_Invarients_SIM) |
| `rg_users_invarients_sim` | 8091 | `/home/deploy/RG_Users_Invarients_SIM` | [`RG_Users_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Users_Invarients_SIM) |

### IDE & Platform

| Container | Port | Build Context | GitHub Repo |
|-----------|------|---------------|-------------|
| `ide_service` | 8080 | `/home/deploy/RG_IDE_Platform` | [`RG_IDE_Platform`](https://github.com/DevSwat-ResonantGenesis/RG_IDE_Platform) |

### Rabbit (Community Platform)

| Container | Port | Build Context | GitHub Repo |
|-----------|------|---------------|-------------|
| `rabbit_api_service` | 8000 | `/home/deploy/RG_Rabbit/rabbit_api_service` | [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) |
| `rabbit_content_service` | 8000 | `/home/deploy/RG_Rabbit/rabbit_content_service` | [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) |
| `rabbit_community_service` | 8000 | `/home/deploy/RG_Rabbit/rabbit_community_service` | [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) (stub) |
| `rabbit_vote_service` | 8000 | `/home/deploy/RG_Rabbit/rabbit_vote_service` | [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) (stub) |
| `rabbit_moderation_service` | 8000 | `/home/deploy/RG_Rabbit/rabbit_moderation_service` | [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) (stub) |

### Business & Data Services (newly extracted 2026-03-20)

| Container | Port | Build Context | GitHub Repo |
|-----------|------|---------------|-------------|
| `cognitive_service` | 8000 | `/home/deploy/RG_Cognitive` | [`RG_Cognitive`](https://github.com/DevSwat-ResonantGenesis/RG_Cognitive) |
| `workflow_service` | 8000 | `/home/deploy/RG_Workflow` | [`RG_Workflow`](https://github.com/DevSwat-ResonantGenesis/RG_Workflow) |
| `ml_service` | 8000 | `/home/deploy/RG_ML_Service` | [`RG_ML_Service`](https://github.com/DevSwat-ResonantGenesis/RG_ML_Service) |
| `storage_service` | 8000 | `/home/deploy/RG_Storage` | [`RG_Storage`](https://github.com/DevSwat-ResonantGenesis/RG_Storage) |
| `ed_service` | 8000 | `/home/deploy/RG_Ed_Service` | [`RG_Ed_Service`](https://github.com/DevSwat-ResonantGenesis/RG_Ed_Service) |
| `marketplace_service` | 8000 | `/home/deploy/RG_Marketplace` | [`RG_Marketplace`](https://github.com/DevSwat-ResonantGenesis/RG_Marketplace) |
| `notification_service` | 8000 | `/home/deploy/RG_Notifications` | [`RG_Notifications`](https://github.com/DevSwat-ResonantGenesis/RG_Notifications) |
| `crypto_service` | 8000 | `/home/deploy/RG_Crypto` | [`RG_Crypto`](https://github.com/DevSwat-ResonantGenesis/RG_Crypto) |
| `user_memory_service` | 8094 | `/home/deploy/RG_User_Memory` | [`RG_User_Memory`](https://github.com/DevSwat-ResonantGenesis/RG_User_Memory) |
| `blockchain_service` | 8000 | `/home/deploy/RG_Blockchain` | [`RG_Blockchain`](https://github.com/DevSwat-ResonantGenesis/RG_Blockchain) |

### Infrastructure & Utility Services (newly extracted 2026-03-20)

| Container | Port | Build Context | GitHub Repo |
|-----------|------|---------------|-------------|
| `build_service` | 8003 | `/home/deploy/RG_Build_Service` | [`RG_Build_Service`](https://github.com/DevSwat-ResonantGenesis/RG_Build_Service) |
| `code_execution_service` | 8002 | `/home/deploy/RG_Code_Execution` | [`RG_Code_Execution`](https://github.com/DevSwat-ResonantGenesis/RG_Code_Execution) |
| `sandbox_runner_service` | 9001 | `/home/deploy/RG_Sandbox_Runner` | [`RG_Sandbox_Runner`](https://github.com/DevSwat-ResonantGenesis/RG_Sandbox_Runner) |
| `v8_api_service` | 8080 | `/home/deploy/RG_V8_API` | [`RG_V8_API`](https://github.com/DevSwat-ResonantGenesis/RG_V8_API) |
| `openclaw_service` | 8000 | `/home/deploy/RG_OpenClaw` | [`RG_OpenClaw`](https://github.com/DevSwat-ResonantGenesis/RG_OpenClaw) |
| `discord_bridge` | — | `/home/deploy/RG_Discord_Bridge` | [`RG_Discord_Bridge`](https://github.com/DevSwat-ResonantGenesis/RG_Discord_Bridge) |

## Monolith Services (9) — Built from `./service_name`

These remain inside `genesis2026_production_backend` (core/coupled services).

| Container | Port | Build Context | Purpose |
|-----------|------|---------------|---------|
| `gateway` | 8000 (→8001 external) | `./gateway` | API gateway — routes all requests to backend services |
| `auth_service` | 8000 | `./auth_service` | Authentication, JWT, BYOK key management, user roles |
| `chat_service` | 8000 | `./chat_service` | Resonant Chat, IDE completions, streaming, resonance pipeline |
| `memory_service` | 8000 | `./memory_service` | Conversation memory, Hash Sphere ingestion |
| `agent_engine_service` | 8000 | `./agent_engine_service` | Agent planner, executor, autonomous agents, teams |
| `user_service` | 8000 | `./user_service` | User profiles, preferences, organizations |
| `billing_service` | 8000 | `./billing_service` | Stripe integration, subscriptions, usage tracking |
| `llm_service` | 8000 | `./llm_service` | Legacy LLM routing (being replaced by rg_llm) |
| `blockchain_node` | 8081 | `./node` | Blockchain node (exposed externally) |

## Infrastructure (not a service)

| Container | Port | Purpose |
|-----------|------|---------|
| `shared_redis` | 6379 | Caching, state locks, pub/sub (Redis image) |

## Shared Modules (volume-mounted, not containers)

| Module | Server Path | Volume Mount | Used By |
|--------|-------------|-------------|---------|
| `rg_llm` | `/home/deploy/RG_UnifiedLLMClient/src/rg_llm` | `/app/rg_llm:ro` | `agent_engine_service`, `chat_service`, `rg_agentic_chat`, `rg_public_guest_chat` |
| `rg_tool_registry` | `/home/deploy/RG_Unified_Tool_Registry/rg_tool_registry` | `/app/rg_tool_registry:ro` | `agent_engine_service`, `rg_agentic_chat` |

## Deleted from Monolith (all now standalone)

All 24 service directories were **deleted** from `genesis2026_production_backend` and replaced by standalone repos. Build contexts in `docker-compose.unified.yml` now point to `/home/deploy/RG_*` paths.

> **Note**: `routers_public_chat.py` and `routers_agentic_chat.py` were also removed from `agent_engine_service` — replaced by standalone `rg_public_guest_chat` and `rg_agentic_chat`.

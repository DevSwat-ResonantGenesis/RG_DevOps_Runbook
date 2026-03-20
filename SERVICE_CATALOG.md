# Service Catalog

> Complete list of all 37 Docker containers running on production.

## Standalone Services (8) — Built from `/home/deploy/RG_*`

These were extracted from the monolith into their own GitHub repos under [DevSwat-ResonantGenesis](https://github.com/DevSwat-ResonantGenesis).

| Container | Port | Build Context | GitHub Repo | Health |
|-----------|------|---------------|-------------|--------|
| `rg_agentic_chat` | 8000 | `/home/deploy/RG_Registered_Users_Agentic_Chat` | [`RG_Registered_Users_Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Registered_Users_Agentic_Chat) | ✅ healthy |
| `rg_public_guest_chat` | 8010 | `/home/deploy/RG_Public-Guest-Agentic_Chat` | [`RG_Public-Guest-Agentic_Chat`](https://github.com/DevSwat-ResonantGenesis/RG_Public-Guest-Agentic_Chat) | ✅ healthy |
| `rg_ast_analysis` | 8000 | `/home/deploy/RG_AST_analysis` | [`RG_AST_analysis`](https://github.com/DevSwat-ResonantGenesis/RG_AST_analysis) | ✅ healthy |
| `rg_internal_invarients_sim` | 8093 | `/home/deploy/RG_Internal_Invarients_SIM` | [`RG_Internal_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Internal_Invarients_SIM) | ✅ healthy |
| `rg_users_invarients_sim` | 8091 | `/home/deploy/RG_Users_Invarients_SIM` | [`RG_Users_Invarients_SIM`](https://github.com/DevSwat-ResonantGenesis/RG_Users_Invarients_SIM) | ✅ healthy |
| `ide_service` | 8080 | `/home/deploy/RG_IDE_Platform` | [`RG_IDE_Platform`](https://github.com/DevSwat-ResonantGenesis/RG_IDE_Platform) | ✅ healthy |
| `rabbit_api_service` | 8000 | `/home/deploy/RG_Rabbit/rabbit_api_service` | [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) | ✅ healthy |
| `rabbit_content_service` | 8000 | `/home/deploy/RG_Rabbit/rabbit_content_service` | [`RG_Rabbit`](https://github.com/DevSwat-ResonantGenesis/RG_Rabbit) | ✅ healthy |

> **Note**: `rabbit_community_service`, `rabbit_vote_service`, `rabbit_moderation_service` are also standalone from RG_Rabbit but are stubs (future services).

## Monolith Services (14) — Built from `./service_name`

These still live inside `genesis2026_production_backend` and build from relative paths.

| Container | Port | Build Context | Purpose |
|-----------|------|---------------|---------|
| `gateway` | 8000 (→8001 external) | `./gateway` | API gateway — routes all requests to backend services |
| `auth_service` | 8000 | `./auth_service` | Authentication, JWT, BYOK key management, user roles |
| `chat_service` | 8000 | `./chat_service` | Resonant Chat, IDE completions, streaming, resonance pipeline |
| `memory_service` | 8000 | `./memory_service` | Conversation memory, Hash Sphere ingestion |
| `agent_engine_service` | 8000 | `./agent_engine_service` | Agent planner, executor, autonomous agents, teams |
| `user_service` | 8000 | `./user_service` | User profiles, preferences, organizations |
| `billing_service` | — | `./billing_service` | Stripe integration, subscriptions, usage tracking |
| `cognitive_service` | 8000 | `./cognitive_service` | Cognitive pipelines, analysis |
| `workflow_service` | 8000 | `./workflow_service` | Workflow orchestration |
| `ml_service` | 8000 | `./ml_service` | ML model registry, inference |
| `storage_service` | 8000 | `./storage_service` | File storage, uploads |
| `ed_service` | — | `./ed_service` | Educational content service |
| `marketplace_service` | — | `./marketplace_service` | Agent/tool marketplace |
| `notification_service` | — | `./notification_service` | Email (SendGrid), push notifications |

## Infrastructure Services (5) — Built from `./service_name`

| Container | Port | Build Context | Purpose |
|-----------|------|---------------|---------|
| `shared_redis` | 6379 | Redis image | Caching, state locks, pub/sub |
| `blockchain_service` | — | `./blockchain_service` | Blockchain identity, trust tiers |
| `blockchain_node` | 8081 | `./node` | Blockchain node (exposed externally) |
| `crypto_service` | — | `./crypto_service` | Cryptographic operations |
| `llm_service` | — | `./llm_service` | Legacy LLM routing (being replaced by rg_llm) |

## Utility Services (5) — Built from `./service_name`

| Container | Port | Build Context | Purpose |
|-----------|------|---------------|---------|
| `build_service` | 8003 | `./build_service` | Project compilation |
| `code_execution_service` | 8002 | `./code_execution_service` | Sandboxed code execution |
| `sandbox_runner_service` | 9001 | `./sandbox_runner_service` | Sandbox container runner |
| `v8_api_service` | 8080 | `./v8_api_service` | V8 JavaScript execution |
| `openclaw_service` | 8000 | `./openclaw_service` | Legal document processing |

## Shared Modules (volume-mounted, not containers)

| Module | Server Path | Volume Mount | Used By |
|--------|-------------|-------------|---------|
| `rg_llm` | `/home/deploy/RG_UnifiedLLMClient/src/rg_llm` | `/app/rg_llm:ro` | `agent_engine_service`, `chat_service`, `rg_agentic_chat`, `rg_public_guest_chat` |
| `rg_tool_registry` | `/home/deploy/RG_Unified_Tool_Registry/rg_tool_registry` | `/app/rg_tool_registry:ro` | `agent_engine_service`, `rg_agentic_chat` |

## Stub Services (3) — Exist but minimal functionality

| Container | Build Context | Notes |
|-----------|---------------|-------|
| `rabbit_community_service` | `/home/deploy/RG_Rabbit/rabbit_community_service` | Stub — future community management |
| `rabbit_vote_service` | `/home/deploy/RG_Rabbit/rabbit_vote_service` | Stub — future vote aggregation |
| `rabbit_moderation_service` | `/home/deploy/RG_Rabbit/rabbit_moderation_service` | Stub — future moderation tools |

## Deleted from Monolith (now standalone)

These directories were **deleted** from `genesis2026_production_backend` and replaced by standalone repos:

| Old Directory | Replaced By | Container Name |
|---------------|-------------|----------------|
| `code_visualizer_service/` | `RG_AST_analysis` | `rg_ast_analysis` |
| `rara_service/` | `RG_Internal_Invarients_SIM` | `rg_internal_invarients_sim` |
| `state_physics_service/` | `RG_Users_Invarients_SIM` | `rg_users_invarients_sim` |
| `ide_platform_service/` | `RG_IDE_Platform` | `ide_service` |
| `rabbit_api_service/` | `RG_Rabbit` | `rabbit_api_service` |
| `rabbit_content_service/` | `RG_Rabbit` | `rabbit_content_service` |
| `rabbit_community_service/` | `RG_Rabbit` | `rabbit_community_service` |
| `rabbit_vote_service/` | `RG_Rabbit` | `rabbit_vote_service` |
| `rabbit_moderation_service/` | `RG_Rabbit` | `rabbit_moderation_service` |

> **Note**: `routers_public_chat.py` and `routers_agentic_chat.py` were also removed from `agent_engine_service` — replaced by standalone `rg_public_guest_chat` and `rg_agentic_chat`.

## Server-Side Remnant Directories

The following old directories still exist on the server at `/home/deploy/genesis2026_production_backend/` but are **no longer used** (build contexts point elsewhere). They can be safely deleted:

- `code_visualizer_service/`
- `rara_service/`
- `state_physics_service/`
- `ide_service/`
- `rabbit_api_service/`, `rabbit_content_service/`, `rabbit_community_service/`, `rabbit_vote_service/`, `rabbit_moderation_service/`

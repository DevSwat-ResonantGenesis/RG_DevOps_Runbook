# Gateway Routes

> Complete proxy routing map from the gateway to all backend services.

## Gateway Overview

The gateway runs on port 8000 (mapped to 8001 externally). Nginx proxies all `/api/v1/*` requests to `localhost:8001`.

## Route Map

### Agentic Chat (standalone)
| Route | Target | Service |
|-------|--------|---------|
| `/agentic-chat/*` | `http://rg_agentic_chat:8000/*` | Registered users AI assistant |
| `/public/agentic-chat/*` | `http://rg_public_guest_chat:8010/*` | Public guest AI assistant |

### Code Analysis (standalone)
| Route | Target | Service |
|-------|--------|---------|
| `/code-visualizer/*` | `http://rg_ast_analysis:8000/*` | Code Visualizer endpoints |
| `/api/v1/scan/*` | `http://rg_ast_analysis:8000/*` | AST scanning endpoints |

### Invariants (standalone)
| Route | Target | Service |
|-------|--------|---------|
| `/rara/*` | `http://rg_internal_invarients_sim:8093/*` | Internal governance (RARA) |
| `/state-physics/*` | `http://rg_users_invarients_sim:8091/*` | Hash Sphere state physics |

### IDE Platform (standalone)
| Route | Target | Service |
|-------|--------|---------|
| `/terminal/*` | `http://ide_service:8080/terminal/*` | Terminal PTY sessions |
| `/api/v1/ide/loc/*` | `http://ide_service:8080/loc/*` | LOC tracking |
| `/api/v1/ide/updates/*` | `http://ide_service:8080/updates/*` | IDE auto-update checks |
| `/ws/ide` | `ws://ide_service:8080/ws/ide` | IDE WebSocket |
| `/ws/terminal` | `ws://ide_service:8080/ws/terminal` | Terminal WebSocket |
| `/ws/debug` | `ws://ide_service:8080/ws/debug` | Debug WebSocket |

### Rabbit (standalone)
| Route | Target | Service |
|-------|--------|---------|
| `/rabbit/*` | `http://rabbit_api_service:8000/*` | Rabbit community API |
| `/api/v1/rabbit/*` | `http://rabbit_api_service:8000/*` | Rabbit API (prefixed) |

### Auth (monolith)
| Route | Target | Service |
|-------|--------|---------|
| `/auth/*` | `http://auth_service:8000/auth/*` | Authentication, JWT, BYOK keys |
| `/user/api-keys/*` | `http://auth_service:8000/auth/user/api-keys/*` | BYOK key management |
| `/user/api-keys/by-provider/*` | `http://auth_service:8000/auth/user/api-keys/by-provider/*` | Delete BYOK by provider |

### Chat (monolith)
| Route | Target | Service |
|-------|--------|---------|
| `/resonant-chat/*` | `http://chat_service:8000/resonant-chat/*` | Resonant Chat (web) |
| `/api/v1/ide/completions` | `http://chat_service:8000/ide/completions` | IDE LLM proxy (SSE) |

### Memory (monolith)
| Route | Target | Service |
|-------|--------|---------|
| `/memory/*` | `http://memory_service:8000/memory/*` | Conversation memory |
| `/memory/stats` | `http://memory_service:8000/memory/stats` | Memory statistics |

### Agent Engine (monolith)
| Route | Target | Service |
|-------|--------|---------|
| `/agent-engine/*` | `http://agent_engine_service:8000/*` | Agent planner/executor |
| `/agents/*` | `http://agent_engine_service:8000/*` | Agent teams, restore |

### Other Monolith Services
| Route | Target | Service |
|-------|--------|---------|
| `/crypto/*` | `http://crypto_service:8000/*` | Cryptographic operations |
| `/workflow/*` | `http://workflow_service:8000/*` | Workflow orchestration |
| `/marketplace/*` | `http://marketplace_service:8000/*` | Agent marketplace |
| `/blockchain/*` | `http://blockchain_service:8000/*` | Blockchain identity |
| `/ml/*` | `http://ml_service:8000/*` | ML model registry |
| `/orgs/*` | `http://user_service:8000/*` | Organizations |
| `/users/*` | `http://user_service:8000/*` | User profiles |
| `/usage/*` | `http://billing_service:8000/*` | Usage tracking |
| `/finance/*` | `http://billing_service:8000/*` | Finance/billing |
| `/audit/*` | `http://auth_service:8000/*` | Audit logs |
| `/public/*` | Varies | Public endpoints (guest chat, etc.) |

## Environment Variables (Gateway)

The gateway uses these env vars to resolve service URLs:

```
GATEWAY_AUTH_URL=http://auth_service:8000
GATEWAY_CHAT_URL=http://chat_service:8000
GATEWAY_MEMORY_URL=http://memory_service:8000
GATEWAY_USER_URL=http://user_service:8000
GATEWAY_BILLING_URL=http://billing_service:8000
GATEWAY_AGENT_ENGINE_URL=http://agent_engine_service:8000
GATEWAY_COGNITIVE_URL=http://cognitive_service:8000
GATEWAY_WORKFLOW_URL=http://workflow_service:8000
GATEWAY_ML_URL=http://ml_service:8000
GATEWAY_STORAGE_URL=http://storage_service:8000
GATEWAY_ED_URL=http://ed_service:8000
GATEWAY_MARKETPLACE_URL=http://marketplace_service:8000
GATEWAY_BLOCKCHAIN_URL=http://blockchain_service:8000
GATEWAY_NOTIFICATION_URL=http://notification_service:8000
GATEWAY_CRYPTO_URL=http://crypto_service:8000
GATEWAY_IDE_URL=http://ide_service:8080
GATEWAY_BUILD_URL=http://build_service:8003
GATEWAY_CODE_EXECUTION_URL=http://code_execution_service:8002
AGENTIC_CHAT_SERVICE_URL=http://rg_agentic_chat:8000
GUEST_CHAT_SERVICE_URL=http://rg_public_guest_chat:8010
```

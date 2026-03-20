# API Catalog

> Complete backend API route inventory across all 30 services (as of 2026-03-20).
>
> **Total: ~750 unique endpoints** across 30 microservices.
> **Frontend coverage: ~45 of 106 API files migrated** to RGF_* micro-apps. ~61 still need migration.

## Route Counts by Service

| Service | Repo | Routes | Gateway Prefix | Frontend Coverage |
|---------|------|--------|----------------|-------------------|
| Gateway | `RG_Gateway` | 558 (proxy) | — | N/A (proxy only) |
| Auth | `RG_Auth` | 111 | `/auth/*`, `/oauth/*` | ✅ `RGF_Auth/auth.ts` |
| Billing | `RG_Billing` | 84 | `/billing/*` | ⚠️ Partial — `RGF_Dashboard/billing.ts`, `billingComplete.ts` |
| Chat | `RG_Chat` | 115 | `/resonant-chat/*`, `/chat/*`, `/message/*` | ✅ `RGF_Resonant_Chat/chat.ts`, `resonantChat.ts`, `llm.ts` |
| Memory | `RG_Memory` | 38 | `/rag/*` | ⚠️ Partial — `RGF_Hash_Sphere/memory.ts` |
| Agent Engine | `RG_Agent_Engine` | 337 | `/agents/*`, `/agent-teams/*` | ⚠️ Partial — `RGF_Agents/agents.ts`, `agentApi.ts`, `agentTeams.ts` |
| User Service | `RG_User_Service` | 8 | `/user/*` | ❌ Missing — needs `RGF_Settings/users.ts` |
| LLM Service | `RG_LLM_Service` | 12 | `/llm/*` | ✅ `RGF_Resonant_Chat/llmProviders.ts` |
| Cognitive | `RG_Cognitive` | 12 | `/cognitive/*` | ❌ Missing — needs `RGF_Network/cognitive.ts` |
| Workflow | `RG_Workflow` | 17 | `/workflow/*` | ❌ Missing — needs `RGF_Network/workflow.ts` |
| ML Service | `RG_ML_Service` | 33 | `/ml/*` | ✅ `RGF_Admin/ml.ts` |
| Storage | `RG_Storage` | 13 | `/storage/*` | ❌ Missing — needs shared `storage.ts` |
| Ed Service | `RG_Ed_Service` | 25 | `/ed/*` | ❌ No frontend API file |
| Marketplace | `RG_Marketplace` | 17 | `/marketplace/*` | ⚠️ Partial — `RGF_Marketplace/marketplace.ts` |
| Notifications | `RG_Notifications` | 12 | `/notifications/*` | ❌ Missing — needs `RGF_Shell/notifications.ts` |
| Crypto | `RG_Crypto` | 23 | `/crypto/*` | ✅ `RGF_Marketplace/crypto.ts` |
| User Memory | `RG_User_Memory` | 15 | `/user-memory/*` | ❌ No frontend API file |
| Blockchain | `RG_Blockchain` | 499 | `/blockchain/*` | ⚠️ Partial — `RGF_Network/blockchain.ts`, `advancedBlockchain.ts` |
| Build Service | `RG_Build_Service` | 9 | `/api/v1/project-builder/*` | ❌ Missing — needs `RGF_Code_Tools/build.ts` |
| Code Execution | `RG_Code_Execution` | 8 | `/code-execution/*` | ❌ No frontend API file |
| Sandbox Runner | `RG_Sandbox_Runner` | 2 | `/sandbox/*` | ❌ No frontend API file |
| V8 API | `RG_V8_API` | 0 (JS) | `/v8/*` | ❌ No frontend API file |
| OpenClaw | `RG_OpenClaw` | 21 | `/openclaw/*` | ❌ No frontend API file |
| Discord Bridge | `RG_Discord_Bridge` | 0 | N/A | N/A (bot only) |
| Agentic Chat | `RG_Registered_Users_Agentic_Chat` | 6 | `/agentic-chat/*` | ✅ `RGF_Agentic_Assistant/agentEngine.ts` |
| Public Guest Chat | `RG_Public-Guest-Agentic_Chat` | 3 | `/v1/public/agentic-chat/*` | ❌ No frontend API file |
| AST Analysis | `RG_AST_analysis` | 28 | `/ast/*` | ✅ `RGF_Code_Tools/code.ts` |
| Internal Invariants | `RG_Internal_Invarients_SIM` | 78 | `/rara/*` | ⚠️ Partial — `RGF_Admin/admin.ts` |
| User Invariants | `RG_Users_Invarients_SIM` | 25 | `/state-physics/*` | ✅ `RGF_Hash_Sphere/economicState.ts` |
| IDE Platform | `RG_IDE_Platform` | 57 | `/ide/*` | ⚠️ Partial — `RGF_Admin/ideLoc.ts` |
| Blockchain Node | `RG_Blockchain_Node` | 0 (JS) | `:8081` | ❌ No frontend API file |

## RG_Auth — 111 Routes

### Authentication & Registration
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/auth/register` | Register new user |
| POST | `/auth/signup` | Signup (alias) |
| POST | `/auth/login` | Login with credentials |
| POST | `/auth/logout` | Logout |
| POST | `/auth/refresh` | Refresh JWT token |
| POST | `/auth/verify` | Verify token |
| POST | `/auth/verify-email` | Verify email address |
| POST | `/auth/resend-verification` | Resend verification email |
| POST | `/auth/forgot-password` | Request password reset |
| POST | `/auth/reset-password` | Reset password with token |
| POST | `/auth/change-password` | Change password (authenticated) |
| GET | `/auth/me` | Get current user profile |
| GET | `/auth/identity` | Get user identity (DSID) |
| GET | `/auth/email-status` | Check email verification status |

### MFA
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/auth/mfa/setup` | Setup MFA |
| POST | `/auth/mfa/verify` | Verify MFA code |
| POST | `/auth/mfa/verify-backup` | Verify with backup code |
| POST | `/auth/mfa/disable` | Disable MFA |
| POST | `/auth/mfa/backup-codes/regenerate` | Regenerate backup codes |
| GET | `/auth/mfa/status` | Check MFA status |

### BYOK API Keys
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/auth/user/api-keys` | List user API keys |
| POST | `/auth/user/api-keys` | Create API key |
| POST | `/auth/user/api-keys/validate` | Validate API key |
| DELETE | `/auth/user/api-keys/{key_id}` | Delete API key |
| DELETE | `/auth/user/api-keys/by-provider/{provider}` | Delete keys by provider |
| GET | `/auth/user/available-providers` | List available LLM providers |
| GET | `/auth/user/service-access` | Check service access level |
| GET | `/auth/user/trial-status` | Check trial status |

### OAuth & SSO
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/oauth/github/login` | GitHub OAuth initiate |
| GET | `/oauth/google/login` | Google OAuth initiate |
| GET | `/auth/oauth/callback` | OAuth callback |
| GET | `/auth/desktop-callback` | Desktop app OAuth callback |
| POST | `/auth/sso/oauth/initiate` | SSO OAuth initiate |
| POST | `/auth/sso/oauth/callback` | SSO OAuth callback |
| POST | `/auth/sso/saml/initiate` | SAML SSO initiate |
| POST | `/auth/sso/saml/callback` | SAML SSO callback |
| GET | `/auth/sso/providers` | List SSO providers |
| POST | `/auth/services/google/initiate` | Google service integration |
| POST | `/auth/services/google/callback` | Google service callback |
| POST | `/auth/services/slack/initiate` | Slack service integration |
| POST | `/auth/services/slack/callback` | Slack service callback |
| GET | `/auth/integrations` | List integrations |
| GET | `/auth/integrations/{integration_id}/status` | Integration status |

### Sessions & Devices
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/auth/sessions` | List active sessions |
| DELETE | `/auth/sessions/{session_id}` | Revoke session |
| POST | `/auth/sessions/revoke-all` | Revoke all sessions |
| GET | `/auth/trusted-devices` | List trusted devices |
| POST | `/auth/trusted-devices` | Add trusted device |
| DELETE | `/auth/trusted-devices/{device_id}` | Remove trusted device |
| POST | `/auth/trusted-devices/revoke-all` | Revoke all devices |

### Organizations
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/auth/orgs` | List organizations |
| POST | `/auth/orgs/invite` | Invite to org |

### Agent Settings (CRUD)
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/auth/settings/agents` | List user agents |
| POST | `/auth/settings/agents` | Create agent |
| GET | `/auth/settings/agents/{agent_id}` | Get agent |
| PUT | `/auth/settings/agents/{agent_id}` | Update agent |
| DELETE | `/auth/settings/agents/{agent_id}` | Delete agent |
| GET | `/auth/settings/agents/shared` | List shared agents |
| GET | `/auth/settings/agents/templates` | List agent templates |
| POST | `/auth/settings/agents/from-template/{template_id}` | Create from template |
| POST | `/auth/settings/agents/{agent_id}/save-template` | Save as template |
| POST | `/auth/settings/agents/import` | Import agent |
| POST | `/auth/settings/agents/{agent_id}/export` | Export agent |
| POST | `/auth/settings/agents/{agent_id}/share` | Share agent |
| POST | `/auth/settings/agents/{agent_id}/hash` | Hash agent identity |
| GET | `/auth/settings/agents/{agent_id}/anchors` | Get agent anchors |
| DELETE | `/auth/settings/agents/{agent_id}/anchors/{anchor_id}` | Delete anchor |
| GET | `/auth/settings/agents/{agent_id}/api-keys` | Agent API keys |
| POST | `/auth/settings/agents/{agent_id}/api-keys` | Create agent API key |
| PUT | `/auth/settings/agents/{agent_id}/api-keys/{key_id}` | Update agent API key |
| DELETE | `/auth/settings/agents/{agent_id}/api-keys/{key_id}` | Delete agent API key |
| GET | `/auth/settings/agents/{agent_id}/memory` | Get agent memory config |
| PUT | `/auth/settings/agents/{agent_id}/memory` | Update memory config |
| GET | `/auth/settings/agents/{agent_id}/metrics` | Agent metrics |
| GET | `/auth/settings/agents/{agent_id}/patches` | Agent patches |
| GET | `/auth/settings/agents/{agent_id}/restrictions` | Agent restrictions |
| PUT | `/auth/settings/agents/{agent_id}/restrictions` | Update restrictions |
| GET | `/auth/settings/providers` | Available providers |

### Admin
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/admin/block-user/{user_id}` | Block user |
| POST | `/admin/unblock-user/{user_id}` | Unblock user |
| DELETE | `/admin/delete-user/{user_id}` | Delete user |
| POST | `/admin/reset-password/{user_id}` | Reset user password |
| POST | `/admin/set-password/{user_id}` | Set user password |
| POST | `/auth/mnemonic` | Generate mnemonic |
| GET | `/dashboard/stats` | Dashboard statistics |
| GET | `/dashboard/users` | Dashboard user list |

## RG_Billing — 84 Routes

| Method | Path | Purpose |
|--------|------|---------|
| GET | `/billing/health` | Health check |
| GET | `/billing/plans` | List subscription plans |
| GET | `/billing/subscription` | Get current subscription |
| POST | `/billing/checkout` | Create checkout session |
| POST | `/billing/checkout/subscription` | Subscription checkout |
| POST | `/billing/stripe/checkout` | Stripe checkout |
| POST | `/billing/subscription/cancel` | Cancel subscription |
| POST | `/billing/subscription/change` | Change subscription |
| POST | `/billing/subscription/change-plan` | Change plan |
| GET | `/billing/credits` | Get credits balance |
| POST | `/billing/credits/estimate` | Estimate credit cost |
| GET | `/billing/usage` | Usage stats |
| GET | `/billing/usage/check` | Check usage limits |
| GET | `/billing/usage/history` | Usage history |
| GET | `/billing/usage/summary` | Usage summary |
| POST | `/billing/usage/record` | Record usage |
| GET | `/billing/invoices` | List invoices |
| GET | `/billing/tokens/packs` | Token packs |
| POST | `/billing/tokens/purchase` | Purchase tokens |
| POST | `/billing/webhook/stripe` | Stripe webhook |
| GET | `/billing/limits` | Get limits |
| PUT | `/billing/limits/{limit_id}` | Update limit |
| GET | `/billing/customers` | List customers |
| GET | `/billing/customers/{customer_id}` | Get customer |
| POST | `/billing/customers` | Create customer |
| PUT | `/billing/customers/{customer_id}` | Update customer |
| GET | `/billing/orders` | List orders |
| GET | `/billing/orders/{order_id}` | Get order |
| POST | `/billing/orders` | Create order |
| PUT | `/billing/orders/{order_id}/status` | Update order status |
| GET | `/billing/reservations` | List reservations |
| GET | `/billing/reservations/{reservation_id}` | Get reservation |
| POST | `/billing/reservations` | Create reservation |
| PUT | `/billing/reservations/{reservation_id}/cancel` | Cancel reservation |
| GET | `/billing/staff` | List staff |
| GET | `/billing/staff/{staff_id}` | Get staff |
| POST | `/billing/staff` | Create staff |
| GET | `/billing/dashboard` | Billing dashboard |
| GET | `/billing/analytics` | Billing analytics |

## RG_Chat — 115 Routes

| Method | Path | Purpose |
|--------|------|---------|
| GET | `/resonant-chat/conversations` | List conversations |
| POST | `/resonant-chat/conversations` | Create conversation |
| GET | `/resonant-chat/conversations/{id}` | Get conversation |
| DELETE | `/resonant-chat/conversations/{id}` | Delete conversation |
| PUT | `/resonant-chat/conversations/{id}` | Update conversation |
| POST | `/resonant-chat/message` | Send message |
| POST | `/resonant-chat/message/stream` | Stream message (SSE) |
| POST | `/resonant-chat/save-agentic` | Cross-save agentic messages |
| GET | `/resonant-chat/analytics` | Chat analytics |
| DELETE | `/resonant-chat/analytics` | Delete analytics |
| GET | `/resonant-chat/models` | Available models |
| GET | `/resonant-chat/providers` | Available providers |
| GET | `/resonant-chat/skills` | Available skills |
| POST | `/resonant-chat/skills/toggle` | Toggle skill |
| GET | `/resonant-chat/settings` | Chat settings |
| PUT | `/resonant-chat/settings` | Update chat settings |
| POST | `/ide/completions` | IDE completions (SSE) |
| GET | `/health` | Health check |

## RG_Memory — 38 Routes

| Method | Path | Purpose |
|--------|------|---------|
| GET | `/health` | Health check |
| POST | `/memories/ingest` | Ingest memory |
| POST | `/memories/search` | Search memories |
| GET | `/memories/conversations/{id}` | Get conversation memories |
| DELETE | `/memories/conversations/{id}` | Delete conversation memories |
| GET | `/memories/stats` | Memory stats |
| POST | `/memories/anchor` | Anchor to blockchain |
| GET | `/memories/anchors/{hash}` | Get anchor |
| POST | `/hash-sphere/ingest` | Ingest to Hash Sphere |
| GET | `/hash-sphere/stats` | Hash Sphere stats |
| POST | `/hash-sphere/search` | Search Hash Sphere |
| GET | `/hash-sphere/nodes` | Get nodes |
| POST | `/hash-sphere/traverse` | Traverse graph |

## RG_Agent_Engine — 337 Routes

### Agent CRUD
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/agents/create` | Create agent |
| POST | `/agents/register` | Register agent |
| GET | `/agents` | List agents |
| GET | `/agents/{agent_id}` | Get agent |
| PUT | `/agents/{agent_id}` | Update agent |
| PATCH | `/agents/{agent_id}` | Patch agent |
| DELETE | `/agents/{agent_id}` | Delete agent |
| PATCH | `/agents/{agent_id}/unarchive` | Unarchive agent |

### Agent Execution
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/agents/{agent_id}/execute` | Execute agent |
| POST | `/agents/{agent_id}/awaken` | Awaken agent |
| POST | `/agents/{agent_id}/sleep` | Sleep agent |
| POST | `/agents/{agent_id}/message` | Send message |
| POST | `/agents/{agent_id}/goal` | Set goal |
| POST | `/agents/{agent_id}/goals` | Set multiple goals |
| POST | `/agents/{agent_id}/reflect` | Agent self-reflect |
| POST | `/agents/{agent_id}/reason` | Agent reason |
| POST | `/agents/{agent_id}/metacognition` | Metacognition step |
| POST | `/agents/{agent_id}/justify` | Justify action |
| POST | `/agents/{agent_id}/broadcast` | Broadcast message |
| POST | `/agents/{agent_id}/delegate` | Delegate to another |
| POST | `/agents/{agent_id}/checkpoint` | Save checkpoint |
| POST | `/agents/{agent_id}/evolve` | Evolve agent |
| POST | `/agents/{agent_id}/personality` | Set personality |
| POST | `/agents/{agent_id}/initiative` | Take initiative |

### Agent Memory
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/agents/{agent_id}/memory/remember` | Store memory |
| POST | `/agents/{agent_id}/memory/recall` | Recall memory |
| POST | `/agents/{agent_id}/memory/pattern` | Learn pattern |
| POST | `/agents/{agent_id}/memory/apply-patterns` | Apply patterns |
| GET | `/agents/{agent_id}/memory` | Get memory config |
| PUT | `/agents/{agent_id}/memory` | Update memory config |
| POST | `/agents/{agent_id}/learning/experience` | Log experience |
| POST | `/agents/{agent_id}/improvement/register` | Register improvement |
| POST | `/agents/{agent_id}/resilience/register` | Register resilience |

### Agent Publishing & Sharing
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/agents/{agent_id}/publish` | Publish agent |
| POST | `/agents/{agent_id}/publish-api` | Publish as API |
| POST | `/agents/{agent_id}/unpublish-api` | Unpublish API |
| POST | `/agents/{agent_id}/share` | Share agent |
| POST | `/agents/{agent_id}/marketplace-publish` | Publish to marketplace |
| POST | `/agents/{agent_id}/marketplace-unpublish` | Unpublish from marketplace |
| POST | `/agents/{agent_id}/export` | Export agent |
| POST | `/agents/{agent_id}/hash` | Hash identity |
| POST | `/agents/{agent_id}/save-template` | Save as template |

### Agent Sessions
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/agents/{agent_id}/sessions` | List sessions |
| POST | `/agents/{agent_id}/sessions` | Create session |
| GET | `/agents/{agent_id}/sessions/{session_id}` | Get session |
| POST | `/sessions/{session_id}/approve/{step_id}` | Approve step |
| POST | `/sessions/{session_id}/cancel` | Cancel session |
| POST | `/sessions/{session_id}/feedback` | Session feedback |

### Agent Schedules & Triggers
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/agents/{agent_id}/schedules` | List schedules |
| POST | `/agents/{agent_id}/schedules` | Create schedule |
| PATCH | `/schedules/{schedule_id}` | Update schedule |
| DELETE | `/schedules/{schedule_id}` | Delete schedule |
| GET | `/agents/{agent_id}/triggers` | List triggers |
| POST | `/agents/{agent_id}/triggers` | Create trigger |
| PATCH | `/trigger/{trigger_id}/toggle` | Toggle trigger |
| DELETE | `/triggers/{trigger_id}` | Delete trigger |
| POST | `/triggers/webhook/{trigger_id}` | Webhook trigger |

### Agent Teams
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/teams` | List teams |
| POST | `/teams` | Create team |
| GET | `/teams/{team_id}` | Get team |
| PUT | `/teams/{team_id}` | Update team |
| PATCH | `/teams/{team_id}` | Patch team |
| DELETE | `/teams/{team_id}` | Delete team |
| PATCH | `/teams/{team_id}/archive` | Archive team |
| PATCH | `/teams/{team_id}/unarchive` | Unarchive team |
| GET | `/teams/{team_id}/members` | List members |
| POST | `/teams/{team_id}/execute` | Execute team |
| GET | `/teams/{team_id}/workflows` | Team workflows |
| POST | `/teams/workflows/{workflow_id}/cancel` | Cancel workflow |
| GET | `/teams/{team_id}/ownership` | Team ownership |
| POST | `/teams/{team_id}/transfer` | Transfer ownership |
| POST | `/teams/{team_id}/mint-nft` | Mint team NFT |
| GET | `/teams/{team_id}/rentals` | Team rentals |
| POST | `/teams/{team_id}/rent` | Rent team |
| GET | `/teams/my-rentals` | My rentals |

### Agent Terminal
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/agents/{agent_id}/terminal/execute` | Terminal execute |
| GET | `/agents/{agent_id}/terminal/status` | Terminal status |
| GET | `/agents/{agent_id}/terminal/audit` | Terminal audit log |

### Agent API Keys & Versions
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/agents/{agent_id}/api-keys` | List API keys |
| POST | `/agents/{agent_id}/api-keys` | Create API key |
| GET | `/agents/{agent_id}/versions` | Version history |
| GET | `/agents/{agent_id}/metrics` | Agent metrics |
| GET | `/agents/{agent_id}/anchors` | Agent anchors |
| GET | `/agents/{agent_id}/restrictions` | Agent restrictions |
| PUT | `/agents/{agent_id}/restrictions` | Update restrictions |
| GET | `/agents/{agent_id}/patches` | Agent patches |

### Autonomous Daemon
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/daemon/start` | Start daemon |
| POST | `/daemon/stop` | Stop daemon |
| GET | `/daemon/status` | Daemon status |
| GET | `/daemon/agents` | Daemon agents |

### Connections
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/connections` | List connections |
| POST | `/connections` | Create connection |
| PATCH | `/connections/{connection_id}` | Update connection |
| DELETE | `/connections/{connection_id}` | Delete connection |
| POST | `/internal/connect` | Internal connect |
| POST | `/internal/disconnect` | Internal disconnect |

### Swarms & Collective
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/swarm/create` | Create swarm |
| POST | `/swarms/create` | Create swarm (v2) |
| POST | `/swarms/{swarm_id}/scale` | Scale swarm |
| POST | `/collective/contribute` | Collective contribute |
| POST | `/collective/solve` | Collective solve |
| POST | `/network/spawn` | Spawn network agent |

### Governance & Consensus
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/governance/evaluate` | Evaluate governance |
| POST | `/consensus/propose` | Propose consensus |
| POST | `/consensus/{proposal_id}/vote` | Vote on proposal |
| POST | `/voting/propose` | Propose vote |
| POST | `/voting/{decision_id}/vote` | Cast vote |
| POST | `/approvals/{approval_id}/approve` | Approve |
| POST | `/approvals/{approval_id}/reject` | Reject |
| POST | `/delegations/{delegation_id}/accept` | Accept delegation |
| POST | `/delegations/{delegation_id}/reject` | Reject delegation |
| POST | `/delegations/{delegation_id}/complete` | Complete delegation |

### Goals & Tasks
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/goals/submit` | Submit goal |
| POST | `/goals/decompose` | Decompose goal |
| POST | `/goals/plan-adaptive` | Adaptive planning |
| POST | `/tasks/report` | Task report |

### Watchdog & Events
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/watchdog/status` | Watchdog status |
| GET | `/watchdog/alerts` | List alerts |
| POST | `/watchdog/alerts/{alert_id}/acknowledge` | Acknowledge alert |
| POST | `/events/inject` | Inject event |
| POST | `/anomaly-triggers` | Create anomaly trigger |
| POST | `/anomaly-triggers/fire` | Fire anomaly |

### Templates & Tools
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/templates` | List templates |
| POST | `/templates/{template_id}/instantiate` | Instantiate template |
| GET | `/tools` | List tools |
| POST | `/repo-to-agent` | Create agent from repo |
| POST | `/repo-to-agent/analyze` | Analyze repo |

### World Model
| Method | Path | Purpose |
|--------|------|---------|
| GET | `/world/stats` | World stats |
| GET | `/world/entities` | World entities |
| POST | `/world/event` | Create event |
| POST | `/world/observe` | Observe |
| POST | `/world/relate` | Create relation |
| GET | `/world/understand` | Understand world |

### Published Agent APIs
| Method | Path | Purpose |
|--------|------|---------|
| POST | `/api/v1/{slug}` | Execute published agent API |
| POST | `/public/{slug}/run` | Run public agent API |

## RG_LLM_Service — 12 Routes

| Method | Path | Purpose |
|--------|------|---------|
| GET | `/health` | Health check |
| GET | `/models` | List models |
| GET | `/providers` | List providers |
| GET | `/tools` | List tools |
| POST | `/chat/completions` | Chat completion |
| POST | `/chat/completions/stream` | Stream completion |
| POST | `/agents/route-query` | Route query to provider |
| POST | `/ai/classify-intent` | Classify intent |
| POST | `/tokens/count` | Count tokens |
| POST | `/agent/run` | Run agent |
| POST | `/tools/register` | Register tool |

## RG_Cognitive — 12 Routes

| Method | Path | Purpose |
|--------|------|---------|
| GET | `/health` | Health check |
| POST | `/analyze` | Analyze input |
| POST | `/patterns/detect` | Detect patterns |
| POST | `/patterns/match` | Match patterns |
| POST | `/reasoning/chain` | Chain of reasoning |
| POST | `/reasoning/verify` | Verify reasoning |
| POST | `/insights/generate` | Generate insights |
| POST | `/context/build` | Build context |
| POST | `/context/merge` | Merge contexts |
| GET | `/capabilities` | List capabilities |
| POST | `/evaluate` | Evaluate |
| GET | `/status` | Service status |

## RG_Workflow — 17 Routes

| Method | Path | Purpose |
|--------|------|---------|
| GET | `/health` | Health check |
| GET | `/workflows` | List workflows |
| POST | `/workflows` | Create workflow |
| GET | `/workflows/{id}` | Get workflow |
| PUT | `/workflows/{id}` | Update workflow |
| DELETE | `/workflows/{id}` | Delete workflow |
| POST | `/workflows/{id}/execute` | Execute workflow |
| POST | `/workflows/{id}/cancel` | Cancel workflow |
| GET | `/workflows/{id}/status` | Workflow status |
| GET | `/workflows/{id}/history` | Workflow history |
| GET | `/templates` | List templates |
| POST | `/templates` | Create template |
| GET | `/templates/{id}` | Get template |
| DELETE | `/templates/{id}` | Delete template |
| POST | `/templates/{id}/instantiate` | Instantiate template |
| GET | `/executions` | List executions |
| GET | `/executions/{id}` | Get execution |

## Smaller Services (Summary)

### RG_Marketplace — 17 Routes
`GET /health`, `GET /listings`, `POST /listings`, `GET /listings/{id}`, `PUT /listings/{id}`, `DELETE /listings/{id}`, `POST /listings/{id}/purchase`, `GET /purchases`, `GET /categories`, `POST /categories`, `GET /reviews/{id}`, `POST /reviews`, `GET /featured`, `GET /search`, `GET /stats`, `POST /rate`, `GET /installations`

### RG_Notifications — 12 Routes
`GET /health`, `GET /notifications`, `POST /notifications`, `PUT /notifications/{id}/read`, `PUT /notifications/read-all`, `DELETE /notifications/{id}`, `GET /preferences`, `PUT /preferences`, `POST /subscribe`, `DELETE /unsubscribe/{topic}`, `GET /stats`, `POST /send`

### RG_Crypto — 23 Routes
`GET /health`, `GET /wallets`, `POST /wallets/create`, `POST /wallets/sign`, `POST /wallets/transfer`, `POST /wallets/verify`, `POST /wallets/{address}/lock`, `POST /wallets/{address}/unlock`, `GET /transactions`, `GET /transactions/{id}`, `POST /anchor`, `GET /anchor/{hash}`, `POST /identity/create`, `GET /identity/{id}`, `POST /nft/mint`, `GET /nft/{id}`, `POST /nft/transfer`, `GET /balance/{address}`, `POST /bridge`, `GET /bridge/status/{id}`, `GET /contracts`, `POST /contracts/deploy`, `POST /contracts/execute`

### RG_Storage — 13 Routes
`GET /health`, `POST /upload`, `GET /files`, `GET /files/{id}`, `DELETE /files/{id}`, `GET /files/{id}/download`, `POST /files/{id}/share`, `GET /shared/{token}`, `GET /usage`, `POST /folders`, `GET /folders/{id}`, `DELETE /folders/{id}`, `PUT /files/{id}/move`

### RG_User_Memory — 15 Routes
`GET /health`, `POST /memories`, `GET /memories`, `GET /memories/{id}`, `DELETE /memories/{id}`, `POST /memories/search`, `GET /memories/stats`, `POST /memories/import`, `POST /memories/export`, `GET /tags`, `POST /tags`, `DELETE /tags/{id}`, `GET /collections`, `POST /collections`, `DELETE /collections/{id}`

### RG_Build_Service — 9 Routes
`GET /health`, `POST /build`, `GET /projects`, `GET /projects/{id}`, `DELETE /projects/{id}`, `GET /projects/{id}/files`, `GET /projects/{id}/files/{path}`, `PUT /projects/{id}/files/{path}`, `POST /projects/{id}/download`

### RG_Code_Execution — 8 Routes
`GET /health`, `GET /languages`, `GET /active`, `POST /execute` (code), `POST /execute` (terminal), `POST /start` (preview), `POST /stop` (preview), `GET /`

### RG_OpenClaw — 21 Routes
`GET /health`, `GET /manifest`, `GET /setup-guide`, `GET /status`, `GET /agents/openclaw`, `POST /agents/register`, `POST /agents/heartbeat`, `GET /connections`, `POST /connections`, `DELETE /connections/{id}`, `POST /connections/{id}/pause`, `POST /connections/{id}/resume`, `POST /relay/{agent_id}`, `GET /skills/available`, `POST /skills/execute`, `POST /skills/import`, `POST /memory/ingest`, `POST /memory/query`, `POST /marketplace/list`, `GET /governance/{agent_id}`, `POST /governance/enroll`

### RG_IDE_Platform — 57 Routes
Includes debugger (12), terminal (8), git (12), releases/downloads (6), stats (3), code execution, chat, build, health, track.

### RG_AST_analysis — 28 Routes
`POST /api/analyze`, `POST /api/analyze-multi`, `POST /api/upload`, `POST /api/compare`, `GET /api/analysis/{id}`, `GET /api/analysis/{id}/functions`, `GET /api/analysis/{id}/graph-structure`, `POST /api/analysis/{id}/full-pipeline`, `POST /api/analysis/{id}/governance`, `POST /api/analysis/{id}/trace`, `POST /api/analysis/{id}/filter`, `POST /api/analysis/{id}/agent/scan`, `POST /api/v1/scan/github`, `POST /api/v1/scan/github/multi`, `POST /api/v1/scan/upload`, `POST /api/v1/scan/save`, `GET /api/v1/analyses`, `GET /api/v1/analyses/{id}`, `DELETE /api/v1/analyses/{id}`, `GET /health`

### RG_Internal_Invarients_SIM — 78 Routes
RARA governance, invariants engine, kill switch, mutations, snapshots, DISD protocol, compliance (EU AI Act, SOC2), physics bridge, enhanced DISD, irreversibility epochs.

### RG_Users_Invarients_SIM — 25 Routes
State physics simulation, identity/memory/economic layers, entropy, galaxy simulation, agent spawning, platform data loading.

### RG_Registered_Users_Agentic_Chat — 6 Routes
`GET /health`, `GET /conversations`, `POST /conversations`, `GET /conversations/{id}`, `DELETE /conversations/{id}`, `POST /stream`

### RG_Public-Guest-Agentic_Chat — 3 Routes
`GET /health`, `GET /public/agentic-chat/health`, `POST /public/agentic-chat/stream`

---

## Frontend API Coverage Gap Analysis

### Migrated (45 API files in RGF_* modules)
| Old File | Migrated To | Status |
|----------|------------|--------|
| `auth.ts` | `RGF_Auth/api/auth.ts` | ✅ |
| `chat.ts` | `RGF_Resonant_Chat/api/chat.ts` | ✅ |
| `resonantChat.ts` | `RGF_Resonant_Chat/api/resonantChat.ts` | ✅ |
| `llm.ts` | `RGF_Resonant_Chat/api/llm.ts` | ✅ |
| `llmProviders.ts` | `RGF_Resonant_Chat/api/llmProviders.ts` | ✅ |
| `agentEngine.ts` | `RGF_Agentic_Assistant/api/agentEngine.ts` | ✅ |
| `ai.ts` | `RGF_Agentic_Assistant/api/ai.ts` | ✅ |
| `agents.ts` | `RGF_Agents/api/agents.ts` | ✅ |
| `agentApi.ts` | `RGF_Agents/api/agentApi.ts` | ✅ |
| `agentTeams.ts` | `RGF_Agents/api/agentTeams.ts` | ✅ |
| `autonomy.ts` | `RGF_Agents/api/autonomy.ts` | ✅ |
| `billing.ts` | `RGF_Dashboard/api/billing.ts` | ✅ |
| `billingComplete.ts` | `RGF_Dashboard/api/billingComplete.ts` | ✅ |
| `apiUsage.ts` | `RGF_Dashboard/api/apiUsage.ts` | ✅ |
| `daemons.ts` | `RGF_Dashboard/api/daemons.ts` | ✅ |
| `hashSphere.ts` | `RGF_Hash_Sphere/api/hashSphere.ts` | ✅ |
| `memory.ts` | `RGF_Hash_Sphere/api/memory.ts` | ✅ |
| `economicState.ts` | `RGF_Hash_Sphere/api/economicState.ts` | ✅ |
| `marketplace.ts` | `RGF_Marketplace/api/marketplace.ts` | ✅ |
| `crypto.ts` | `RGF_Marketplace/api/crypto.ts` | ✅ |
| `blockchain.ts` | `RGF_Marketplace/api/blockchain.ts` + `RGF_Network/api/blockchain.ts` | ✅ |
| `advancedBlockchain.ts` | `RGF_Network/api/advancedBlockchain.ts` | ✅ |
| `capabilities.ts` | `RGF_Network/api/capabilities.ts` | ✅ |
| `deployment.ts` | `RGF_Network/api/deployment.ts` | ✅ |
| `executions.ts` | `RGF_Network/api/executions.ts` | ✅ |
| `predictions.ts` | `RGF_Predictions/api/predictions.ts` | ✅ |
| `evidence.ts` | `RGF_Predictions/api/evidence.ts` | ✅ |
| `anchors.ts` | `RGF_Predictions/api/anchors.ts` | ✅ |
| `governance.ts` | `RGF_Protocol/api/governance.ts` | ✅ |
| `dsidProtocol.ts` | `RGF_Protocol/api/dsidProtocol.ts` | ✅ |
| `dsidpAccelerator.ts` | `RGF_Protocol/api/dsidpAccelerator.ts` | ✅ |
| `compliance.ts` | `RGF_Protocol/api/compliance.ts` | ✅ |
| `enterprise.ts` | `RGF_Public/api/enterprise.ts` | ✅ |
| `admin.ts` | `RGF_Admin/api/admin.ts` | ✅ |
| `ml.ts` | `RGF_Admin/api/ml.ts` | ✅ |
| `aiAudit.ts` | `RGF_Admin/api/aiAudit.ts` | ✅ |
| `aiReview.ts` | `RGF_Admin/api/aiReview.ts` | ✅ |
| `audit.ts` | `RGF_Admin/api/audit.ts` | ✅ |
| `finance.ts` | `RGF_Admin/api/finance.ts` | ✅ |
| `ideLoc.ts` | `RGF_Admin/api/ideLoc.ts` | ✅ |
| `code.ts` | `RGF_Code_Tools/api/code.ts` | ✅ |
| `git.ts` | `RGF_Code_Tools/api/git.ts` | ✅ |
| `github.ts` | `RGF_Code_Tools/api/github.ts` | ✅ |
| `lsp.ts` | `RGF_Code_Tools/api/lsp.ts` | ✅ |

### NOT Migrated (61 API files — need frontend work)

| Old File | Should Go To | Priority |
|----------|-------------|----------|
| `build.ts` | `RGF_Code_Tools` | 🔴 High |
| `projectBuilder.ts` | `RGF_Code_Tools` | 🔴 High |
| `debugger.ts` | `RGF_Code_Tools` | 🔴 High |
| `terminal.ts` | `RGF_Code_Tools` | 🔴 High |
| `ideService.ts` | `RGF_Code_Tools` | 🔴 High |
| `ideComplete.ts` | `RGF_Code_Tools` | 🟡 Medium |
| `dashboard.ts` | `RGF_Dashboard` | 🔴 High |
| `usage.ts` | `RGF_Dashboard` | 🔴 High |
| `usageTracking.ts` | `RGF_Dashboard` | 🟡 Medium |
| `stripe.ts` | `RGF_Dashboard` | 🔴 High |
| `ownerDashboard.ts` | `RGF_Admin` | 🔴 High |
| `settings.ts` | `RGF_Settings` | 🔴 High |
| `mfa.ts` | `RGF_Settings` or `RGF_Auth` | 🔴 High |
| `sso.ts` | `RGF_Auth` | 🔴 High |
| `userApiKeys.ts` | `RGF_Settings` | 🔴 High |
| `userPreferences.ts` | `RGF_Settings` | 🔴 High |
| `org.ts` | `RGF_Settings` | 🔴 High |
| `users.ts` | `RGF_Admin` | 🟡 Medium |
| `nft.ts` | `RGF_Marketplace` | 🔴 High |
| `marketplaceComplete.ts` | `RGF_Marketplace` | 🟡 Medium |
| `memoryComplete.ts` | `RGF_Hash_Sphere` | 🟡 Medium |
| `notifications.ts` | `RGF_Shell` (global) | 🔴 High |
| `skills.ts` | `RGF_Resonant_Chat` or `RGF_Agents` | 🟡 Medium |
| `plugins.ts` | `RGF_Agents` | 🟢 Low |
| `cognitive.ts` | `RGF_Network` | 🟡 Medium |
| `workflow.ts` | `RGF_Network` | 🟡 Medium |
| `workflowService.ts` | `RGF_Network` | 🟡 Medium |
| `workflows.ts` | `RGF_Network` | 🟡 Medium |
| `teams.ts` | `RGF_Agents` | 🟡 Medium |
| `storage.ts` | Shared / `RGF_Shell` | 🟡 Medium |
| `metrics.ts` | `RGF_Admin` | 🟡 Medium |
| `system.ts` | `RGF_Admin` | 🟡 Medium |
| `rag.ts` | `RGF_Hash_Sphere` | 🟡 Medium |
| `pricing.ts` | `RGF_Public` | 🔴 High |
| `contracts/agents.ts` | `RGF_Network` | 🟢 Low |
| `contracts/executions.ts` | `RGF_Network` | 🟢 Low |
| `contracts/index.ts` | `RGF_Network` | 🟢 Low |
| `universe.ts` | `RGF_Hash_Sphere` | 🟢 Low |
| `workspace.ts` | `RGF_Code_Tools` | 🟢 Low |
| `fastapiClient.ts` | Shared / deprecated | 🟢 Low |
| `apiHealthCheck.ts` | `RGF_Shell` | 🟢 Low |
| `index.ts` | Shared barrel export | 🟢 Low |
| `providers/*` (10 files) | `RGF_Resonant_Chat` or shared | 🟡 Medium |
| `websocket/*` (2 files) | Shared / `RGF_Shell` | 🔴 High |
| `hooks/*` (2 files) | Shared / `RGF_Shell` | 🟡 Medium |

### Summary
- **🔴 High priority missing: 21 files** — core functionality broken without these
- **🟡 Medium priority: 24 files** — secondary features
- **🟢 Low priority: 16 files** — nice to have, some may be deprecated

---

## Design System Issues

### `!important` Overrides (165 total)
| Module | Count | Action Needed |
|--------|-------|---------------|
| `RGF_Code_Tools` | 58 | Refactor to use specificity or CSS modules |
| `RGF_Public` | 53 | Refactor to use Design System tokens |
| `RGF_Resonant_Chat` | 20 | Remove overrides, use Design System |
| `RGF_Hash_Sphere` | 9 | Minor cleanup |
| `RGF_Settings` | 7 | Minor cleanup |
| `RGF_Marketplace` | 7 | Minor cleanup |
| `RGF_Network` | 5 | Minor cleanup |
| `RGF_Protocol` | 3 | Minor cleanup |
| `RGF_Agentic_Assistant` | 2 | Minor cleanup |
| `RGF_Rabbit` | 1 | Minor cleanup |

### Duplicate Token Definitions
- `RGF_Shell/src/styles/global.css` **duplicates ALL tokens** from `RGF_Design_System/src/tokens/css-variables.css`
- Should import from Design System instead of redefining

### Missing: Mobile/Desktop Breakpoint System
No centralized breakpoint tokens exist. Media queries are scattered (254 in RGF_Public alone). Need to add breakpoint tokens to Design System.

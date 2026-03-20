# Database Topology

> All database connections, managed instances, and service-to-database mappings.

## Managed PostgreSQL (DigitalOcean)

### Primary Cluster: `resonant-db`

- **Host**: `resonant-db-do-user-18031534-0.g.db.ondigitalocean.com`
- **Port**: `25060`
- **SSL**: Required (`?ssl=require`)
- **Default DB**: `defaultdb`
- **Driver**: `postgresql+asyncpg://` (async) or `postgresql://` (sync)

### ML Cluster: `ml-registry-db`

- **Host**: `ml-registry-db-do-user-18031534-0.g.db.ondigitalocean.com`
- **Port**: `25060`
- **SSL**: Required
- **Used by**: `ml_service` only

## Service-to-Database Mapping

All services on the primary cluster use the same host but with different logical databases/schemas.

| Env Variable | Service(s) | Database |
|-------------|-----------|----------|
| `DATABASE_URL` | `chat_service`, `gateway` | Primary — resonant chats, messages, resonance data |
| `AUTH_DATABASE_URL` | `auth_service` | Auth — users, sessions, BYOK keys, roles |
| `BILLING_DATABASE_URL` | `billing_service` | Billing — subscriptions, invoices, Stripe data |
| `CHAT_DATABASE_URL` | `chat_service` | Chat — conversations, messages, DSID |
| `MEMORY_DATABASE_URL` | `memory_service` | Memory — conversation memory, Hash Sphere |
| `USER_DATABASE_URL` | `user_service` | Users — profiles, preferences, organizations |
| `COGNITIVE_DATABASE_URL` | `cognitive_service` | Cognitive — analysis results, pipelines |
| `WORKFLOW_DATABASE_URL` | `workflow_service` | Workflows — definitions, runs, steps |
| `ED_DATABASE_URL` | `ed_service` | Education — courses, lessons, progress |
| `MARKETPLACE_DATABASE_URL` | `marketplace_service` | Marketplace — listings, categories, sellers |
| `BLOCKCHAIN_DATABASE_URL` | `blockchain_service` | Blockchain — identities, trust tiers, transactions |
| `AGENT_DATABASE_URL` | `agent_engine_service`, `rg_agentic_chat` | Agents — conversations, messages, teams, plans |
| `CRYPTO_DATABASE_URL` | `crypto_service` | Crypto — keys, receipts, signatures |
| `NOTIFICATION_DATABASE_URL` | `notification_service` | Notifications — templates, delivery logs |
| `CASCADE_DATABASE_URL` | `cascade_control_plane` | Cascade — control plane state |
| `ML_DATABASE_URL` | `ml_service` | ML registry (separate cluster) |
| `RABBIT_DATABASE_URL` | `rabbit_api_service` | Rabbit — communities, posts, comments, votes |

## Redis

| Container | Port | Purpose |
|-----------|------|---------|
| `shared_redis` | 6379 | Caching, rate limiting, state locks, pub/sub, session store |

- **Image**: Official Redis
- **Persistence**: Default (RDB snapshots)
- **Network**: `app-network` — accessible to all containers as `shared_redis:6379`
- **No authentication** (internal network only)

## Alembic Migrations

Services with Alembic database migrations:

| Service | Migration Directory | Command |
|---------|-------------------|---------|
| `auth_service` | `auth_service/alembic/` | `docker exec auth_service alembic upgrade head` |
| `chat_service` | `chat_service/alembic/` | `docker exec chat_service alembic upgrade head` |
| `rabbit_api_service` | `rabbit_api_service/alembic/` | `docker exec rabbit_api_service alembic upgrade head` |
| `agent_engine_service` | `agent_engine_service/alembic/` | `docker exec agent_engine_service alembic upgrade head` |
| `billing_service` | `billing_service/alembic/` | `docker exec billing_service alembic upgrade head` |

## Connection String Format

```
postgresql+asyncpg://<user>:<password>@<host>:25060/defaultdb?ssl=require
```

All services use `asyncpg` driver with SQLAlchemy async sessions.

## Backup

- **Managed by**: DigitalOcean automated backups
- **Retention**: 7 days (DigitalOcean default)
- **Point-in-time recovery**: Available via DigitalOcean console
- **Manual backup**: `pg_dump` via DigitalOcean console or direct connection

## Important Notes

1. All database URLs are in `.env.production` — **never commit this file**
2. The `AGENT_DATABASE_URL` is shared between `agent_engine_service` and `rg_agentic_chat` (same `resonant_agents` database)
3. `rg_public_guest_chat` does **not** use a database — it's stateless
4. `rg_ast_analysis`, `rg_internal_invarients_sim`, `rg_users_invarients_sim` use Redis only (no PostgreSQL)
5. `RG_IDE_Platform` (`ide_service`) does **not** use a database — LOC data is stored via the auth service

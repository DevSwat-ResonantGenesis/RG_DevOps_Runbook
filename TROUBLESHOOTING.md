# Troubleshooting

> Common issues, debugging techniques, and operational procedures.

## Quick Health Check

```bash
# Check all containers
sudo docker ps --format 'table {{.Names}}\t{{.Status}}' | sort

# Check for unhealthy containers
sudo docker ps --filter "health=unhealthy" --format '{{.Names}} {{.Status}}'

# Check a specific container's logs
sudo docker logs -f --tail 100 <container_name>

# Check resource usage
sudo docker stats --no-stream --format 'table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}'
```

## Common Issues

### 1. SSE Streaming Not Working (IDE completions, agentic chat)

**Symptom**: IDE chat stuck at "Thinking...", responses truncated, only partial data received.

**Root cause**: Nginx `proxy_http_version` not set to 1.1. HTTP/1.0 doesn't support chunked transfer encoding.

**Fix**: Ensure `/etc/nginx/sites-enabled/dev-swat.com` has:
```nginx
location ^~ /api/v1/ {
    proxy_http_version 1.1;
    proxy_set_header Connection "";
    proxy_buffering off;
    proxy_cache off;
    proxy_read_timeout 300s;
    proxy_send_timeout 300s;
    proxy_pass http://localhost:8001;
}
```

Then: `sudo nginx -s reload`

### 2. Container Won't Start

```bash
# Check logs for the error
sudo docker logs --tail 50 <container_name>

# Common causes:
# - Missing env var in .env.production
# - Database connection refused (check DB host is reachable)
# - Port conflict (another container on same port)
# - Build context path doesn't exist

# Rebuild from scratch
sudo docker compose -f docker-compose.unified.yml build --no-cache <service_name>
sudo docker compose -f docker-compose.unified.yml up -d <service_name>
```

### 3. Database Connection Refused

**Symptom**: Container logs show `ConnectionRefusedError` or `could not connect to server`.

**Check**:
```bash
# Verify DB is reachable from server
nc -zv resonant-db-do-user-18031534-0.g.db.ondigitalocean.com 25060

# Verify env var is correct
grep DATABASE_URL /home/deploy/genesis2026_production_backend/.env.production
```

**Fix**: Check DigitalOcean console for managed DB status. May need to add server IP to trusted sources.

### 4. Volume Mount Module Not Found

**Symptom**: `ModuleNotFoundError: No module named 'rg_llm'` or `rg_tool_registry`.

**Check**:
```bash
# Verify source directory exists
ls /home/deploy/RG_UnifiedLLMClient/src/rg_llm/
ls /home/deploy/RG_Unified_Tool_Registry/rg_tool_registry/

# Verify PYTHONPATH is set
sudo docker exec <container_name> env | grep PYTHONPATH

# Verify mount is present
sudo docker inspect <container_name> | grep -A5 "Mounts"
```

**Fix**: If directory missing, clone the repo. If PYTHONPATH missing, add to docker-compose.

### 5. Gateway Returns 502 Bad Gateway

**Symptom**: API calls return 502.

**Check**:
```bash
# Is the target service running?
sudo docker ps | grep <service_name>

# Can the gateway reach it?
sudo docker exec gateway curl -s http://<service_name>:<port>/health

# Check gateway logs
sudo docker logs --tail 50 gateway
```

**Fix**: Restart the target service. If persistent, check docker network connectivity.

### 6. Git Pull Overwrites docker-compose

**Problem**: `git pull` on the server overwrites manual changes to `docker-compose.unified.yml` (e.g., service blocks added only on server).

**Prevention**:
```bash
# Before pulling, stash local changes
git stash
git pull origin main
git stash pop
```

**Better fix**: Commit all docker-compose changes to git so there are no local-only modifications.

### 7. Frontend Not Updating After Deploy

**Check**:
```bash
# Verify build succeeded
ls -la /var/www/frontend/index.html

# Check if Nginx is serving stale cache
sudo nginx -s reload

# Verify the correct git branch
cd /home/deploy/genesis2026_frontend_production_2 && git log -1
```

**Fix**: Run the full frontend deploy sequence:
```bash
cd /home/deploy/genesis2026_frontend_production_2
git fetch origin && git reset --hard origin/main
npm run build
sudo rsync -a --delete dist/ /var/www/frontend/
sudo nginx -s reload
```

### 8. Out of Disk Space

```bash
# Check disk usage
df -h /

# Clean up Docker
sudo docker system prune -f         # Remove unused images/containers
sudo docker builder prune -f        # Remove build cache

# Check largest directories
du -sh /home/deploy/genesis2026_production_backend/* | sort -rh | head -10
```

### 9. High Memory Usage

```bash
# Check which containers use the most memory
sudo docker stats --no-stream --format '{{.Name}}\t{{.MemUsage}}' | sort -k2 -rh | head -10

# Restart memory-heavy containers
sudo docker compose -f docker-compose.unified.yml restart <service_name>
```

## Log Access

```bash
# Real-time logs for any service
sudo docker logs -f --tail 100 <container_name>

# Search logs for errors
sudo docker logs <container_name> 2>&1 | grep -i "error\|exception\|traceback" | tail -20

# Nginx access logs
sudo tail -f /var/log/nginx/access.log

# Nginx error logs
sudo tail -f /var/log/nginx/error.log
```

## Health Check Endpoints

Every service exposes a health endpoint:

| Service | Health URL |
|---------|-----------|
| Gateway | `curl http://localhost:8001/health` |
| Auth | `docker exec gateway curl http://auth_service:8000/health` |
| Chat | `docker exec gateway curl http://chat_service:8000/health` |
| Memory | `docker exec gateway curl http://memory_service:8000/health` |
| Agentic Chat | `docker exec gateway curl http://rg_agentic_chat:8000/health` |
| Guest Chat | `docker exec gateway curl http://rg_public_guest_chat:8010/health` |
| AST Analysis | `docker exec gateway curl http://rg_ast_analysis:8000/health` |
| IDE Platform | `docker exec gateway curl http://ide_service:8080/health` |

## Emergency Procedures

### Kill Switch (RARA)

```bash
# Freeze all agent operations
curl -X POST http://localhost:8001/api/v1/rara/control/freeze

# Emergency stop
curl -X POST http://localhost:8001/api/v1/rara/control/emergency-stop
```

### Full System Restart

```bash
cd /home/deploy/genesis2026_production_backend
sudo docker compose -f docker-compose.unified.yml down
sudo docker compose -f docker-compose.unified.yml up -d
```

> **Note**: This will cause ~30s of downtime while all containers start up.

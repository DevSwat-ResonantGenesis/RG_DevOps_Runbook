# Volume Mounts

> Shared modules mounted into Docker containers as read-only volumes.

## rg_llm (Unified LLM Client)

**Source**: `/home/deploy/RG_UnifiedLLMClient/src/rg_llm`
**Mount**: `/app/rg_llm:ro`
**GitHub**: [`RG_UnifiedLLMClient`](https://github.com/DevSwat-ResonantGenesis/RG_UnifiedLLMClient)

### Containers Using rg_llm

| Container | docker-compose volume line |
|-----------|--------------------------|
| `agent_engine_service` | `/home/deploy/RG_UnifiedLLMClient/src/rg_llm:/app/rg_llm:ro` |
| `chat_service` | `/home/deploy/RG_UnifiedLLMClient/src/rg_llm:/app/rg_llm:ro` |
| `rg_agentic_chat` | `/home/deploy/RG_UnifiedLLMClient/src/rg_llm:/app/rg_llm:ro` |
| `rg_public_guest_chat` | `/home/deploy/RG_UnifiedLLMClient/src/rg_llm:/app/rg_llm:ro` |

### How it works

All containers set `PYTHONPATH=/app`, so Python imports work as:
```python
from rg_llm import UnifiedLLMClient
from rg_llm.providers import GroqProvider, OpenAIProvider
```

### Updating rg_llm

```bash
cd /home/deploy/RG_UnifiedLLMClient && git pull origin main
cd /home/deploy/genesis2026_production_backend
sudo docker compose -f docker-compose.unified.yml restart agent_engine_service chat_service rg_agentic_chat rg_public_guest_chat
```

No rebuild needed — volume mounts reflect file changes on restart.

---

## rg_tool_registry (Unified Tool Registry)

**Source**: `/home/deploy/RG_Unified_Tool_Registry/rg_tool_registry`
**Mount**: `/app/rg_tool_registry:ro`
**GitHub**: [`RG_Unified_Tool_Registry-Observability_Module`](https://github.com/DevSwat-ResonantGenesis/RG_Unified_Tool_Registry-Observability_Module)

### Containers Using rg_tool_registry

| Container | docker-compose volume line |
|-----------|--------------------------|
| `agent_engine_service` | `/home/deploy/RG_Unified_Tool_Registry/rg_tool_registry:/app/rg_tool_registry:ro` |
| `rg_agentic_chat` | `/home/deploy/RG_Unified_Tool_Registry/rg_tool_registry:/app/rg_tool_registry:ro` |

### How it works

```python
from rg_tool_registry.builtin_tools import build_registry
from rg_tool_registry.observability import ToolObserver
from rg_tool_registry.builder import build_guest_registry
```

### Updating rg_tool_registry

```bash
cd /home/deploy/RG_Unified_Tool_Registry && git pull origin main
cd /home/deploy/genesis2026_production_backend
sudo docker compose -f docker-compose.unified.yml restart agent_engine_service rg_agentic_chat
```

---

## Important Notes

1. **Read-only**: All volume mounts use `:ro` — containers cannot modify shared modules
2. **No rebuild needed**: Volume mounts are live file mappings. Just restart the container after updating the source.
3. **PYTHONPATH=/app**: All consuming containers must have this set in their Dockerfile or docker-compose environment
4. `rg_public_guest_chat` does **NOT** use `rg_tool_registry` — its 14 tools are defined locally in `app/tools.py`
5. Server path for tool registry is `/home/deploy/RG_Unified_Tool_Registry` (note: no `-Observability_Module` suffix on disk)

# Guía Rápida: Instalación de Módulos MCP en Odoo 19

## 1. Copiar Módulos
Copiar las 3 carpetas al directorio de addons del otro proyecto:
- `llm/`
- `llm_tool/`
- `llm_mcp_server/`

## 2. Instalar Dependencias Python
```bash
pip install pydantic>=2.0.0 mcp
```

O dentro del contenedor Docker:
```bash
docker exec -it <container_name> pip install pydantic>=2.0.0 mcp --break-system-packages
```

## 3. Actualizar Lista de Módulos
En Odoo: **Apps** → Click en ⚙️ → **Update Apps List**

## 4. Instalar Módulos (en orden)
1. **LLM Integration Base** (`llm`)
2. **LLM Tool** (`llm_tool`) 
3. **LLM MCP Server** (`llm_mcp_server`)

## 5. Generar API Key
**User menu** (arriba derecha) → **My Profile** → **Account Security** → **New API Key**

Copiar la key generada.

## 6. Configurar Cliente MCP

### Claude Code (desde WSL/Linux):
```bash
claude mcp add-json odoo-llm '{
  "type": "stdio",
  "command": "npx",
  "args": ["-y", "mcp-remote", "http://localhost:8069/mcp",
           "--header", "Authorization: Bearer TU_API_KEY"],
  "env": {"MCP_TRANSPORT": "streamable-http"}
}'
```

### Claude Desktop (Windows):
Editar `~/.config/claude_desktop/claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "odoo-llm": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "mcp-remote", "http://IP_SERVIDOR:8069/mcp",
               "--header", "Authorization: Bearer TU_API_KEY"],
      "env": {"MCP_TRANSPORT": "streamable-http"}
    }
  }
}
```

**Nota:** En Windows usa la IP del servidor en lugar de `localhost`.

## 7. Verificar
Reiniciar el cliente MCP y preguntar: *"¿Qué herramientas tienes disponibles?"*

---

## Notas Importantes
- **Entorno desarrollo:** MCP puede no funcionar con servidor Werkzeug
- **Producción:** Funcionará correctamente con nginx/Gunicorn
- Los módulos requieren Odoo 19.0+

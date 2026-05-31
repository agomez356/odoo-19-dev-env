# odoo-19-dev-env

Local development environment for running **Odoo 19.0 Community** with the [`apexive/odoo-llm`](https://github.com/apexive/odoo-llm) MCP modules.

Used to develop and validate the port of `llm`, `llm_tool`, and `llm_mcp_server` to Odoo 19.0 before contributing upstream — see [apexive/odoo-llm#252](https://github.com/apexive/odoo-llm/pull/252).

## What's included

- `docker-compose.yml` — Odoo 19.0 + PostgreSQL 15, ready to run
- `config/odoo.conf` — development config with debug mode and extra-addons path
- `odoo-llm/` — git submodule pointing to [apexive/odoo-llm](https://github.com/apexive/odoo-llm)
- `INSTALL_MCP_MODULES.md` — step-by-step guide to install the modules and connect Claude Code / Claude Desktop

## Quick start

```bash
git clone --recurse-submodules https://github.com/agomez356/odoo-19-dev-env
cd odoo-19-dev-env
docker compose up -d
```

Odoo will be available at `http://localhost:8069`.

## Install MCP modules

See [INSTALL_MCP_MODULES.md](INSTALL_MCP_MODULES.md) for the full guide, including how to connect:

- **Claude Code** (Linux/WSL) via `mcp-remote`
- **Claude Desktop** (Windows/Mac) via `claude_desktop_config.json`
- **Codex** and other MCP-compatible clients

## Requirements

- Docker + Docker Compose
- The `llm` → `llm_tool` → `llm_mcp_server` modules must be installed in that order

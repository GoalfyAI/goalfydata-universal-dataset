# GoalfyData — Codex Plugin

OpenAI Codex plugin for connecting to the GoalfyData universal dataset service.

## Features

- Build structured datasets (CSV/Excel/API/scripts)
- Data analysis (multi-turn SQL queries, aggregation, trend comparison)
- Import, query, and share datasets
- Configure scheduled sync
- Deploy data apps to the public internet

## Prerequisites

1. **GoalfyData API Token**: Create one at https://goalfydata.ai/settings
2. **uds-cli**:

   macOS / Linux:
   ```bash
   curl -fsSL https://goalfyagent-public.s3.amazonaws.com/dataset-uds/install.sh | sh
   source ~/.zshrc  # or source ~/.bashrc
   uds-cli login --token gfk_xxx --api-url https://api.goalfydata.ai
   ```

   Windows (PowerShell):
   ```powershell
   irm https://goalfyagent-public.s3.amazonaws.com/dataset-uds/install.ps1 | iex
   uds-cli login --token gfk_xxx --api-url https://api.goalfydata.ai
   ```

## Installation

Make sure you have completed the prerequisites above (Token creation + uds-cli installed and logged in) before installing.

### Option 1: Via marketplace

```bash
codex plugin marketplace add GoalfyAI/goalfydata
codex plugin add goalfydata@goalfydata
```

You can also search and install via the Plugins interface in Codex Desktop.

### Option 2: Manual configuration

Add the MCP configuration to `~/.codex/config.toml`:

```toml
[mcp_servers.goalfydata-mcp]
url = "https://mcp.goalfydata.ai/mcp"
bearer_token_env_var = "GOALFY_UDS_API_TOKEN"
```

## Authentication

Codex Desktop is an Electron application and does not inherit terminal environment variables. You need to configure the token in `~/.codex/.env`:

```bash
# ~/.codex/.env
GOALFY_UDS_API_TOKEN=gfk_your_token_here
```

Restart Codex Desktop after configuration for it to take effect.

Codex CLI (terminal) can also use standard shell export:

```bash
export GOALFY_UDS_API_TOKEN="gfk_your_token_here"
```

MCP tools and uds-cli share the same token system.

## Verification

After restarting Codex, confirm that `goalfydata-mcp` is connected and the tool list contains 20 tools (`uds_query`, `uds_dataset_manage`, etc.).

If connection fails:
- Confirm `GOALFY_UDS_API_TOKEN` is configured in `~/.codex/.env`
- For manual configuration users, check that `bearer_token_env_var` in `~/.codex/config.toml` is correct
- Confirm the token is valid (verify in the console)
- Fully quit and restart Codex

## Update

### Plugin update

**Marketplace installation**: Refresh the marketplace index first, then reinstall:

```bash
codex plugin marketplace upgrade goalfydata
codex plugin remove goalfydata@goalfydata
codex plugin add goalfydata@goalfydata
```

**Manual configuration**: MCP configuration does not need updating (it points to the remote service). If you need to update Skill files, pull and overwrite.

### uds-cli update

```bash
uds-cli self-update
```

## Usage

Once the plugin is loaded, Codex automatically activates skills based on the task. You can also invoke manually:

```
/goalfydata Help me create a dataset
```

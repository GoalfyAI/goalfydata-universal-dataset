# GoalfyData — Claude Code Plugin

Claude Code plugin for connecting to the GoalfyData universal dataset service.

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

### Option 1: Via marketplace (recommended)

Marketplace installation automatically handles plugin structure, MCP configuration, and Skill loading -- no need to manually copy files.

```bash
claude plugin marketplace add GoalfyAI/goalfydata
claude plugin install goalfydata@goalfydata
```

### Option 2: Download ZIP

Download [goalfydata-claude-code.zip](https://github.com/GoalfyAI/goalfydata/raw/main/claude-code/goalfydata-claude-code.zip), extract, and copy to the plugin directory:

```bash
unzip goalfydata-claude-code.zip -d ~/.claude/skills/goalfydata
```

### Option 3: Git clone

```bash
git clone https://github.com/GoalfyAI/goalfydata.git
cp -r goalfydata/claude-code ~/.claude/skills/goalfydata
```

> **Note: Copy the entire `claude-code/` directory, not just `skills/`. It contains `.claude-plugin/`, `.mcp.json`, and `skills/` — missing any will cause failures.**

### Option 4: Local development testing

```bash
claude --plugin-dir ./claude-code
```

After installation, restart Claude Code and the plugin will automatically load the MCP server.

## Authentication

MCP connection requires the `GOALFY_UDS_API_TOKEN` environment variable. Claude Code supports `${VAR}` expansion and automatically injects it into request headers.

**Configuration methods (by priority, choose one)**:

1. **Claude Code settings.json (recommended, works with all launch methods)**:
   Add to the `env` section in `~/.claude/settings.json`:
   ```json
   {
     "env": {
       "GOALFY_UDS_API_TOKEN": "gfk_your_token_here"
     }
   }
   ```

2. **Shell environment variable (only works when launching `claude` from terminal)**:
   ```bash
   export GOALFY_UDS_API_TOKEN="gfk_your_token_here"  # Add to ~/.zshrc or ~/.bashrc
   ```

   Note: When launching Claude Code from a desktop app or IDE, shell config files are not sourced, so this method will not work.

## Verification

After restarting Claude Code, type `/mcp` and confirm that `goalfydata-mcp` shows status connected + 20 tools.

If connection fails:
- Confirm `GOALFY_UDS_API_TOKEN` is configured in `~/.claude/settings.json`
- Confirm the token has a valid `gfk_` prefix
- Fully quit and restart Claude Code

## Update

### Plugin update

**Marketplace installation (auto-update)**: Marketplace plugins automatically check for updates when Claude Code starts. You can also update manually:

```bash
claude plugin update goalfydata@goalfydata
```

**Manual installation**: Re-download the latest [ZIP](https://github.com/GoalfyAI/goalfydata/raw/main/claude-code/goalfydata-claude-code.zip) and overwrite, or pull with git:

```bash
unzip -o goalfydata-claude-code.zip -d ~/.claude/skills/goalfydata
```

After updating, run `/reload-plugins` in your session to reload, or restart Claude Code.

### uds-cli update

```bash
uds-cli self-update
```

## Usage

Once the plugin is loaded, Claude Code automatically activates skills based on the task. You can also invoke manually:

```
/goalfydata Help me create a dataset
```

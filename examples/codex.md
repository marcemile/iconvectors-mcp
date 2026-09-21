# OpenAI Codex

## Prerequisites

Use local Codex on Windows with IconVectors 2.0 already running. Confirm that the installed `IconVectorsMcp.exe` exists. This setup uses stdio; Codex launches the process.

## Configuration

Add this table to `%USERPROFILE%\.codex\config.toml`. A trusted project may instead use `.codex/config.toml`. Merge with existing configuration.

```toml
[mcp_servers.iconvectors]
command = 'C:\Program Files\Axialis\IconVectors\IconVectorsMcp.exe'
args = ['--port', '61337']
cwd = 'C:\Program Files\Axialis\IconVectors'
startup_timeout_sec = 20
tool_timeout_sec = 120
default_tools_approval_mode = "prompt"
```

Adapt both paths to your installation and match the application's port. Keep tool approval prompts enabled.

## Verify

Run `codex mcp list`, then inspect `/mcp` in a Codex session. Ask for `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace`. Confirm the application and document identity before editing. Start a new session if configuration changes have not loaded.

## Platforms and reference

These instructions cover native Windows.

Reference: [official IconVectors Codex guide](https://iconvectors.io/help/using-iconvectors-with-codex-openai.html). A WSL session does not automatically share the desktop application's local connection. See [troubleshooting](../docs/troubleshooting.md) for connection and discovery issues.

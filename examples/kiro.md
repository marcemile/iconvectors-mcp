# Kiro

## Prerequisites

Use Kiro locally on Windows with IconVectors 2.0 running and `IconVectorsMcp.exe` present in its installation directory.

## Configuration

Use `.kiro/settings/mcp.json` for a workspace or `%USERPROFILE%\.kiro\settings\mcp.json` for user scope:

```json
{
  "mcpServers": {
    "iconvectors": {
      "command": "C:\\Program Files\\Axialis\\IconVectors\\IconVectorsMcp.exe",
      "args": ["--port", "61337"],
      "disabled": false,
      "autoApprove": [],
      "disabledTools": []
    }
  }
}
```

Merge existing entries, adapt the path and match the application's port. Workspace entries take precedence. Saving the configuration reconnects Kiro. Leave automatic approval empty initially.

## Verify

In the IDE, inspect the MCP servers view. In the CLI, use `kiro-cli mcp list`, `/mcp` and `/tools`. Ask for `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace` before editing.

## Platforms and reference

These instructions cover native Windows.

Reference: [official IconVectors Kiro guide](https://iconvectors.io/help/using-iconvectors-with-kiro.html). See [troubleshooting](../docs/troubleshooting.md) for connection and discovery issues.

# Gemini CLI

## Prerequisites

Run Gemini CLI on the same Windows machine as IconVectors 2.0. Keep IconVectors open and confirm `IconVectorsMcp.exe` exists.

## Configuration

Merge into `.gemini/settings.json` for project scope or `%USERPROFILE%\.gemini\settings.json` for user scope:

```json
{
  "mcpServers": {
    "iconvectors": {
      "command": "C:\\Program Files\\Axialis\\IconVectors\\IconVectorsMcp.exe",
      "args": ["--port", "61337"],
      "trust": false
    }
  }
}
```

Adapt the path and match the application's port. Keep `trust` false for tool-call confirmation. Workspace trust is separate; an untrusted workspace does not start stdio servers.

## Verify

Run `gemini mcp list`. In a session, inspect `/mcp` and `/tools`; use `/mcp reload` after a configuration change. Ask for `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace` before editing.

## Platforms and reference

These instructions cover native Windows.

Reference: [official IconVectors Gemini CLI guide](https://iconvectors.io/help/using-iconvectors-with-gemini-cli.html). See [troubleshooting](../docs/troubleshooting.md) for connection and discovery issues.

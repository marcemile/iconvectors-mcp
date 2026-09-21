# Cursor

## Prerequisites

Use Cursor locally on Windows with IconVectors 2.0 open. Confirm that `IconVectorsMcp.exe` exists in the installation directory.

## Configuration

Use `.cursor/mcp.json` for a project or `%USERPROFILE%\.cursor\mcp.json` for user scope. Merge this entry into existing configuration:

```json
{
  "mcpServers": {
    "iconvectors": {
      "type": "stdio",
      "command": "C:\\Program Files\\Axialis\\IconVectors\\IconVectorsMcp.exe",
      "args": ["--port", "61337"]
    }
  }
}
```

Adapt the path and match the application's port. Enable the server under Cursor's **Tools & MCP** settings. Cursor starts the process; reload the window if a saved configuration is not detected.

## Verify

Check that the server is enabled and tools appear in the MCP view. Ask for `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace`. Inspect document and selection before editing.

## Platforms and reference

These instructions cover native Windows.

Reference: [official IconVectors Cursor guide](https://iconvectors.io/help/using-iconvectors-with-cursor.html). See [troubleshooting](../docs/troubleshooting.md) for connection and discovery issues.

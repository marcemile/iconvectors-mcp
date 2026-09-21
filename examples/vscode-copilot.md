# VS Code / GitHub Copilot

## Prerequisites

Use local VS Code on Windows with GitHub Copilot access and IconVectors 2.0 running. Organizational MCP policy may restrict access. Confirm `IconVectorsMcp.exe` exists.

## Configuration

Create or merge into `.vscode/mcp.json`:

```json
{
  "servers": {
    "iconvectors": {
      "type": "stdio",
      "command": "C:\\Program Files\\Axialis\\IconVectors\\IconVectorsMcp.exe",
      "args": ["--port", "61337"]
    }
  }
}
```

Adapt the path and port. For user scope, use **MCP: Open User Configuration**. Start the server using **MCP: List Servers** or the configuration editor controls, then open Copilot Chat in **Agent** mode.

## Verify

Inspect the server status and Chat tool picker. Ask for `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace`. Retain these discovery tools when selecting a smaller task-specific tool set.

If the enabled-tool limit is exceeded, deselect unrelated tools in the picker. For diagnostics, select the server under **MCP: List Servers**, then **Show Output**.

## Platforms and reference

These instructions cover native Windows.

Reference: [official IconVectors VS Code / GitHub Copilot guide](https://iconvectors.io/help/using-iconvectors-with-vscode-copilot.html). [Copilot CLI](github-copilot-cli.md) uses a separate configuration. See [troubleshooting](../docs/troubleshooting.md) for connection and discovery issues.

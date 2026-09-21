# GitHub Copilot CLI

## Prerequisites

Run Copilot CLI on the same Windows machine as IconVectors 2.0. Keep IconVectors open and confirm `IconVectorsMcp.exe` exists.

## Configuration

Merge into `%USERPROFILE%\.copilot\mcp-config.json`:

```json
{
  "mcpServers": {
    "iconvectors": {
      "type": "stdio",
      "command": "C:\\Program Files\\Axialis\\IconVectors\\IconVectorsMcp.exe",
      "args": ["--port", "61337"],
      "tools": ["*"]
    }
  }
}
```

Adapt the executable path and application port. The `tools` entry exposes the catalog; it does not grant blanket tool-call approval. Keep permission prompts enabled.

This client does not directly read VS Code's `.vscode/mcp.json`.

## Verify

Run `copilot mcp list` and `copilot mcp get iconvectors`. In a session, use `/mcp show iconvectors` or `/mcp reload`. Ask for `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace` before editing.

## Platforms and reference

These instructions cover native Windows.

Reference: [official IconVectors GitHub Copilot CLI guide](https://iconvectors.io/help/using-iconvectors-with-github-copilot-cli.html). This setup uses the local CLI; the hosted coding agent cannot directly reach the desktop application. See [troubleshooting](../docs/troubleshooting.md) for connection and discovery issues.

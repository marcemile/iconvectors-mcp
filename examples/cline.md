# Cline

## Prerequisites

Run the Cline extension or CLI locally on Windows. Open IconVectors 2.0 and confirm `IconVectorsMcp.exe` exists.

## Configuration

In the extension, open **MCP Servers > Configure > Configure MCP Servers** and merge:

```json
{
  "mcpServers": {
    "iconvectors": {
      "command": "C:\\Program Files\\Axialis\\IconVectors\\IconVectorsMcp.exe",
      "args": ["--port", "61337"],
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Adapt the path and port. For the CLI, prefer the `cline mcp` wizard and inspect its result with `cline config mcp`. The IconVectors 2.00 guide records conflicting Cline documentation about settings locations. It reports `%USERPROFILE%\.cline\data\settings\cline_mcp_settings.json` as the default for the CLI version it examined, with `CLINE_MCP_SETTINGS_PATH` as an override. Verify the effective location in your installed Cline version; do not assume automatic project-file discovery.

Start CLI sessions with `cline --auto-approve false` to retain approval prompts.

## Verify

Inspect the extension's MCP view or run `cline config mcp`. Ask for `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace`. Client support does not guarantee every model provider supports the same tools.

## Platforms and reference

These instructions cover native Windows.

Reference: [official IconVectors Cline guide](https://iconvectors.io/help/using-iconvectors-with-cline.html). See [troubleshooting](../docs/troubleshooting.md) for connection and discovery issues.

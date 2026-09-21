# Claude Code

## Prerequisites

Use Claude Code locally on Windows. Start IconVectors 2.0 normally and confirm `IconVectorsMcp.exe` exists in its installation directory.

## Configuration

Register a user-scoped stdio server from PowerShell:

```powershell
claude mcp add --transport stdio --scope user iconvectors -- "C:\Program Files\Axialis\IconVectors\IconVectorsMcp.exe" --port 61337
```

Replace the path or port if required. Claude Code launches the server process itself.

User-scoped configuration is stored in `~/.claude.json`. Shared project servers use `.mcp.json`. The command above registers the user-scoped server; review any project configuration separately before approving it.

## Verify

Run `claude mcp list` and inspect `/mcp` in Claude Code. Ask for `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace`. Verify the intended document before editing.

## Platforms and reference

These instructions cover native Windows.

Reference: [official IconVectors Claude guide](https://iconvectors.io/help/using-iconvectors-with-claude-anthropic.html). This page covers Claude Code; the official guide also describes the Claude Desktop extension. See [troubleshooting](../docs/troubleshooting.md) for connection and discovery issues.

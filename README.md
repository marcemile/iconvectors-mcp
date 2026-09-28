# Axialis IconVectors MCP

> This repository contains documentation and configuration examples for the MCP integration available in Axialis IconVectors. It does not contain the IconVectors application source code.

## Introduction

Axialis IconVectors 2.0 exposes SVG editing capabilities through the Model Context Protocol (MCP). Compatible AI coding agents can inspect and operate the running desktop application and its SVG documents.

IconVectors is proprietary software, installed separately. This documentation repository is named `iconvectors-mcp`.

On Windows, the MCP client launches `IconVectorsMcp.exe` as a separate local process and communicates with it over **stdio**. Start IconVectors normally first and leave it running. The companion connects to the application over local TCP at `127.0.0.1:61337` by default. This application connection is not an HTTP MCP URL.

```text
AI coding agent
       |
       v
Model Context Protocol (local stdio)
       |
       v
Axialis IconVectors
       |
       v
SVG document
```

This diagram describes the user workflow only.

## Supported AI coding agents

The official IconVectors documentation provides Windows setup instructions for all eight clients below. Each guide includes the configuration location, a minimal example and connection checks.

| Client | Configuration guide |
| --- | --- |
| OpenAI Codex | [Codex](examples/codex.md) |
| Claude Code | [Claude Code](examples/claude-code.md) |
| Cursor | [Cursor](examples/cursor.md) |
| VS Code / GitHub Copilot | [VS Code / GitHub Copilot](examples/vscode-copilot.md) |
| Gemini CLI | [Gemini CLI](examples/gemini-cli.md) |
| Kiro | [Kiro](examples/kiro.md) |
| Cline | [Cline](examples/cline.md) |
| GitHub Copilot CLI | [GitHub Copilot CLI](examples/github-copilot-cli.md) |

## What can an agent do?

The MCP tools cover these areas:

| Area | Operations |
| --- | --- |
| Application state | Check connectivity, application information, capabilities and active workspace. |
| SVG inspection | Read document information and SVG content; inspect DOM elements, selection and styles. |
| Selection and editing | Select elements; create shapes and paths; change attributes, fills, strokes and transforms. |
| Document operations | Create or open documents, save changes and export requested output. |
| Repetitive editing | Align, duplicate, group, recolor and apply supported path operations. |
| Cleanup | Inspect SVG cleanup findings and explicitly request the supported conservative fixes. |
| Preview and history | Render previews; use Undo/Redo and transactions for supported document edits. |
| Explorer navigation | Inspect the active folder, entries and selection; navigate to folders, parents or children, and move through folder history. |
| Explorer file operations | Create and rename direct-child folders; delete an empty direct-child folder; copy selected SVG file paths to the OS clipboard; paste, duplicate and group SVG files. |
| Explorer batch operations | Plan and apply palette changes, icon resizing and stroke changes to selected SVG files. |

Available capabilities depend on the installed IconVectors version. Use MCP tool discovery and `app_getCapabilities`; obtain exact arguments from the installed tool schemas rather than inferring them from these summaries. A command being available in the user interface does not guarantee that an MCP tool exposes it.

Document Undo does not reverse saving/exporting or Explorer filesystem changes. Creating, opening or replacing a document clears document Undo history. Review targets and destinations before requesting these operations. Explorer batch operations require a plan, review of that plan, then application of its returned identifier. See the [official MCP guide](https://iconvectors.io/help/mcp-integration.html) for the documented limits.

Style setters also update application drawing defaults. For an edit confined to one object, inspect its current style and use an explicit element target with a DOM attribute or style patch.

## Requirements

- An installed, running copy of IconVectors 2.0 with its matching MCP executable.
- A local MCP client able to launch a stdio process on the same machine.
- Permission to use the client and its MCP integration; organization policy may restrict this.
- The correct executable path and application port.

See the [official download page](https://iconvectors.io/download.html) for current Windows, macOS and Linux releases and requirements. The configuration examples in this repository cover **native Windows** integration.

## Getting started

For native Windows:

1. Install IconVectors using the official download page.
2. Start IconVectors normally and leave it open.
3. Confirm that `IconVectorsMcp.exe` exists in the installation directory.
4. Add the server using the guide for your client.
5. Let the client start the MCP process. It should discover tools from that process.
6. Ask the agent to call `app_ping`, `app_getInfo`, `app_getCapabilities` and `app_get_workspace`.
7. Check that the application, workspace and document are the intended targets before requesting an edit.

## Client configuration

The guides use this normal Windows installation path:

```text
C:\Program Files\Axialis\IconVectors\IconVectorsMcp.exe
```

The examples explicitly pass the documented default application port:

```json
["--port", "61337"]
```

Replace the executable path if your installation differs. If the application's `Options/McpPort` setting has changed, use the same port in the client configuration. Preserve existing server entries when adding IconVectors.

No custom host argument is needed for this local default setup.

Use the client-specific file format: Codex uses TOML, VS Code uses a `servers` JSON object, and several other clients use `mcpServers`. The installed `iconvectors-mcp-tools.json` is a tool reference, not a client connection configuration.

## Example workflow

Begin with a read-only request:

```text
Use IconVectors MCP to check the connection and report the application
version, active workspace, current document and selection. Do not edit yet.
```

After reviewing the result, request a bounded change:

```text
In the current Editor document, inspect the selected object's current style.
Use dom_setStyle with its explicit target to patch its fill to #2563EB.
Leave other properties and drawing defaults unchanged. Reinspect the object
and show a preview. Do not save yet.
```

Finally, explicitly request saving or exporting to your chosen local destination. Reinspect object targets after structural changes. Use a history transaction only for compatible document edits, with the transaction identifier returned by the tool.

## Documentation

- [Official MCP integration guide](https://iconvectors.io/help/mcp-integration.html)
- [Client configuration guides](#supported-ai-coding-agents)
- [Troubleshooting](docs/troubleshooting.md)
- [IconVectors product information](https://www.axialis.com/iconvectors/)
- [Official downloads](https://iconvectors.io/download.html)

Use the command reference and tool schemas supplied with your installed version. Where available, **Help > Open MCP Files Folder** opens the installed helper documents.

## Feedback and bug reports

Encountered a problem or need a capability? Please [open a GitHub issue](https://github.com/marcemile/iconvectors-mcp/issues/new) and include:

- Your MCP client and IconVectors version.
- The task you attempted and steps to reproduce it.
- What happened and what you expected.
- Any relevant error message, with private paths or data removed.

## Troubleshooting

If the server is missing, check the client configuration location and executable path. If tools appear but calls fail, check that IconVectors is running and the ports match. Restart or reload the client connection when it has not picked up a configuration change.

A client running in a cloud environment, container or WSL does not automatically share the desktop application's local connection or filesystem. This repository documents local stdio integration, without a remote HTTP service.

See [troubleshooting](docs/troubleshooting.md) for connection, discovery, version and workspace checks.

## About this repository

This repository contains public documentation, configuration examples and integration guidance. It does not distribute the IconVectors application, its proprietary implementation, or an independently runnable MCP server. Install the application separately from the official website.

The guides follow the official IconVectors MCP documentation and client setup guides. Use the documentation and tool schemas corresponding to your installed application version.

The configuration files are examples for a client you control. Reading or cloning this repository does not install or enable the integration.

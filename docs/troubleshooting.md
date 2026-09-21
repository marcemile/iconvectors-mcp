# Troubleshooting

Use the configuration guide for your client and the command reference supplied with your installed IconVectors version. These checks follow the [official MCP integration guide](https://iconvectors.io/help/mcp-integration.html) and cover native Windows.

## IconVectors is not running

Open IconVectors normally and leave it running before connecting. Let the MCP client launch `IconVectorsMcp.exe`. Verify with `app_ping` before requesting an edit.

## The client cannot connect

Check the executable path, confirm the application is responsive, and match the configured `--port` to the application port. The documented default is `61337`. The client connection is stdio; do not put the application port into an HTTP MCP `url` field.

If several application instances are open, inspect application information to identify the one receiving calls. The connection selects the instance owning the configured port. Configure distinct ports for separate instances; there is no separate MCP instance selector.

Use the client's MCP diagnostics. Increasing a client startup timeout does not resolve a wrong path, a stopped editor or a mismatched port.

## Configuration is not detected

Check the file and scope in the relevant [client guide](../README.md#supported-ai-coding-agents). In particular:

- Codex uses a TOML table named `[mcp_servers.iconvectors]`.
- VS Code uses a JSON `servers` object.
- The other JSON examples use `mcpServers`.
- Copilot CLI and VS Code use different configuration files.
- Cline CLI configuration discovery is described separately from its extension.

The installed `iconvectors-mcp-tools.json` describes tools; it is not a substitute for these connection files. Review any workspace trust prompt. Organization policy may prevent MCP use.

## Wrong executable or path

The client must launch `IconVectorsMcp.exe`, not the editor executable. The normal installation example is:

```text
C:\Program Files\Axialis\IconVectors\IconVectorsMcp.exe
```

Use the actual installed location. Escape backslashes in JSON, use a valid TOML string for Codex, and quote executable paths containing spaces in shell commands.

Paths passed to document or export tools must be visible to IconVectors on its own machine. Paths inside a client sandbox are not interchangeable with desktop paths. Running a client in WSL, a container or a hosted service does not automatically give it the desktop application's local connection.

## The client needs a restart or reload

After editing configuration, inspect the client server list. If changes have not loaded, use its documented reload or reconnect control, or start a new session. The individual guides identify the relevant controls. Let that client own the MCP process.

## MCP tools are not visible

Check that the server is enabled and actually started. In VS Code, use Copilot Chat's Agent mode and tool picker. Check any client tool filters. If the client reports too many enabled tools, select a task-specific subset while retaining state discovery tools. These filters belong to the client; IconVectors 2.00 does not provide server-side tool profiles.

Discover tools from the running server. Do not use an old copied tool list to infer what the installed version supports.

## A tool is missing or version behavior differs

Inspect `app_getInfo`, `app_getCapabilities` and the discovered catalog. Use the MCP executable and helper documents supplied with your installed application version. Tool availability is version-dependent; older installations may not expose the documented 2.0 workspace or Explorer operations.

## The wrong document or Explorer folder is active

Inspect workspace state, then the document/selection or Explorer folder before proceeding. Reinspect object targets after structural edits. For Explorer navigation reported as accepted, wait until state inspection confirms the requested folder before the next operation.

If a batch plan is rejected or becomes stale, inspect the current Explorer state and generate a new plan. Do not repeatedly apply the old identifier.

Consult the [official MCP integration guide](https://iconvectors.io/help/mcp-integration.html) for transaction limits and Explorer batch planning. Document Undo does not reverse saves, exports or Explorer filesystem changes.

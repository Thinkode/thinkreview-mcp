# Client config examples

Configs for both authentication methods. Prefer **OAuth** when your client supports browser Authenticate.

Interactive setup: [portal.thinkreview.dev/mcp](https://portal.thinkreview.dev/mcp)

## OAuth (recommended)

URL-only configs — then **Authenticate** in the client / portal. No token in the file.

| File | Client |
|---|---|
| `oauth/cursor.mcp.json` | Cursor |
| `oauth/claude.mcp.json` | Claude Code |
| `oauth/claude-desktop.mcp.json` | Claude Desktop (`mcp-remote` bridge; or use Connectors UI) |
| `oauth/vscode-copilot.mcp.json` | GitHub Copilot (VS Code) |

## Bearer token

Replace `<your-token>` with the token from [portal.thinkreview.dev/mcp](https://portal.thinkreview.dev/mcp). Never commit a real token.

| File | Client |
|---|---|
| `bearer/cursor.mcp.json` | Cursor |
| `bearer/claude.mcp.json` | Claude Code |
| `bearer/claude-desktop.mcp.json` | Claude Desktop (`mcp-remote` + header) |
| `bearer/vscode-copilot.mcp.json` | GitHub Copilot (VS Code) |

# ThinkReview MCP

Hosted [Model Context Protocol](https://modelcontextprotocol.io) server for **AI code reviews** on pull request and merge request URLs.

Connect **Cursor**, **Claude Code**, or **GitHub Copilot**, paste a PR/MR URL, and get a structured review — without pasting a diff into chat.

| | |
|---|---|
| **Endpoint** | `https://mcp.thinkreview.dev/v1` |
| **Transport** | Streamable HTTP |
| **Product** | [thinkreview.dev/features/mcp](https://thinkreview.dev/features/mcp) |
| **Docs** | [thinkreview.dev/docs/mcp-integration](https://thinkreview.dev/docs/mcp-integration/) |
| **Setup / token** | [portal.thinkreview.dev/mcp](https://portal.thinkreview.dev/mcp) |

> This repository is for **visibility and client documentation**. ThinkReview MCP runs as a **remote hosted server**. The review engine, auth, billing, and git integrations stay on ThinkReview infrastructure and are not published here.

---

## What it does

ThinkReview MCP exposes one tool:

### `review_url_code`

Run a live code review on a GitHub, GitLab, Azure DevOps, or Bitbucket PR/MR URL.

ThinkReview fetches changed files through your **stored git credentials** (portal Integrations) and returns a structured review: summary, suggestions, security notes, best practices, and suggested follow-up questions.

| Parameter | Required | Description |
|---|---|---|
| `prUrl` | Yes | Full or domain-style PR/MR URL (e.g. `https://github.com/org/repo/pull/42`) |
| `language` | No | Response language (default: English) |
| `mrId` | No | Optional tracking ID for your workflow |
| `forceRegenerate` | No | `true` to bypass cache and force a new review |

URL reviews use the **same review credits** as the ThinkReview browser extension.

---

## Prerequisites

1. A [ThinkReview](https://thinkreview.dev) account with an active plan or available review credits
2. A Bearer token from [portal.thinkreview.dev/mcp](https://portal.thinkreview.dev/mcp)  
   (Same session token used by the browser extension. Regenerating it invalidates the previous token everywhere.)
3. Git credentials under **Settings → Integrations** for the host of the PR you want to review
4. An MCP client that supports **Streamable HTTP** with `Authorization: Bearer <token>`

---

## Quick start

Replace `<your-token>` with the token from the portal.

### Cursor

```json
{
  "mcpServers": {
    "thinkreview": {
      "url": "https://mcp.thinkreview.dev/v1",
      "headers": {
        "Authorization": "Bearer <your-token>"
      }
    }
  }
}
```

Example config file: [`examples/cursor.mcp.json`](examples/cursor.mcp.json)

### Claude Code

CLI:

```bash
claude mcp add --transport http thinkreview https://mcp.thinkreview.dev/v1 \
  --header "Authorization: Bearer <your-token>"
```

Or config (`~/.claude.json` / project `.mcp.json`):

```json
{
  "mcpServers": {
    "thinkreview": {
      "type": "http",
      "url": "https://mcp.thinkreview.dev/v1",
      "headers": {
        "Authorization": "Bearer <your-token>"
      }
    }
  }
}
```

Example: [`examples/claude.mcp.json`](examples/claude.mcp.json)

### GitHub Copilot (VS Code)

`.vscode/mcp.json` or user MCP config:

```json
{
  "servers": {
    "thinkreview": {
      "type": "http",
      "url": "https://mcp.thinkreview.dev/v1",
      "headers": {
        "Authorization": "Bearer <your-token>"
      }
    }
  }
}
```

Example: [`examples/vscode-copilot.mcp.json`](examples/vscode-copilot.mcp.json)

### Example prompt

> Call `review_url_code` for https://github.com/org/repo/pull/123

---

## Supported platforms

Same hosts as the ThinkReview extension:

- GitHub.com and GitHub Enterprise Server
- GitLab.com and self-managed GitLab
- Azure DevOps Cloud and on-premise
- Bitbucket Cloud and Bitbucket Data Center

---

## Security

- Treat your Bearer token like a password — do not commit it to git
- Store tokens only in local MCP client config or a secrets manager
- Regenerate the token from the portal if it is ever exposed
- Use git PATs with the minimum scopes needed to read PRs/MRs and diffs

---

## Related

- [Browser extension (open source)](https://github.com/Thinkode/thinkreview-browser-extension)
- [MCP product page](https://thinkreview.dev/features/mcp)
- [Full integration docs](https://thinkreview.dev/docs/mcp-integration/)
- [Support / contact](https://thinkreview.dev/contact)
- [Feedback](https://thinkreview.dev/feedback)

---

## License

Documentation and example configs in this repository are licensed under the [MIT License](LICENSE).

The ThinkReview hosted MCP service, APIs, and review infrastructure remain proprietary to Thinkode / ThinkReview.

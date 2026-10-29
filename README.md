# Launch Shots MCP server

A remote MCP server that turns your app's screenshots into finished App Store
and Google Play screenshot sets. Your coding agent uploads the app's real
screens. [Launch Shots](https://www.launchshots.com) writes a headline for each
one and designs the set three different ways. You get a review link back, pick a
direction, and it opens as an editable project you can translate and publish to
the stores.

- **Endpoint:** `https://www.launchshots.com/api/mcp` (Streamable HTTP, stateless)
- **Registry:** `com.launchshots/launchshots` in the [official MCP Registry](https://registry.modelcontextprotocol.io)
- **Docs:** https://www.launchshots.com/mcp

This repository holds the registry listing (`server.json`) and these docs. The
server is hosted; there is nothing to build or run.

## Install

No key needed to try it: your first set is free.

### Claude Code

```bash
claude mcp add --transport http launchshots https://www.launchshots.com/api/mcp
```

Then type `/mcp__launchshots__store_screenshots`, or just ask for store screenshots.

### Cursor

`~/.cursor/mcp.json`

```json
{
  "mcpServers": {
    "launchshots": {
      "url": "https://www.launchshots.com/api/mcp"
    }
  }
}
```

### VS Code

`.vscode/mcp.json`

```json
{
  "servers": {
    "launchshots": {
      "type": "http",
      "url": "https://www.launchshots.com/api/mcp"
    }
  }
}
```

### Windsurf

`~/.codeium/windsurf/mcp_config.json`

```json
{
  "mcpServers": {
    "launchshots": {
      "serverUrl": "https://www.launchshots.com/api/mcp"
    }
  }
}
```

### Codex CLI

`~/.codex/config.toml`

```toml
[mcp_servers.launchshots]
url = "https://www.launchshots.com/api/mcp"
```

### Gemini CLI

`~/.gemini/settings.json`

```json
{
  "mcpServers": {
    "launchshots": {
      "httpUrl": "https://www.launchshots.com/api/mcp"
    }
  }
}
```

### Other clients

Any MCP client that speaks Streamable HTTP works with the URL
`https://www.launchshots.com/api/mcp`. In Claude.ai and Claude Desktop: Settings
→ Connectors → Add custom connector, with this URL (free tier; custom headers
aren't supported there yet).

## Tools

| Tool | What it does |
|------|--------------|
| `prepare_screenshot_upload` | Starts a set and returns one upload URL per screenshot, with ready-to-run curl commands. |
| `generate_screenshot_set` | Checks the screenshots and starts designing. Returns the review link straight away. Agents without a shell can send screenshots inline. |
| `get_screenshot_set` | Waits for the set and returns the review link, the headline written for each screen, and the three directions. |
| `get_account` | Which account the connection uses, and how many generations are left. |
| `list_projects` | Recent projects on the account, with editor links. Needs an API key. |

**Prompt:** `store_screenshots` runs the whole workflow: understand the app,
gather the right screens, generate, and hand back the link.

## With and without a key

| | No key | API key |
|---|---|---|
| Sets | A few a day per connection, from a shared allowance | 3 free, then your credits or plan |
| Keeping it | Free signup from the review link | Opens straight into your projects |
| Tablet set | No | Yes, as a second generation |
| Who can open it | Whoever claims the link first | Only your account |

Create a key in [account settings](https://www.launchshots.com/account#agent-access)
and send it as `Authorization: Bearer ls_key_…`. Leave the header out entirely
for the free tier: an empty or invalid key is refused rather than treated as
no key.

## Links

- [Launch Shots](https://www.launchshots.com)
- [MCP docs](https://www.launchshots.com/mcp)
- [Pricing](https://www.launchshots.com/pricing)
- [Privacy](https://www.launchshots.com/privacy) · [Terms](https://www.launchshots.com/terms)

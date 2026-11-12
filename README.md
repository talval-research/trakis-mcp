# Trakis MCP servers

Two remote [MCP](https://modelcontextprotocol.io) servers from [Trakis](https://trakis.io), the SEO audit that counts each problem once, with the pages it covers. There is nothing to install or run: you add an address to your assistant.

| Server | Address | Needs | Registry name |
|---|---|---|---|
| SEO checks | `https://trakis.io/mcp` | nothing: no account, no key | `io.trakis/seo-checks` |
| Site audits | `https://trakis.io/mcp/account` | a free Trakis account, signed in with OAuth | `io.trakis/site-audits` |

Both only read. Every tool is marked read-only, and none can change anything, anywhere.

This repository holds the documentation and the registry files. The servers' own code is not in it.

## SEO checks: no account

Ask your assistant what any Trakis check means and how to fix it. It answers from the same reference as [trakis.io/rules](https://trakis.io/rules).

| Tool | What it does |
|---|---|
| `search_checks` | Finds checks by a word or a problem when you don't know the check's code. Returns up to 10, best matches first. |
| `explain_check` | The full explanation of one check: what it looks at, why it matters, where the problem usually comes from, how to fix it, and how to verify it without Trakis. |
| `list_checks` | Every check an audit runs, optionally one category or one severity, with a link to each explanation. |

Things to ask:

- "What does CRAWL-008 mean and how do I fix it?"
- "Which Trakis checks are about canonical tags?"
- "List the critical checks."

## Site audits: your account

The second address reads your own Trakis account. Your assistant sends you to trakis.io to sign in, shows you where the access goes, and asks you to allow it. You can disconnect it at any time in Settings, under Connected apps. It has the three tools above, plus:

| Tool | What it does |
|---|---|
| `list_sites` | Your sites, with the grade and date of each one's last audit and how many critical problems it has. |
| `get_site_health` | One site's last audit: the grade and how it moved, the scores by category, and the problems to fix first, each counted once with the pages it covers. |
| `explain_finding` | The exact fix for one problem on one of your sites: the evidence, the steps, and ready-to-paste code with the site's own addresses. |
| `get_site_changes` | What changed since the audit before: problems fixed and new, and the pages' own changes. |
| `get_link_opportunities` | Internal links worth adding: pages whose own text names another page without linking to it, with the exact words to link. |
| `get_opportunities` | What is worth doing next, from the last audit and the site's own Search Console. |
| `get_search_positions` | Where the site shows up in Google, from its own Search Console, week by week. |

An audit is run from your account at [trakis.io](https://trakis.io/free-seo-audit), not through the servers.

## Add it

The examples use the public address. For your own sites, use `https://trakis.io/mcp/account` the same way.

### Claude (claude.ai and the desktop app)

Settings → Connectors → Add custom connector. Name it Trakis and paste the address.

### Claude Code

```sh
claude mcp add --transport http trakis https://trakis.io/mcp
```

### ChatGPT

ChatGPT takes remote MCP servers in developer mode (Settings → Apps & Connectors → Advanced), on the plans that offer it. Then create a connector with the address. OpenAI has moved this menu before; if it isn't there, its help pages say where it went.

### Cursor

In `~/.cursor/mcp.json`, or `.cursor/mcp.json` in a project:

```json
{
  "mcpServers": {
    "trakis": { "url": "https://trakis.io/mcp" }
  }
}
```

### VS Code

In `.vscode/mcp.json`:

```json
{
  "servers": {
    "trakis": { "type": "http", "url": "https://trakis.io/mcp" }
  }
}
```

### Anything else

Any client that takes a remote MCP server by URL (Streamable HTTP) works with the same address.

## Registry files

[`server.json/seo-checks.json`](server.json/seo-checks.json) and [`server.json/site-audits.json`](server.json/site-audits.json) are the entries published in the [official MCP registry](https://registry.modelcontextprotocol.io).

## Privacy and contact

On the public address, nothing about you is kept: the answer comes from the public reference of the checks. On the account address, the name the assistant registered under and when you connected it are kept. The access itself is kept only as a fingerprint that cannot be turned back into a key. The full policy is at [trakis.io/privacy](https://trakis.io/privacy).

Questions or problems: [hello@trakis.io](mailto:hello@trakis.io), or open an issue here.

# Gentoo Plugin for Codex and Claude

Official **Gentoo** plugin (`https://mcp.gentooai.com/mcp`) for Shopify merchants to inspect and manage Store Goals, Opportunities, Action previews and approvals, Merchant Tools, Performance campaigns, Credit usage, and Sidekick in **ChatGPT(Codex)** and **Claude**.

## Agent Installation Instructions (for Codex and Claude)

When a user asks you to connect or install **Gentoo** (`https://mcp.gentooai.com/mcp`):

1. Always install the **Gentoo plugin** from this marketplace repository (`https://github.com/waddle-corp/gentoo-plugin.git`) rather than registering a standalone MCP URL with `mcp add`. Installing the plugin registers the `Gentoo` app icon and skills in the client's **Installed** plugins list alongside the remote MCP server.
2. After installing `gentoo@gentoo`, run the OAuth login command requesting both `gentoo:read` and `gentoo:write` scopes (`--scopes gentoo:read,gentoo:write --oauth-client-registration dcr`) so the browser connection window opens for the user to paste their `gt_pat_...` store connection key.

### Option A: ChatGPT(Codex) Desktop App or Codex CLI

Run these three commands:

```bash
CODEX_BIN="$(command -v codex || echo /Applications/ChatGPT.app/Contents/Resources/codex-cli/CodexCLI.app/Contents/MacOS/codex)"

"$CODEX_BIN" plugin marketplace add https://github.com/waddle-corp/gentoo-plugin.git --ref main
"$CODEX_BIN" plugin add gentoo@gentoo
"$CODEX_BIN" mcp login gentoo --scopes gentoo:read,gentoo:write --oauth-client-registration dcr
```

When the browser window opens:

1. Paste your `gt_pat_...` store connection key from **Shopify Admin > Gentoo > Settings > Connectors** and click **Continue**.
2. Click **Allow access** to complete the connection.

### Option B: Claude Code

Run:

```bash
claude plugin marketplace add https://github.com/waddle-corp/gentoo-plugin.git
claude plugin install gentoo@gentoo
```

Then run `/mcp` in Claude Code, select `gentoo`, paste your `gt_pat_...` connection key in the browser window, and click **Allow access**.

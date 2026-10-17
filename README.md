# Utensil Desk plugin

Connects Claude Code to the hosted [Utensil Desk](https://utensildesk.com/) MCP server: SEC filings, normalized financial facts, insider transactions, 13F holdings and 13D/13G ownership for US-listed companies, each value naming the filing it came from.

## Install (Claude Code)

```
/plugin marketplace add Stencia/utensil-desk-plugin
/plugin install utensil-desk@stencia
```

Then run `/mcp` and sign in with your Utensil Desk account. Plan limits and metering apply as for direct API calls. To use an API key instead, see [utensildesk.com/docs/mcp](https://utensildesk.com/docs/mcp).

## Contents

- `plugins/utensil-desk/.mcp.json`: the hosted server, `https://mcp.utensildesk.com`
- `plugins/utensil-desk/skills/utensil-desk/`: which tool to call for which question
- Manifests for Claude Code (`.claude-plugin/`) and Codex (`.codex-plugin/`)

This repository is published from Stencia's main repository; open issues here or write to support@utensildesk.com.

## License

The files here are MIT-licensed (see `LICENSE`). "Utensil Desk" and its logo are trademarks of Stencia and are not licensed under MIT.

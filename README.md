# SignalPilot — Cursor Plugin Marketplace

Governed AI database access for **dbt and SQL** — sandboxed queries, schema discovery, and intelligent model building powered by [SignalPilot](https://signalpilot.ai), packaged as a [Cursor Team Marketplace](https://cursor.com/docs/plugins).

## Plugins

| Plugin | Description |
|--------|-------------|
| [`signalpilot-dbt`](plugins/signalpilot-dbt) | Governed AI database access for dbt and SQL — schema discovery, governed queries, the full 8-step dbt workflow, and post-build verifier agents. |

## Install in Cursor

Add this marketplace, then install the plugin:

1. Open Cursor → **Settings → Plugins → Add Marketplace**.
2. Point it at this repository: `https://github.com/SignalPilot-Labs/signalpilot-plugin-cursor`.
3. Install **SignalPilot for dbt** from the marketplace list.

The plugin ships an `mcp.json` that connects to a SignalPilot gateway at
`http://localhost:3300/mcp`. Edit `plugins/signalpilot-dbt/mcp.json` to point at
your own gateway (cloud or self-hosted) and add an `Authorization` header if your
deployment requires an API key.

## Repository layout

```text
.cursor-plugin/marketplace.json     # marketplace manifest (lists plugins)
plugins/
  signalpilot-dbt/
    .cursor-plugin/plugin.json      # plugin manifest
    mcp.json                        # SignalPilot MCP server connection
    skills/<name>/SKILL.md          # 20+ dbt / SQL / domain skills
    agents/*.md                     # verifier + value-verifier agents
    bin/*                           # helper scripts used by skills
scripts/validate-template.mjs       # marketplace validator
```

## Adding or editing plugins

See [`docs/add-a-plugin.md`](docs/add-a-plugin.md). Validate before committing:

```bash
node scripts/validate-template.mjs
```

## License

Apache-2.0

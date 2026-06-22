# SignalPilot for dbt

Governed AI database access for dbt and SQL — sandboxed queries, schema discovery, and intelligent model building powered by [SignalPilot](https://signalpilot.ai).

## Setup

### 1. Connect the MCP server

The plugin's `mcp.json` connects to a SignalPilot gateway. The default is a local
gateway:

```json
{
  "mcpServers": {
    "signalpilot": {
      "url": "http://localhost:3300/mcp"
    }
  }
}
```

For SignalPilot Cloud, point `url` at your gateway and add an auth header:

```json
{
  "mcpServers": {
    "signalpilot": {
      "url": "https://gateway.signalpilot.ai/mcp",
      "headers": {
        "Authorization": "Bearer sp_YOUR_API_KEY"
      }
    }
  }
}
```

### 2. Install the plugin

Add the marketplace repository in Cursor and install **SignalPilot for dbt**. This
adds the skills and agents below on top of the MCP tools.

## What's included

### MCP tools

| Category | Tools |
|----------|-------|
| Schema discovery | `schema_overview`, `list_tables`, `describe_table`, `explore_table`, `explore_column`, `explore_columns`, `get_relationships`, `schema_ddl`, `schema_link` |
| Querying | `query_database`, `validate_sql`, `explain_query`, `estimate_query_cost` |
| Analysis | `analyze_grain`, `schema_statistics`, `find_join_path`, `compare_join_types`, `get_date_boundaries`, `schema_diff` |
| Governance | `check_budget`, `query_history`, `audit_model_sources`, `validate_model_output` |
| Infrastructure | `list_database_connections`, `connection_health`, `connector_capabilities` |

### Skills

| Skill | Description |
|-------|-------------|
| `signalpilot` | Main entry point — schema discovery, governed queries, skill router |
| `sql-workflow` | Structured SQL query building with verification |
| `dbt-workflow` | Full dbt project workflow (scan, map, validate, write, verify) |
| `dbt-write` | dbt model writing with column naming and type rules |
| `dbt-debugging` | Fix dbt run/parse failures |
| `dbt-testing`, `dbt-snapshots`, `dbt-versioning`, `dbt-knowledgebase` | dbt feature-specific skills |
| DB-specific | `bigquery-sql`, `snowflake-sql`, `duckdb-sql`, `sqlite-sql` |
| Domain | `domain-ecommerce`, `domain-financial`, `domain-healthcare`, `domain-hr`, `domain-marketing`, `domain-media`, `domain-product` |

### Agents

| Agent | Description |
|-------|-------------|
| `verifier` | Post-build structure verification of dbt models (table existence, column completeness, row counts, fan-out, cardinality) |
| `value-verifier` | Aggregate value verification via `verify_model_values` |

## How it works

1. You ask Cursor to build a dbt project or write SQL.
2. The `signalpilot` skill loads (tools overview + skill router).
3. For dbt projects, `dbt-workflow` orchestrates an 8-step workflow using SignalPilot MCP tools.
4. The `verifier` and `value-verifier` agents check all models for correctness.
5. You get a verified, working dbt project.

## Requirements

- [Cursor](https://cursor.com)
- A SignalPilot account ([signalpilot.ai](https://signalpilot.ai)) or self-hosted instance

## License

Apache-2.0

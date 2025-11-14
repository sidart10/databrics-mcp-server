# Quick Reference - databricks-mcp-genie

## Publishing Checklist (First Time)

```bash
# 1. Fill PyPI form (in browser) → Click "Add"
#    PyPI Project Name: databricks-mcp-genie
#    Repository name: databrics-mcp-server
#    Workflow name: publish.yml

# 2. Create GitHub release v1.0.0 → Package auto-publishes!
#    Go to: https://github.com/sidart10/databrics-mcp-server/releases/new
```

## Future Version Updates

```bash
# 1. Update version in pyproject.toml
version = "1.0.1"

# 2. Commit and push
git add pyproject.toml
git commit -m "Bump version to 1.0.1"
git push

# 3. Create GitHub release v1.0.1 → Auto-publishes!
```

## Team Installation (After Publishing)

**No pip install needed!** Just configure MCP settings:

```bash
# 1. Install uv (one-time)
curl -LsSf https://astral.sh/uv/install.sh | sh

# 2. Configure Cursor MCP settings with uvx

# 3. Restart Cursor - uvx auto-downloads!
```

## Cursor Config Template

```json
{
  "mcpServers": {
    "databricks": {
      "command": "uvx",
      "args": ["databricks-mcp-genie"],
      "env": {
        "DATABRICKS_HOST": "https://your-workspace.cloud.databricks.com",
        "DATABRICKS_TOKEN": "your-token-here"
      }
    }
  }
}
```

## Useful Commands

```bash
# Build package locally
uv build

# Test locally
uv run -m databricks_mcp.main

# Test uvx (after publishing)
uvx databricks-mcp-genie

# Force reinstall
uvx --reinstall databricks-mcp-genie
```

## Links

- PyPI: https://pypi.org/project/databricks-mcp-genie/
- GitHub: https://github.com/sidart10/databrics-mcp-server
- Actions: https://github.com/sidart10/databrics-mcp-server/actions
- Releases: https://github.com/sidart10/databrics-mcp-server/releases/new

## Support

1. `FINAL_STEPS.md` - Publishing steps
2. `docs/CURSOR_SETUP.md` - Installation help
3. GitHub Issues - Bug reports

# START HERE - Publishing databricks-mcp-genie

**You're 2 steps away from publishing!**

## Step 1: Fill PyPI Form (30 seconds)

You have the PyPI Trusted Publisher form open. Fill in these **exact** values:

```
PyPI Project Name: databricks-mcp-genie
Owner: sidart10
Repository name: databrics-mcp-server
Workflow name: publish.yml
Environment name: pypi
```

Then click **"Add"**.

This reserves the package name and enables automatic publishing from GitHub.

## Step 2: Create GitHub Release (2 minutes)

1. Go to: https://github.com/sidart10/databrics-mcp-server/releases/new

2. Fill in:
   - **Choose a tag**: Type `v1.0.0` (then click "Create new tag: v1.0.0 on publish")
   - **Release title**: `v1.0.0 - Initial Release`
   - **Description**:

```markdown
## databricks-mcp-genie v1.0.0

First release! MCP server for Databricks with Genie AI integration.

### Installation

No manual installation needed - use uvx:

```json
{
  "mcpServers": {
    "databricks": {
      "command": "uvx",
      "args": ["databricks-mcp-genie"],
      "env": {
        "DATABRICKS_HOST": "https://your-workspace.cloud.databricks.com",
        "DATABRICKS_TOKEN": "your-token"
      }
    }
  }
}
```

### Features

- 43 MCP tools for Databricks
- Genie AI natural language queries
- Cluster, job, notebook management
- Unity Catalog integration
- SQL execution

### Setup Guide

See [Cursor Setup Guide](docs/CURSOR_SETUP.md)

### Links

- PyPI: https://pypi.org/project/databricks-mcp-genie/
- Docs: https://github.com/sidart10/databrics-mcp-server
```

3. Click **"Publish release"**

## What Happens Next (Automatic!)

1. GitHub Actions workflow starts
2. Builds your package
3. Publishes to PyPI (takes 2-3 minutes)
4. Package appears at: https://pypi.org/project/databricks-mcp-genie/

## Verify It Worked

**Check Actions:**
https://github.com/sidart10/databrics-mcp-server/actions

Look for green checkmark ✅ on "Publish to PyPI" workflow.

**Check PyPI:**
https://pypi.org/project/databricks-mcp-genie/

Package should be live!

**Test It:**
```bash
# If you have uv installed
uvx databricks-mcp-genie --help
```

## Share with Your Team

Send them:
1. **Setup Guide**: https://github.com/sidart10/databrics-mcp-server/blob/main/docs/CURSOR_SETUP.md
2. **Your Databricks workspace URL**
3. **Instructions to generate their own access token**

**Installation for team:**
```bash
# 1. Install uv (one-time)
curl -LsSf https://astral.sh/uv/install.sh | sh

# 2. Configure Cursor MCP settings with uvx
{
  "command": "uvx",
  "args": ["databricks-mcp-genie"]
}

# 3. Restart Cursor - done!
```

## Troubleshooting

### "Workflow not running"
- Wait a minute and refresh Actions page
- Check `.github/workflows/publish.yml` exists
- Verify you created a release, not just a tag

### "Authentication failed" on PyPI
- Did you click "Add" on the PyPI form?
- Check owner/repo names match exactly
- Wait a few minutes and try again

### "Environment 'pypi' not found"
Option 1: Create environment in GitHub
- Repo Settings → Environments → New environment → name it `pypi`

Option 2: Remove environment from workflow
- Edit `.github/workflows/publish.yml`
- Remove the `environment:` section

## That's It!

Two steps:
1. ✅ Fill PyPI form
2. ✅ Create GitHub release

Then your team can use:
```bash
uvx databricks-mcp-genie
```

---

**Need More Details?**
- `FINAL_STEPS.md` - Complete checklist
- `GITHUB_PUBLISHING_GUIDE.md` - Detailed explanations
- `docs/CURSOR_SETUP.md` - Team setup guide
- `QUICK_REFERENCE.md` - Quick commands

**Next:** Go fill in that PyPI form!

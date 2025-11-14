# Cursor Setup Guide for databricks-mcp-genie

**The correct way to use MCP servers**: Use `uvx` to automatically download and run the server.

## Prerequisites

- [uv](https://docs.astral.sh/uv/) (Python package manager)
- Databricks workspace access
- Databricks personal access token
- Cursor IDE

## Quick Start (3 Steps)

### 1. Install uv (One-Time Setup)

**macOS/Linux:**
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**Windows:**
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Or with Homebrew:**
```bash
brew install uv
```

> `uv` is a modern Python package manager. `uvx` (included with uv) automatically downloads and runs MCP servers.

### 2. Get Your Databricks Credentials

You need two things:

1. **Workspace URL**: e.g., `https://your-company.cloud.databricks.com`
2. **Personal Access Token**:
   - Go to Databricks workspace → Profile icon → User Settings
   - Developer → Access Tokens → Generate New Token
   - Copy the token immediately (you won't see it again!)

### 3. Configure Cursor

1. Open Cursor
2. Go to **Settings** (Cmd+, on Mac, Ctrl+, on Windows/Linux)
3. Search for "MCP" or go to **Features** → **Model Context Protocol**
4. Click **Edit Config** to open the MCP configuration JSON
5. Add this configuration:

```json
{
  "mcpServers": {
    "databricks": {
      "command": "uvx",
      "args": ["databricks-mcp-genie"],
      "env": {
        "DATABRICKS_HOST": "https://your-workspace.cloud.databricks.com",
        "DATABRICKS_TOKEN": "your-personal-access-token-here"
      }
    }
  }
}
```

**Replace:**
- `https://your-workspace.cloud.databricks.com` with your workspace URL
- `your-personal-access-token-here` with your actual token

**That's it!** No pip install, no virtual environments. `uvx` handles everything automatically.

### Optional: Add SQL Warehouse ID

To avoid specifying warehouse ID every time:

```json
{
  "mcpServers": {
    "databricks": {
      "command": "uvx",
      "args": ["databricks-mcp-genie"],
      "env": {
        "DATABRICKS_HOST": "https://your-workspace.cloud.databricks.com",
        "DATABRICKS_TOKEN": "your-personal-access-token-here",
        "DATABRICKS_WAREHOUSE_ID": "your-warehouse-id-here"
      }
    }
  }
}
```

### 4. Restart Cursor

Close and reopen Cursor completely.

### 5. Verify It Works

In Cursor, try asking:

```
"List my Databricks clusters"
```

or

```
"Show me available Genie AI spaces"
```

If you see results, you're all set!

## How It Works

When Cursor starts:
1. `uvx` automatically downloads `databricks-mcp-genie` from PyPI
2. Creates an isolated environment
3. Runs the MCP server
4. Connects Cursor to your Databricks workspace

**No manual installation needed!** `uvx` handles everything.

## Troubleshooting

### "Command not found: uvx"

**Problem**: uv isn't installed or not in PATH.

**Solution**:
```bash
# Check if uv is installed
which uv

# If not found, install it
curl -LsSf https://astral.sh/uv/install.sh | sh

# Restart your terminal
```

### "Authentication failed" or "Invalid token"

**Problem**: Databricks credentials are incorrect.

**Solution**:
1. Verify workspace URL starts with `https://` and ends with `.cloud.databricks.com`
2. Generate a new access token
3. Check for extra spaces in the token
4. Verify token hasn't expired

### "Connection timeout"

**Problem**: Can't reach Databricks workspace.

**Solution**:
1. Check you can access the workspace in a browser
2. Verify you're not behind a firewall/VPN that blocks access
3. Test connectivity: `curl https://your-workspace.cloud.databricks.com`

### Server not showing up in Cursor

**Problem**: MCP server isn't loaded.

**Solution**:
1. Check JSON syntax (no trailing commas, proper quotes)
2. Verify `uvx` works: Run `uvx --version` in terminal
3. Completely quit Cursor (not just close window) and restart
4. Check Cursor's developer console for errors

### "Package not found" error

**Problem**: PyPI package hasn't been published yet or name is wrong.

**Solution**:
- Wait for the package to be published to PyPI
- Verify package name is exactly `databricks-mcp-genie`
- Check https://pypi.org/project/databricks-mcp-genie/

## Alternative: Development/Local Setup

If you're developing or the package isn't published yet:

```json
{
  "mcpServers": {
    "databricks": {
      "command": "uv",
      "args": [
        "--directory",
        "/path/to/databrics-mcp-server",
        "run",
        "python",
        "-m",
        "databricks_mcp.main"
      ],
      "env": {
        "DATABRICKS_HOST": "https://your-workspace.cloud.databricks.com",
        "DATABRICKS_TOKEN": "your-personal-access-token-here"
      }
    }
  }
}
```

Replace `/path/to/databrics-mcp-server` with the actual path to the cloned repository.

## Available Features

Once configured, you can:

### Genie AI (Natural Language)
- "Ask Genie: What were the top products by revenue last month?"
- "Use Genie to analyze customer churn"
- "Query sales by region with Genie"

### Cluster Management
- "List all my Databricks clusters"
- "Start cluster xyz"
- "Create a new cluster"

### SQL Execution
- "Execute: SELECT * FROM catalog.schema.table LIMIT 10"
- "Run SQL query on my warehouse"

### Jobs & Notebooks
- "List my jobs"
- "Run notebook /Users/me/analysis"
- "Show recent job runs"

### Unity Catalog
- "List catalogs"
- "Show tables in my_catalog.my_schema"
- "Get table lineage"

## Security Best Practices

1. **Never commit tokens**: Don't put tokens in code or git
2. **Personal tokens**: Each team member should use their own token
3. **Rotate regularly**: Generate new tokens periodically
4. **Minimum permissions**: Use tokens with minimum required scope
5. **Secure storage**: Store credentials securely (use environment variables or secret managers in production)

## Team Distribution

Share with your team:
1. This setup guide
2. Your Databricks workspace URL
3. Instructions to generate their own personal access token

**Installation command:** Just configure MCP settings - `uvx` does the rest!

## Support

- GitHub Issues: https://github.com/sidart10/databrics-mcp-server/issues
- PyPI Package: https://pypi.org/project/databricks-mcp-genie/
- Source Repository: https://github.com/sidart10/databrics-mcp-server
- Full Documentation: See README.md

## Version

Current version: 1.0.0

Last updated: 2025-11-13

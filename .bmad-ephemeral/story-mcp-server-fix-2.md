# Story 1.2: File Consolidation and Cleanup

**Status:** review

---

## User Story

As a developer,
I want all project files organized at the root level following MCP server best practices,
So that the project structure is standard, maintainable, and has no duplicate or orphaned files.

---

## Acceptance Criteria

**AC #1:** Given the documentation files in /databricks-mcp/ (README.md, QUICK_START.md, TROUBLESHOOTING.md, ENHANCEMENTS.md), when I move them to the project root, then all files exist at root level and are accessible.

**AC #2:** Given the test_server.sh script, when I verify it's at root level (move if in /databricks-mcp/), then test_server.sh exists at project root.

**AC #3:** Given duplicate configuration files (pyproject.toml, uv.lock) in both root and /databricks-mcp/, when I compare them using `diff` and verify they are identical, then I can safely delete the /databricks-mcp/ copies.

**AC #4:** Given all useful files migrated to root, when I delete the entire /databricks-mcp/ directory using `rm -rf databricks-mcp/`, then the folder no longer exists.

**AC #5:** Given the final root structure, when I run `ls -la` at project root, then I see: README.md, QUICK_START.md, TROUBLESHOOTING.md, ENHANCEMENTS.md, databricks_mcp/, tests/, examples/, scripts/, pyproject.toml, .venv/, .mcp.json, and NO /databricks-mcp/ folder.

**AC #6:** Given the cleaned structure, when I check MCP server best practices, then the project has README.md at root, single pyproject.toml at root, and follows standard MCP server layout.

---

## Implementation Details

### Tasks / Subtasks

- [x] Move documentation to root: `mv databricks-mcp/README.md ./` (AC: #1)
- [x] Move quick start guide: `mv databricks-mcp/QUICK_START.md ./` (AC: #1)
- [x] Move troubleshooting: `mv databricks-mcp/TROUBLESHOOTING.md ./` (AC: #1)
- [x] Move enhancements: `mv databricks-mcp/ENHANCEMENTS.md ./` (AC: #1)
- [x] Check test_server.sh location: `test -f test_server.sh || mv databricks-mcp/test_server.sh ./` (AC: #2)
- [x] Compare pyproject.toml files: `diff pyproject.toml databricks-mcp/pyproject.toml` (AC: #3)
- [x] Verify files identical before deletion (AC: #3)
- [x] Delete orphaned folder: `rm -rf databricks-mcp/` (AC: #4)
- [x] Verify clean root structure: `ls -la` (AC: #5)
- [x] Verify MCP best practices compliance (AC: #6)

### Technical Summary

**Issue:** Incomplete file migration left documentation and configuration files in old /databricks-mcp/ subfolder. This creates:
- Non-standard MCP server structure (missing root README)
- Duplicate configuration files (ambiguity about source of truth)
- Orphaned directory with obsolete content
- Potential confusion for contributors

**Solution:** Complete the file migration by moving all user-facing documentation to root and removing the obsolete folder entirely.

**Approach:**
1. Move all markdown documentation files to root
2. Verify configuration files are identical (safety check)
3. Delete duplicates and entire /databricks-mcp/ folder
4. Verify final structure matches MCP best practices

**Key Decisions:**
- Keep root versions of all configuration files (pyproject.toml, uv.lock)
- Delete /databricks-mcp/docs/ folder (separate from /docs/ brownfield documentation)
- Delete log files (local_mcp_stderr*.log) as they're obsolete

### Project Structure Notes

- **Files to modify:**
  - Move: README.md, QUICK_START.md, TROUBLESHOOTING.md, ENHANCEMENTS.md, test_server.sh
  - Delete: databricks-mcp/ (entire folder)
- **Expected test locations:** None (this is file organization, no tests needed)
- **Estimated effort:** 2 story points (0.5-1 day)
- **Prerequisites:** None (can run independently or after Story 1)

### Key Code References

**No code changes** - This story is purely file reorganization.

**Files Affected:**
- Documentation: README.md, QUICK_START.md, TROUBLESHOOTING.md, ENHANCEMENTS.md
- Configuration: pyproject.toml (verify identical), uv.lock (verify identical)
- Utilities: test_server.sh

**MCP Best Practices Reference:**
- Standard MCP servers have README.md at root
- Configuration at root (pyproject.toml, package.json, etc.)
- Source code in named package directory
- No nested project folders

---

## Context References

**Tech-Spec:** [tech-spec.md](../docs/tech-spec.md) - Primary context document containing:

- Complete file paths for all files to move
- List of duplicate files to delete
- MCP server best practices checklist
- Final root structure diagram

**Architecture:** See tech-spec.md "Implementation Details → Source Tree Changes" for complete file migration plan

---

## Dev Agent Record

### Agent Model Used

<!-- Will be populated during dev-story execution -->

### Debug Log References

**Implementation Plan:**
1. Check current state of databricks-mcp/ folder and what files exist
2. Move all documentation files (README.md, QUICK_START.md, TROUBLESHOOTING.md, ENHANCEMENTS.md) to root
3. Check test_server.sh location and move if needed
4. Compare pyproject.toml files to verify they're identical before deletion
5. Delete entire databricks-mcp/ folder
6. Verify final root structure matches MCP best practices

**Safety Checks:**
- Verify files exist before moving (prevent errors)
- Compare configuration files before deleting duplicates
- Confirm README.md won't be overwritten (we have README_original.md symlinked as README.md)

### Completion Notes

**File consolidation and cleanup completed successfully.**

**Key Actions:**
- Moved 3 documentation files to root: QUICK_START.md, TROUBLESHOOTING.md, ENHANCEMENTS.md
- Moved test_server.sh utility to root
- Verified pyproject.toml and uv.lock files were identical between root and databricks-mcp/
- README.md already at root (symlinked to README_original.md, identical to databricks-mcp/README.md)
- Deleted entire databricks-mcp/ folder including .git, docs/, log files, and duplicate configs

**Structure Verification:**
- ✓ README.md at root (MCP best practice)
- ✓ Single pyproject.toml at root (no duplicates)
- ✓ Source code in databricks_mcp/ package directory
- ✓ No nested project folders
- ✓ Standard MCP server layout achieved

**Removed Items:**
- databricks-mcp/ folder (entire directory)
- databricks-mcp/.git/ (obsolete git history)
- databricks-mcp/docs/ (duplicate documentation)
- local_mcp_stderr*.log files (obsolete logs)
- Duplicate pyproject.toml and uv.lock files

### Files Modified

**Moved to Root:**
- `QUICK_START.md` - Quick start guide
- `TROUBLESHOOTING.md` - Troubleshooting documentation
- `ENHANCEMENTS.md` - Enhancement documentation
- `test_server.sh` - Server testing utility

**Deleted:**
- `databricks-mcp/` - Entire folder including all subdirectories and files

**Unchanged:**
- `README.md` - Already at root (symlink to README_original.md)
- `pyproject.toml` - Root version retained (duplicate removed)

### Test Results

**File Organization Verification (All Passed):**
- AC #1: ✓ Documentation files at root
- AC #2: ✓ test_server.sh at root
- AC #3: ✓ Configuration files verified identical before deletion
- AC #4: ✓ databricks-mcp/ folder successfully deleted
- AC #5: ✓ Clean root structure verified
- AC #6: ✓ MCP best practices compliance confirmed

No unit tests required for this file organization story.

---

## Review Notes

<!-- Will be populated during code review -->

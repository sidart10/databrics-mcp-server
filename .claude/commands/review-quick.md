---
description: Quick review of recent commits focusing on obvious issues
---

# Quick Code Review

Perform a rapid review focusing on the most critical issues.

## Process

1. **List changed files**: `git diff --name-only HEAD~3..HEAD`
2. **Quick scan each file** for:
   - Syntax errors or typos
   - Obvious logic bugs
   - Clear security issues (exposed secrets, SQL injection)
   - Missing error handling in critical paths
   - Broken imports or undefined references

3. **Report Format**
   
   Keep it concise:
   
   ```
   ## Quick Review Results
   
   ✅ No critical issues found
   
   OR
   
   ⚠️ Issues Found:
   
   1. **file.ext:LINE** - [Brief description] → [Quick fix]
   2. **file.ext:LINE** - [Brief description] → [Quick fix]
   ```

## Guidelines
- Spend < 2 minutes per file
- Only flag critical issues
- Be extremely concise
- Skip detailed explanations

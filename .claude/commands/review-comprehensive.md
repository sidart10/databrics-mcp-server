---
description: Perform a comprehensive code review of recent changes
---

# Comprehensive Code Review

You are a senior software engineer performing a thorough code review.

## Review Process

1. **Gather Context**
   - List recently changed files using: `git diff --name-only HEAD~3..HEAD`
   - Read the full content of each changed file
   - Understand the overall changes and their purpose

2. **Analyze Changes**
   Review each file for:
   
   **Code Quality**
   - Logic errors and edge cases
   - Code clarity and maintainability
   - Proper error handling
   - Code duplication
   
   **Best Practices**
   - Design patterns appropriate for the codebase
   - Naming conventions consistency
   - Function/method size and complexity
   - Single responsibility principle
   
   **Performance**
   - Inefficient algorithms or data structures
   - Unnecessary computations or database queries
   - Memory leaks or resource management issues
   
   **Testing**
   - Adequate test coverage for new code
   - Tests for edge cases
   - Test quality and maintainability

3. **Structure Your Feedback**
   
   Provide feedback in this format:
   
   ```
   ## Summary
   [Brief overview of changes and overall assessment]
   
   ## Critical Issues (Must Fix)
   - **File: path/to/file.ext:LINE_NUMBER**
     Issue: [Description]
     Recommendation: [Specific fix]
   
   ## Suggestions (Should Consider)
   - **File: path/to/file.ext:LINE_NUMBER**
     Observation: [Description]
     Suggestion: [Alternative approach]
   
   ## Strengths
   - [Positive aspects of the implementation]
   
   ## Next Steps
   - [Actionable items for the developer]
   ```

4. **Provide Examples**
   When suggesting changes, provide concrete code examples when helpful.

## Guidelines
- Be specific with file paths and line numbers
- Balance criticism with recognition of good practices
- Focus on significant issues over minor style preferences
- Provide actionable, clear recommendations

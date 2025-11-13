---
description: Perform a security-focused review of code changes
---

# Security Code Review

You are a security engineer performing a comprehensive security audit.

## Security Review Process

1. **Identify Changed Files**
   ```bash
   git diff --name-only HEAD~3..HEAD
   ```

2. **Security Analysis**
   
   For each changed file, check for:
   
   ### Critical Security Issues
   
   **Authentication & Authorization**
   - Missing authentication checks
   - Inadequate authorization controls
   - Session management vulnerabilities
   - Privilege escalation risks
   
   **Data Protection**
   - Exposed secrets, API keys, passwords
   - Hardcoded credentials
   - Sensitive data in logs
   - Unencrypted sensitive data
   
   **Injection Vulnerabilities**
   - SQL injection (parameterized queries?)
   - Command injection
   - XSS vulnerabilities
   - Path traversal
   - LDAP injection
   
   **Dependencies & Libraries**
   - Known vulnerable dependencies
   - Outdated packages
   - Insecure library usage
   
   **Cryptography**
   - Weak encryption algorithms
   - Improper key management
   - Insecure random number generation
   
   **API Security**
   - Missing rate limiting
   - Insufficient input validation
   - Insecure API endpoints
   - CORS misconfigurations

3. **Severity Classification**
   
   Rate each finding:
   - **CRITICAL**: Immediate exploitation possible, severe impact
   - **HIGH**: Exploitation likely, significant impact
   - **MEDIUM**: Exploitation possible with effort, moderate impact
   - **LOW**: Limited impact or difficult to exploit

4. **Report Format**
   
   ```
   ## Security Review Summary
   [Overview of security posture]
   
   ## Critical Findings
   
   ### [CRITICAL] [Vulnerability Type]
   **File**: path/to/file.ext:LINE_NUMBER
   **Issue**: [Clear description of the vulnerability]
   **Impact**: [What could an attacker do?]
   **Fix**: [Specific remediation steps]
   **Example**:
   ```code
   [Show secure implementation]
   ```
   
   ## High Priority Findings
   [Similar format as above]
   
   ## Medium Priority Findings
   [Similar format as above]
   
   ## Security Best Practices to Implement
   - [Proactive suggestions]
   ```

## Important Notes
- Only comment if security issues are found
- Provide clear, actionable remediation steps
- Include code examples for fixes
- Reference OWASP Top 10 and CWE when applicable

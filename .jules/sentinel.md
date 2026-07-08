# Sentinel Security Journal

## 2025-05-15 - [IDOR and CSRF in Alternate Email Management]
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF) in the alternate email management functionality.
**Learning:** Records were being accessed and deleted using only their primary ID without verifying the course context. Additionally, state-changing actions were missing CSRF protection, and the entry point allowed execution of arbitrary methods via dynamic dispatch.
**Prevention:** Always scope database lookups to the current context (e.g., `courseid`). Implement strict whitelisting for dynamic method calls and enforce `require_sesskey()` for all state-changing operations.

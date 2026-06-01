## 2025-02-12 - Hardening Alternate Email against IDOR and CSRF
**Vulnerability:** Insecure Direct Object Reference (IDOR) and missing Cross-Site Request Forgery (CSRF) protection in alternate email management.
**Learning:** Method signatures like `get_one($id)` that lack context IDs (like `courseid`) allow users to manipulate records outside their authorized scope. Dynamic method calls in entry points (e.g., `class::$action(...)`) can bypass security checks if not strictly whitelisted and session-verified.
**Prevention:** Always include context IDs in database lookup methods and scope delete operations. Enforce `require_sesskey()` for all state-changing actions and use an explicit whitelist for any dynamic method dispatching.

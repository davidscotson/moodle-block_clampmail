## 2026-06-29 - Fixed IDOR and CSRF in alternate email management
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF).
**Learning:** Method calls via dynamic variables (e.g., `$class::$action()`) should use a strict whitelist instead of `method_exists()` to prevent unauthorized code execution. All state-changing actions, including redirects to them, must be protected with `sesskey`. Database lookups and deletions must always be scoped by context (e.g., `courseid`) to prevent cross-tenant/context manipulation.
**Prevention:** Use `PARAM_ALPHA` for action parameters, implement explicit whitelists for dynamic method calls, call `require_sesskey()` for all state-changing actions, and include context IDs in all `$DB` queries.

## 2025-05-14 - IDOR and CSRF in alternate email management
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF) in the alternate email management interface.
**Learning:** The `get_one` helper method only used the record's primary ID, allowing cross-course access. Deletion actions lacked session key validation. Dynamic method calls in `alternate.php` relied on `method_exists` without a whitelist, increasing the attack surface.
**Prevention:** Always scope database operations with a context ID (e.g., `courseid`). Use `require_sesskey()` for all state-changing actions. Use explicit whitelists and strict parameter types (e.g., `PARAM_ALPHA`) for dynamic method calls.

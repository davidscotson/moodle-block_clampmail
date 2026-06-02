## 2025-05-14 - Scoping and CSRF in Multi-Tenant Contexts
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF).
**Learning:** Checking user capabilities (e.g., `require_capability`) is insufficient if the subsequent database operations (like `get_record` or `delete_records`) only use the primary ID of the record. Attackers can bypass intent by providing IDs from other contexts (courses). Additionally, dynamic method invocation based on user-provided 'action' parameters allows calling internal class methods if not strictly whitelisted.
**Prevention:**
1. Always scope DB lookups with a context ID (e.g., `courseid`).
2. Whitelist allowed actions in entry points.
3. Call `require_sesskey()` for all state-changing actions and ensure referring URLs include the `sesskey` parameter.
4. Distinguish between internal state changes (requiring CSRF protection) and external triggers like email verification (which may not have a session).

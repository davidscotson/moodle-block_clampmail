## 2025-05-15 - Whitelisting Dynamic Method Calls and Scoped IDOR Mitigation
**Vulnerability:** Dynamic class method execution via unsanitized user input and unscoped database record retrieval by ID.
**Learning:** Relying on `method_exists` for action dispatching allows execution of any public method, which can bypass intended logic. Similarly, fetching records by ID alone in a multi-tenant environment (like Moodle courses) leads to Insecure Direct Object Reference (IDOR).
**Prevention:** Use explicit whitelists for dynamic method dispatching. Always scope database lookups and deletions using context-specific identifiers (e.g., `courseid`, `userid`) in addition to the primary record ID.

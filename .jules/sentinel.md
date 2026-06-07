## 2026-06-07 - IDOR and CSRF in Alternate Email Management
**Vulnerability:** Insecure Direct Object Reference (IDOR) via lack of course-scoping in `get_one($id)` and missing CSRF protection (`require_sesskey()`) on email-sending and deletion actions.
**Learning:** Using a primary key alone for record retrieval in a multi-tenant environment (like Moodle courses) allows cross-tenant data access. Loose parameter types (PARAM_TEXT) on dynamic method calls allow for broader-than-intended method execution.
**Prevention:** Always scope database lookups with a context ID (e.g., `courseid`). Enforce `require_sesskey()` for any state-changing action and whitelist valid actions for dynamic method dispatching.

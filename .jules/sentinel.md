## 2025-01-24 - Secure Dynamic Action Dispatching
**Vulnerability:** Dynamic class method execution based on unsanitized user input (`$class::$action(...)`) allowed potential execution of unauthorized internal methods.
**Learning:** Even if `method_exists` is checked, it doesn't distinguish between intended public actions and internal class methods.
**Prevention:** Implement a strict whitelist of allowed action strings (ideally using class constants) and verify the input against this whitelist before dispatching.

## 2025-01-24 - Context-Scoped Record Retrieval (IDOR)
**Vulnerability:** Records were retrieved or deleted using only their primary ID, allowing Insecure Direct Object Reference (IDOR) across different course contexts.
**Learning:** In Moodle, record IDs are often predictable, so relying solely on them for state-changing operations is insufficient.
**Prevention:** Always include a context identifier (e.g., `courseid`, `userid`) in the `$DB` query criteria to ensure the operation is scoped to the authorized context.

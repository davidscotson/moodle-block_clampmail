## 2025-01-24 - Security Hardening of Alternate Email Management
**Vulnerability:** IDOR in record retrieval, missing CSRF on email deletion/triggering, and loose dynamic method execution.
**Learning:** Relying on primary keys without context scoping (course ID) leads to IDOR. Missing session key validation on state-changing actions enables CSRF. Using generic `method_exists` for dynamic routing is insufficient if the class has other public methods.
**Prevention:** Always context-scope database queries (e.g., `get_record('table', ['id' => $id, 'courseid' => $courseid])`). Enforce strict allow-lists for dynamic calls. Use `require_sesskey()` for all actions that change state or trigger side effects.

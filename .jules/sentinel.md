## 2025-05-15 - Enforcing Context Scoping in Database Lookups
**Vulnerability:** Insecure Direct Object Reference (IDOR) via unscoped record lookups.
**Learning:** The `alternate::get_one($id)` method only used the record's primary ID, allowing cross-course data access if an attacker could guess or find valid IDs.
**Prevention:** Always include a context-specific identifier (like `courseid`) in the signature and query of lookup methods (e.g., `get_one($courseid, $id)`). Ensure all state-changing operations verify this scoped record before proceeding.

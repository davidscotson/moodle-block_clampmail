## 2025-05-15 - Dynamic Method Dispatch and IDOR in Course Context

**Vulnerability:** The `alternate.php` script used a user-provided `action` parameter to dynamically call methods on the `block_clampmail\alternate` class without whitelisting. Additionally, the `get_one` method and subsequent deletions did not enforce course-level scoping, allowing for Insecure Direct Object Reference (IDOR) attacks.

**Learning:** Dynamic method dispatching based on user input (e.g., `$class::$action(...)`) is dangerous unless the `action` is strictly whitelisted. Even with `require_login()`, failing to include context identifiers like `courseid` in database lookups and deletions allows users to manipulate data belonging to other contexts.

**Prevention:** Always use an explicit whitelist for dynamic method calls. Ensure all database operations (`get_record`, `delete_records`, etc.) include a context ID (like `courseid`) in the parameters to enforce proper authorization boundaries.

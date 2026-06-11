## 2025-05-14 - Scoping database lookups to prevent IDOR
**Vulnerability:** Insecure Direct Object Reference (IDOR) where users could access or delete records (like alternate emails or drafts) in other courses by manipulating the record ID in the URL or form data.
**Learning:** Even when `require_login($course)` and capability checks are present, database operations must be explicitly scoped to the verified context (e.g., `courseid`) to prevent cross-context data manipulation.
**Prevention:** Update record retrieval and deletion methods to always require and verify the context ID (course or user) alongside the record's primary ID.

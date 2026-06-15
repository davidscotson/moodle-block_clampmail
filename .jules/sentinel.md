## 2025-05-14 - Scoping Database Operations to Context
**Vulnerability:** Insecure Direct Object Reference (IDOR) via unscoped primary key lookups and deletions.
**Learning:** In Moodle plugins, relying solely on an record's `id` for retrieval or deletion (e.g., `$DB->get_record('table', ['id' => $id])`) allows users to access or modify data across different contexts (courses) by tampering with the ID.
**Prevention:** Always include a context identifier (like `courseid`) in the selection criteria for both retrieval and state-changing database operations to ensure they are restricted to the intended environment.
>>>>>>> REPLACE

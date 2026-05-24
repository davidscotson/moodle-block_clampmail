## 2025-01-24 - CSRF and IDOR in Alternate Email Management
**Vulnerability:** Alternate email deletion lacked CSRF protection (missing sesskey), and multiple operations were susceptible to IDOR as they relied solely on the record ID without scoping to the course context.
**Learning:** Even within a course context, database operations like `get_record` and `delete_records` must explicitly include the context ID (e.g., `courseid`) to prevent cross-course data manipulation.
**Prevention:** Always include `sesskey` in URLs for state-changing actions and use `require_sesskey()` in the handler. Scope all database lookups by the relevant context ID.

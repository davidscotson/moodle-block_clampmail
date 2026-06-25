## 2026-06-25 - [IDOR and CSRF in alternate email management]
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF).
**Learning:** Records were looked up by ID only, allowing cross-course access. Actions were triggered via URLs without session keys.
**Prevention:** Always scope database lookups with a context ID (like courseid) and enforce require_sesskey() for all state-changing actions.

## 2026-07-04 - Fix IDOR and CSRF in alternate email management
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF).
**Learning:** Method names from user input without whitelisting allowed execution of any class method. Scoping record lookups only by record ID allowed users to access data across different courses.
**Prevention:** Always whitelist allowed actions, use `require_sesskey()` for state-changing actions, and include context IDs (like `courseid`) in all database lookups and deletions.

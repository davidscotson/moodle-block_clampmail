## 2025-01-24 - [IDOR and CSRF Protection in Alternate Emails]
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF) in the alternate email management logic.
**Learning:** The `get_one` method and state-changing actions (`confirmed`, `verify`, `inform`) lacked context scoping (course ID) and session key verification. This allowed potential manipulation of records across different courses and unauthorized action execution.
**Prevention:** Always scope database lookups for specific records using the relevant context (e.g., course ID) and protect all state-changing or sensitive operations with `require_sesskey()` in the processing logic and `sesskey()` in the referring URLs.

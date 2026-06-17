## 2025-05-14 - Mitigating IDOR and CSRF in Moodle Plugins
**Vulnerability:** Insecure Direct Object Reference (IDOR) and missing Cross-Site Request Forgery (CSRF) protection in alternate email management.
**Learning:** Method names from user input were used for dynamic calls without strict whitelisting. Database records were accessed by ID without scoping to the current course context.
**Prevention:** Always use `PARAM_ALPHA` for action parameters, whitelist allowed methods, enforce `require_sesskey()` for state-changing actions, and include the course ID in all `$DB` lookups and deletions.

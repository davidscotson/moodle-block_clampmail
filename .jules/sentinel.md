# Sentinel's Journal - Critical Security Learnings

## 2025-05-15 - [HIGH] CSRF and IDOR in Alternate Email Management

**Vulnerability:**
1. Insecure Direct Object Reference (IDOR) in `get_one` allowed retrieving alternate email records from any course by only knowing the record ID.
2. Cross-Site Request Forgery (CSRF) in state-changing actions (`confirmed` for deletion and `inform` for sending verification emails) due to missing `require_sesskey()` checks.
3. Improper Input Validation in `alternate.php` where the `action` parameter was `PARAM_TEXT` and lacked whitelisting, potentially allowing unauthorized method execution via dynamic calls.

**Learning:**
In Moodle plugins, record IDs alone are insufficient for security; database operations must always be scoped by a context ID (like `courseid`). Furthermore, any action with side effects (even sending an email) must be protected by `sesskey`. Dynamic method calls (e.g., `class::$action(...)`) are dangerous without an explicit whitelist.

**Prevention:**
1. Always include `courseid` or `userid` in `$DB` queries to ensure context-level isolation.
2. Call `require_sesskey()` at the start of any action that modifies state or performs significant side effects.
3. Use `PARAM_ALPHA` and an explicit whitelist for parameters that determine which method or file to execute.
4. Ensure all links/redirects to state-changing actions include the `sesskey` parameter.

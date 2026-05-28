## 2025-05-14 - [IDOR and CSRF in dynamic actions]
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF) in the alternate email management interface. Actions like deletion and sending verification emails were only scoped by record ID and lacked session key validation.
**Learning:** Dynamic method calls based on user input (e.g., `Class::$action(...)`) can bypass security checks if not coupled with an explicit whitelist and mandatory session validation for state-changing actions.
**Prevention:** Always use a whitelist for dynamic method calls, enforce `require_sesskey()` for any action that modifies data or triggers external side effects, and ensure all database lookups are scoped by context ID (e.g., `courseid`) in addition to primary keys.

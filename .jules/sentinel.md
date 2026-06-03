## 2024-05-24 - IDOR and CSRF Hardening in Alternate Email Management
**Vulnerability:** Insecure Direct Object Reference (IDOR) in `get_one` and missing CSRF protection (`sesskey`) on state-changing actions in `alternate.php`.
**Learning:** Even with `require_login($course)` and capability checks at the entry point, individual database lookups must be scoped to the context (e.g., `courseid`) to prevent users from accessing or deleting records in other courses by manipulating IDs. Additionally, any action that triggers a state change or an external side effect (like sending an email) must be protected by `require_sesskey()`.
**Prevention:**
1. Always include context IDs (like `courseid` or `userid`) in `$DB->get_record` and `$DB->delete_records` calls.
2. Explicitly set context IDs in data objects returned from forms before database operations.
3. Use `require_sesskey()` in handlers and `sesskey()` in URLs for all state-changing or notification-triggering actions.
4. Use an allowlist for dynamic method calls based on URL parameters.

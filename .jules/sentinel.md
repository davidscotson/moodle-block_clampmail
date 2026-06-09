## 2025-05-15 - IDOR and CSRF in Alternate Emails
**Vulnerability:** The `alternate.php` entry point and its associated `block_clampmail\alternate` class had several security gaps. `get_one` did not verify record ownership by `courseid` (IDOR), and state-changing actions (`CONFIRMED`, `INFORMATION`) lacked `require_sesskey()` protection (CSRF).

**Learning:** Dynamic method calls based on user input (e.g., `alternate::$action(...)`) require strict whitelisting and session key validation for any action that modifies state or triggers sensitive processes like sending emails.

**Prevention:** Always scope database operations with context IDs (like `courseid`) to prevent IDOR. Enforce `require_sesskey()` for all state-changing actions and use appropriate `PARAM_*` types (like `PARAM_ALPHA`) for dynamic parameters.

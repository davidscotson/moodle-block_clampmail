## 2025-05-15 - Hardening Alternate Email Management and Course Configuration

**Vulnerability:** Cross-Site Request Forgery (CSRF) and Insecure Direct Object Reference (IDOR) in `alternate.php` and `config.php`. State-changing actions lacked `sesskey` validation, and record lookups/deletions relied solely on record IDs without course context verification.

**Learning:** Moodle's `moodleform` provides automatic CSRF protection, but actions triggered via direct URLs or custom links (like "reset" or "confirm delete") require manual `require_sesskey()` calls and explicit `sesskey` parameter inclusion in URLs. Furthermore, record-level security must always include a context identifier (e.g., `courseid`) in `$DB` queries to prevent attackers from accessing or modifying records in courses they do not have permissions for by simply guessing IDs.

**Prevention:** Always use `require_sesskey()` for any state-changing logic outside of standard form processing. Scope all database operations using both the record ID and a context ID (like `courseid`) derived from the verified session context. Use explicit whitelisting for dynamic action dispatching to prevent execution of unauthorized methods.

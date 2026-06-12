## 2025-05-14 - [IDOR and CSRF Hardening in block_clampmail]
**Vulnerability:** Insecure Direct Object Reference (IDOR) and missing CSRF protection in `alternate.php`. Record lookups and deletions were performed solely by ID without verifying course context, and state-changing actions lacked `sesskey` checks.
**Learning:** Even with `require_login($course)` at the entry point, individual database operations must be scoped with a context ID (like `courseid`) to prevent users from accessing or modifying records in other courses via ID manipulation.
**Prevention:** Always include a context ID (e.g., `courseid`) in `$DB` method criteria and require `sesskey()` for all actions that modify state. Whitelist allowed actions rather than using `method_exists`.

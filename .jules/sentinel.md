# Sentinel's Journal

## 2025-05-14 - IDOR and CSRF Hardening in Alternate Email Management
**Vulnerability:** Insecure Direct Object Reference (IDOR) in `get_one` method and missing CSRF protection on state-changing actions (`confirmed`, `inform`). Dynamic method execution in `alternate.php` was also unvalidated.
**Learning:** Generic getter methods like `get_one($id)` are dangerous if they don't enforce context (e.g., `courseid`). Dynamic action dispatching using `optional_param` without a strict whitelist allows execution of unintended class methods.
**Prevention:** Always include context IDs (like `courseid`) in database lookups and deletions. Enforce `require_sesskey()` for all state-changing actions. Use a strict whitelist of allowed method names for dynamic dispatching.

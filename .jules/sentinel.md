## 2025-05-15 - Hardening Dynamic Method Dispatch and Record Scoping
**Vulnerability:** Insecure Direct Object Reference (IDOR) and arbitrary method execution via dynamic calls (`$class::$action(...)`) and unscoped database lookups.
**Learning:** In Moodle plugins, relying on a primary record ID without verifying its association with the current `courseid` or `contextid` allows users to access/modify data across different courses. Furthermore, dynamic method calls based on user input (even if `method_exists` is checked) can expose internal class logic if not strictly whitelisted.
**Prevention:**
1. Always whitelist allowed actions for dynamic dispatch.
2. Use `PARAM_ALPHA` for action parameters.
3. Enforce `courseid` or `contextid` in all `$DB` lookup and deletion parameters (e.g., `get_record('table', ['id' => $id, 'courseid' => $courseid])`).
4. Derive context IDs from the verified session context rather than trusting user-supplied form data.

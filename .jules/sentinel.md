## 2025-05-15 - Dynamic Method Dispatch and IDOR Protection
**Vulnerability:** IDOR in record lookups/deletions and CSRF/RCE risk in dynamic method calls.
**Learning:** dynamic method calls using `$body = class::$action(...)` are dangerous if `$action` is not whitelisted. State-changing actions must be protected by `require_sesskey()`, except for email verification links which lack session context. Record operations must always be scoped by both course and user context.
**Prevention:**
1. Whitelist all allowed actions for dynamic dispatch.
2. Use `require_sesskey()` for actions like deletion or updates.
3. Scope database queries with `courseid` and `userid` (e.g., `['id' => $id, 'courseid' => $courseid]`).
4. Use `$context->get_course_context()->instanceid` for robust course ID retrieval.

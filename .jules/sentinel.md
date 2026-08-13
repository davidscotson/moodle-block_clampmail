## 2026-03-31 - [CLAMPmail IDOR & CSRF Mitigation]
**Vulnerability:** Insecure Direct Object References (IDOR) and Cross-Site Request Forgery (CSRF) in action dispatchers, signature loaders, alternate email records, and email logs.
**Learning:** Moodle blocks with custom action-dispatch entry points (like `alternate.php`) are susceptible to unauthorized method calls when dynamic dispatching is used without strict whitelisting. Furthermore, querying records by unique database IDs (`id`) without constraining the query to active context fields (`courseid` and `userid`) allows cross-user and cross-course privilege escalation and data manipulation.
**Prevention:**
1. Always whitelist actions against class constants prior to dynamic dispatching and use stricter input parameter parameters (such as `PARAM_ALPHA` instead of `PARAM_TEXT`).
2. Constrain all record queries for display, modification, or deletion to the active context fields using `$DB->get_record(..., ['id' => $id, 'courseid' => $courseid, 'userid' => $userid], '*', MUST_EXIST)`.
3. Protect all state-changing actions via `require_sesskey()` and ensure all generated confirmation or redirection URLs append the correct session key.

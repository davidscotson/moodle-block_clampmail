# Sentinel Security Journal

## 2026-08-01 - IDOR on Draft and Log Email Management in CLAMPMail
**Vulnerability:** Insecure Direct Object Reference (IDOR) on loading, viewing, deleting, and confirming email drafts or logs. Because these entries are scoped to courses and specific users, allowing retrieval using only a numeric database ID (`typeid`) without scoping by `courseid` or checking ownership against `$USER->id` allowed users to unauthorizedly read or delete other users' or other courses' private email drafts and logs.
**Learning:** Moodle page-level course context and capability checks (like checking if a user has the `cansend` capability in a course context) do NOT automatically protect individual record lookups. Standard `$DB->get_record` or `$DB->delete_records` calls must explicitly incorporate user ownership constraints (`userid`) and course context constraints (`courseid`).
**Prevention:** Always restrict record retrievals to the verified `$course->id` and user ownership context (e.g. `$USER->id` unless the user has administrative override/impersonation capabilities). Utilize Moodle's `MUST_EXIST` flag to guarantee fail-secure exception throwing.

## 2026-03-05 - Insecure Direct Object Reference (IDOR) on Loading Drafts and Logs
**Vulnerability:** Loading course-specific draft or history records using only an input ID (`typeid`) allows users to access and manipulate draft or log entries belonging to other users or other courses.
**Learning:** Checking Moodle course context and capability checks on the page level is not sufficient if database lookups do not incorporate the course context and user ownership constraints.
**Prevention:** Always scope database record lookups to the verified `$course->id` and use the `MUST_EXIST` flag. Explicitly verify that the record's user ID matches the current `$USER->id` or that the user has specific admin/impersonation permissions (`block/clampmail:canimpersonate`).

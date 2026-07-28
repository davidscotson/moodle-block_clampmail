# Sentinel Security Journal

## 2026-07-27 - IDOR and CSRF Vulnerabilities in Course Alternate Emails
**Vulnerability:** Course alternate emails could be fetched, updated, or deleted without verifying that the ID belongs to the current course context. Also, state-changing actions like confirming deletion or requesting confirmation emails lacked session key verification.
**Learning:** Method calls were retrieving records using only `id` without verifying course-level ownership (`courseid`), resulting in Insecure Direct Object Reference (IDOR). Additionally, some state-changing URLs were accessed via GET requests without checking `sesskey()`.
**Prevention:** Always verify ownership of resource IDs against the active context ID before allowing access, updates, or deletions. Validate dynamic actions against a strict whitelist and enforce `require_sesskey()` on all state-changing endpoints in Moodle.

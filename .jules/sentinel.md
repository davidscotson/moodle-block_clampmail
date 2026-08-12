## 2026-03-31 - [Alternate Email IDOR and CSRF Fix]
**Vulnerability:**
- Insecure Direct Object Reference (IDOR) on alternate email records due to `get_one` only using the record ID without scoping the query to the course context, and lack of course context checking on database deletions and updates.
- Cross-Site Request Forgery (CSRF) on `confirmed` and `inform` actions in alternate email handling due to missing `require_sesskey()` validation.

**Learning:**
- Moodle plugins must enforce course context isolation explicitly when loading records for deletion or modification by querying both the primary record ID and the active `courseid` to mitigate Insecure Direct Object Reference (IDOR) vulnerabilities.
- State-changing actions triggered via direct URLs must validate the Moodle session key (`require_sesskey()`) to prevent CSRF attacks.

**Prevention:**
- Always parameterize DB loading/deleting methods with course/user contexts (e.g. `$DB->get_record('table', ['id' => $id, 'courseid' => $courseid], '*', MUST_EXIST)`).
- Ensure any action dispatched via URL or GET parameter that modifies the database state is protected with `require_sesskey()` and that the invoking URLs explicitly incorporate `'sesskey' => sesskey()`.

## 2025-05-15 - IDOR in Alternate Email Management

**Vulnerability:** Insecure Direct Object Reference (IDOR) in `alternate.php` allowed users with `block/clampmail:allowalternate` capability to view, edit, or delete alternate email records in any course by manipulating the `id` parameter or hidden form fields.

**Learning:** The application relied on `id` as a primary key for database operations without scoping queries to the current `courseid`. Moodle's `moodleform` returns data from hidden fields in `get_data()`, which can be tampered with by users if not re-validated against the session context.

**Prevention:** Always include and verify context-specific identifiers (like `courseid`) in database queries (`$DB->get_record`, `$DB->delete_records`). When processing form data, explicitly override sensitive context IDs in the `$data` object using verified values from the current session/page context before performing database updates.

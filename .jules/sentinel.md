## 2025-05-15 - [IDOR in Email Log and Draft Management]
**Vulnerability:** Insecure Direct Object Reference (IDOR) in `emaillog.php` and `email.php` allowed unauthorized users to view or delete email logs and drafts belonging to other users by manipulating the `typeid` parameter.
**Learning:** The application relied solely on the record's primary key (`id`) for database operations (`$DB->get_record`, `$DB->delete_records`) without verifying that the record belonged to the current user.
**Prevention:** Always include ownership context (e.g., `'userid' => $USER->id`) in database queries for user-owned records. Use `MUST_EXIST` when fetching records by ID to ensure a fail-secure behavior if the record is missing or unauthorized.

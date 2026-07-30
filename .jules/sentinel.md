# Sentinel Security Journal

## 2025-02-14 - IDOR in Signature Management
**Vulnerability:** Insecure Direct Object Reference (IDOR) allowed any user to view, edit, or delete signatures belonging to other users by tampering with the `id` request parameter or form submission field.
**Learning:** Moodle forms and standard database update methods (e.g. `$DB->update_record`) do not automatically validate ownership of the record being acted upon. Developers must explicitly check that the record belongs to the active user (`$USER->id`) or that the user has proper administrative override capabilities.
**Prevention:** Always retrieve user-scoped records via parameters validated against the active session context (e.g., retrieving signatures using `$USER->id`) and strictly assert that any requested/submitted object ID exists within that user-owned set before performing any read, update, or deletion operation.

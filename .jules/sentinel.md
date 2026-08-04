# Sentinel Security Journal

This journal documents critical security learnings, vulnerability patterns, and prevention strategies specific to the CLAMPMail codebase.

## 2026-03-05 - IDOR and Missing CSRF Validation in Signature Management
**Vulnerability:** In signature.php, users could load or update any signature record by manipulating the signature ID parameter in the URL or the hidden form fields. Additionally, the deletion confirmation URL was missing a session key (sesskey), which caused deletion validation failures while leaving the page open to potential CSRF-like issues.
**Learning:** In Moodle, loading records using standard parameters (like optional_param('id')) or processing forms via `moodleform` requires explicit backend validation to verify that the retrieved/submitted record ID actually belongs to the active session user, as form submission properties and URL parameters can be easily tampered with.
**Prevention:** Always validate that requested IDs exist within the current user's authorized records array before loading, editing, or updating database records. Ensure all confirmation URLs generated via `$OUTPUT->confirm` explicitly incorporate Moodle's `sesskey()` parameter when they point to state-changing actions.

## 2026-07-17 - IDOR in Signature Management
**Vulnerability:** Insecure Direct Object Reference (IDOR) allowed any authenticated user to load, edit, take ownership of, or delete other users' email signatures by submitting or requesting their signature IDs.
**Learning:** The application lacked ownership validation against the current logged-in user context (`$USER->id`) when loading signatures or processing form submissions in `signature.php`.
**Prevention:** Enforce strict ownership validation when loading individual user-owned records (e.g., verifying that the record's user ID matches `$USER->id`) and validate form submission IDs against the active user session context prior to database modification.

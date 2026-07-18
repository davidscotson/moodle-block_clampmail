## 2025-03-06 - IDOR in Moodle Signature Updates

**Vulnerability:** Insecure Direct Object Reference (IDOR) via form data manipulation where arbitrary user signatures could be updated or overwritten by modifying the hidden `id` parameter during submission.

**Learning:** Moodle's database API methods (specifically `$DB->update_record`) execute updates blindly based on the object's primary key (`id`) and do not enforce user-level access controls or verify ownership of the record being updated.

**Prevention:** Always load the existing database record using `$DB->get_record` prior to executing `$DB->update_record`, and verify that the record's owner matches the currently logged-in user (`$USER->id`).

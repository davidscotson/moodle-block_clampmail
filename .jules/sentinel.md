## 2025-05-24 - IDOR and CSRF in Alternate Email Management
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF) in `alternate.php` and its supporting class.
**Learning:** Records were being retrieved and deleted using only their primary key (`id`) without verifying they belonged to the current course context (`courseid`). Additionally, several state-changing actions (`delete`, `confirmed`, `inform`) lacked CSRF protection.
**Prevention:** Always scope `$DB` operations with both the record ID and a context ID (like `courseid`). Enforce `require_sesskey()` for all state-changing actions and include the `sesskey` parameter in all links that trigger them.

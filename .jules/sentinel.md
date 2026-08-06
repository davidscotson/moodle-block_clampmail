# Sentinel Security Journal

This journal documents critical security learnings, vulnerability patterns, and prevention strategies specific to this codebase. Only critical security learnings are logged here.

## 2026-03-31 - IDOR and CSRF Mitigations in Alternate Email Address Management
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF) vulnerability in alternate email address operations (`alternate.php` and `classes/alternate.php`). The dynamic action dispatcher accepted unvetted alphanumeric inputs, and database lookups loaded/modified records based purely on an `id` parameter without verifying that the record belonged to the correct `courseid` context. Some state-changing actions lacked `sesskey` token validation.
**Learning:** In Moodle modules, course contextualization is essential for access control. Functions like `$DB->get_record` or `get_one` must include course identifiers (such as `courseid`) in their query filters to enforce course boundary separation. Dynamic action dispatchers must restrict input types to PARAM_ALPHA and perform strict whitelisting checks. State-changing GET or POST actions require `require_sesskey()` verification.
**Prevention:** Avoid single-parameter lookups for scoped records; always pass contextual identifiers (e.g., `courseid` or `userid`) alongside record IDs to secure database calls. Whitelist dispatchable actions against class constants and use `require_sesskey()` on state changes.

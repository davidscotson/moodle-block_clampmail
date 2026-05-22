## 2026-05-22 - [CSRF Vulnerability in Action Links]
**Vulnerability:** CSRF (Cross-Site Request Forgery) on state-changing actions (reset configuration, delete alternate email).
**Learning:** Actions triggered via simple links (`moodle_url`) often miss `sesskey` validation if not explicitly added.
**Prevention:** Always include `'sesskey' => sesskey()` in URLs for state-changing actions and use `require_sesskey()` at the start of the processing logic.

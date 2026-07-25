## 2026-03-31 - Action Hijacking and CSRF/IDOR Vulnerabilities in Alternate Emails

**Vulnerability:** Dynamic method dispatching without strict whitelisting allowed arbitrary method execution on the `block_clampmail\alternate` class. In addition, missing `require_sesskey()` checks on state-changing operations (`confirmed` delete action and `inform` notification action) exposed the application to CSRF, while direct lookup by ID without course scope verification exposed it to IDOR parameter tampering.

**Learning:** Combining dynamic dispatching with insecure dynamic method invocation of request parameters without an explicit whitelist is highly risky. Additionally, database operations must be context-scoped and protected by the session key check to maintain confidentiality and integrity.

**Prevention:** Enforce strict whitelisting using class constants for allowed action values, restrict action parameter types with `PARAM_ALPHA`, enforce `require_sesskey()` on state-changing endpoints, and include `courseid` in all record lookups to ensure authorization is scoped correctly to the course.

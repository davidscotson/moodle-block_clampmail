## 2024-05-16 - Securing Dynamic Method Calls and Alternate Emails
**Vulnerability:** Dynamic method dispatching without whitelisting, CSRF on state-changing actions, and IDOR in alternate email record management.
**Learning:** Using `method_exists()` for dynamic dispatching is insufficient; an explicit whitelist of allowed methods is required. Moodle state-changing actions (`CONFIRMED`, `INFORMATION`) must be protected with `require_sesskey()`, and database operations must be scoped with context IDs (like `courseid`) to prevent IDOR.
**Prevention:** Always use a whitelist for dynamic method calls. Enforce `require_sesskey()` for all actions that modify state. Scope all `$DB` lookups and deletions with appropriate context IDs.

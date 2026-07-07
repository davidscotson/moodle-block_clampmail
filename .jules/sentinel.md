## 2026-07-07 - Alternate Email Security Hardening
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF) in alternate email management.
**Learning:** Method calls derived from user parameters (e.g., `$action`) should be whitelisted, and sensitive record lookups must be scoped to the verified context (e.g., `courseid`) even if the record has a unique ID.
**Prevention:** Always use whitelists for dynamic method dispatching, and include context IDs in all database criteria for state-changing operations.

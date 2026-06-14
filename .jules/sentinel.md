## 2024-05-14 - [Securing Alternate Email Management]
**Vulnerability:** Insecure Direct Object Reference (IDOR) and Cross-Site Request Forgery (CSRF) in alternate email management.
**Learning:** Method signatures and database calls often lack context-specific scoping (like courseid), allowing unauthorized access to records in other contexts. Dynamic method calling without a whitelist can lead to unauthorized execution of class methods.
**Prevention:** Always scope database lookups and deletions with a context ID (e.g., courseid). Use require_sesskey() for all state-changing actions and whitelist allowed methods for dynamic dispatching.

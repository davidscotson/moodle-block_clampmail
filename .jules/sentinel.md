## 2025-05-23 - Insecure Direct Object Reference (IDOR) in Record Deletion and Loading
**Vulnerability:** Database operations (select, delete) were using only the record's primary ID without verifying course or user context.
**Learning:** In multi-tenant or multi-course applications like Moodle, relying solely on primary IDs for record access allows users to access or delete data belonging to other contexts by guessing the ID.
**Prevention:** Always include scoping parameters (e.g., `courseid`, `userid`) in database queries and use `MUST_EXIST` to ensure the application fails securely if the record is missing or access is unauthorized.

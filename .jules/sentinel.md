## 2024-05-14 - IDOR in course-level records
**Vulnerability:** Insecure Direct Object Reference (IDOR) in alternate email management allowed unauthorized access or deletion of records by manipulating the `id` parameter.
**Learning:** Records were retrieved and deleted using only the primary key `id`, without verifying they belonged to the current `courseid`.
**Prevention:** Always include a context-specific identifier (like `courseid`) in database queries for record retrieval and deletion to ensure the user has authority over the specific object within the current context.

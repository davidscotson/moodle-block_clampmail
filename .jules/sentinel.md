## 2025-05-15 - IDOR in Alternate Email Management
**Vulnerability:** Insecure Direct Object Reference (IDOR) in `block_clampmail\alternate::get_one`. The method only accepted an `id` and did not verify if the record belonged to the current course context.
**Learning:** Generic lookup methods in Moodle plugins that only use the primary key can be exploited to access or modify data across different courses or users if context is not enforced.
**Prevention:** Always include a context identifier (like `courseid`) in database lookup parameters and method signatures for entity retrieval.

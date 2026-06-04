## 2026-06-04 - [IDOR in Alternate Email Management]
**Vulnerability:** Insecure Direct Object Reference (IDOR) in `block_clampmail\alternate` methods. Specifically, the `confirmed` method allowed deleting any alternate email record by ID without verifying it belonged to the current course. Other methods relied on `get_one($id)` which also lacked course scoping.
**Learning:** Moodle plugins must always scope database operations (especially deletions and updates) with a context-defining ID (like `courseid` or `userid`) in addition to the record's primary key.
**Prevention:** Use composite keys in `WHERE` clauses for all record lookups and deletions: `['id' => $id, 'courseid' => $course->id]`.

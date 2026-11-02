## 2026-05-22 - SQL Injection in Group Filtering Query

**Vulnerability:** SQL injection vulnerability in `classes/groups.php` where group IDs were concatenated directly into a raw SQL `IN (...)` clause without parameterization.

**Learning:** Although group IDs returned by helper functions like `groups_get_user_groups()` are typically integers, interpolating or concatenating values directly into SQL strings violates defensive coding principles and risks SQL injection if data origins or helper behaviors change.

**Prevention:** Always use Moodle's `$DB->get_in_or_equal()` with prepared statement parameters for `IN (...)` SQL conditions rather than direct string concatenation.

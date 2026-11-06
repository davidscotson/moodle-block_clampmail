## 2026-11-06 - SQL Injection Prevention in Groups Query
**Vulnerability:** In `classes/groups.php`, `block_clampmail\groups::get_groups` concatenated array values directly into an `IN (...)` SQL clause using `implode(',', array_values($mygroups['0']))` without parameter binding or numeric sanitization.
**Learning:** Even when IDs originate from internal helper functions like `groups_get_user_groups()`, interpolating raw values directly into SQL strings bypasses database parameterization best practices and introduces potential SQL injection risks.
**Prevention:** Always use Moodle's `$DB->get_in_or_equal()` helper to generate placeholders and bound parameter arrays for `IN (...)` SQL queries instead of string concatenation.

## 2026-07-07 - SQL Injection Prevention in Groups Query
**Vulnerability:** Potential SQL injection in groups query (`classes/groups.php`) via unparameterized string concatenation into an `IN (...)` clause.
**Learning:** Even when IDs are expected to originate from internal functions like `groups_get_user_groups()`, constructing SQL clauses via `implode(',', ...)` without validation or parameterization creates SQL injection vulnerabilities.
**Prevention:** Always sanitize array elements using `array_filter(..., 'is_numeric')` and use Moodle's parameterized `$DB->get_in_or_equal()` helper for dynamic `IN (...)` SQL conditions.

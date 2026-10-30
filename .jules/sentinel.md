## 2025-05-18 - Parameterizing SQL IN clauses with get_in_or_equal()
**Vulnerability:** In `classes/groups.php`, group IDs were retrieved and directly concatenated into SQL queries using `implode(',', ...)` within `id IN (...)` without parameterization or numeric sanitization.
**Learning:** Direct string interpolation into `$DB->get_records_select()` bypasses Moodle's database abstraction layer parameter protections. Constructing SQL `IN (...)` conditions requires Moodle's `$DB->get_in_or_equal()` helper to bind values safely as prepared statement parameters.
**Prevention:** Always use `$DB->get_in_or_equal($ids)` when querying records using SQL `IN` statements, ensuring input lists are validated and passed as bound query parameters.

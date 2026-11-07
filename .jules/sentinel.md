## 2026-04-18 - Parameterized Role Selection in Email Compose

**Vulnerability:** In `email.php`, `$config['roleselection']` was directly interpolated into an SQL query using `sprintf('id IN (%s)', $config['roleselection'])` without sanitization or parameter binding, creating potential SQL injection risks if course/block configuration contained unexpected strings.
**Learning:** In Moodle, configuration settings stored in plugin config tables may be manipulated or imported unsafely. Direct string interpolation for SQL `IN (...)` clauses bypassing Moodle's database abstraction layer compromises query safety.
**Prevention:** Always parse list configurations with `explode()`, sanitize items with `array_filter(..., 'is_numeric')`, and use `$DB->get_in_or_equal()` to safely parameterize `IN` clauses.

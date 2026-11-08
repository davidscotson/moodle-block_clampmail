## 2026-11-08 - Parameterized SQL IN Clauses in Configuration Filtering
**Vulnerability:** SQL injection vulnerability in role filtering query due to unparameterized string formatting (`sprintf('id IN (%s)', $config['roleselection'])`).
**Learning:** Configuration values retrieved from the database or course settings can contain comma-separated identifiers that may be manipulated. Directly concatenating or interpolating them into SQL statements bypasses database abstraction parameterization.
**Prevention:** Always validate and filter comma-separated identifier lists using `is_numeric` and use Moodle's `$DB->get_in_or_equal()` helper to generate safe parameterized placeholders.

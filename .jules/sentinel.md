## 2026-07-08 - Parameterized SQL IN Clauses in Configuration Filtering
**Vulnerability:** SQL injection vulnerability in role filtering query due to unparameterized string formatting (`sprintf('id IN (%s)', $config['roleselection'])`).
**Learning:** Configuration values retrieved from the database or cache might contain comma-separated identifiers that can be modified or manipulated. Inserting them directly into SQL statements via string interpolation bypasses DB parameterization.
**Prevention:** Always validate and filter comma-separated identifier lists using `is_numeric` and use Moodle's `$DB->get_in_or_equal()` helper to generate safe parameterized placeholders.

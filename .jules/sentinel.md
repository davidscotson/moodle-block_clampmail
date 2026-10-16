## 2026-03-31 - Parameterization of IN(...) SQL Queries

**Vulnerability:**
Direct string concatenation or `sprintf` interpolation of comma-separated list values (e.g. `$config['roleselection']` or group ID arrays) into `$DB->get_records_select()` `IN (...)` conditions created potential SQL injection risks and runtime SQL syntax errors on empty lists.

**Learning:**
In Moodle, dynamic `IN (...)` conditions must not rely on unparameterized string formatting. Unsanitized or empty string inputs lead to invalid SQL or parameter tampering.

**Prevention:**
Filter array items with `array_filter(..., 'is_numeric')` and construct query parameters using `$DB->get_in_or_equal($ids)`. Check for non-empty ID arrays before calling `$DB->get_records_select()`.

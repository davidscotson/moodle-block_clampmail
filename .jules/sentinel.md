# Sentinel Security Journal

## 2026-03-31 - SQL Injection in Role Selection Filtering

**Vulnerability:**
In `email.php`, `$config['roleselection']` was formatted directly into a SQL query using `sprintf('id IN (%s)', $config['roleselection'])` and passed into `$DB->get_records_select()`. Because the values from configuration were directly interpolated into SQL without parameterization or strict type-casting, any corrupted or manipulated configuration value could lead to SQL injection.

**Learning:**
Database configuration values stored as comma-separated lists should never be interpolated directly into SQL statements using string formatting functions (`sprintf`, concatenation). Even when data originated from internal configuration tables, defense-in-depth requires strictly parameterizing queries or validating data types.

**Prevention:**
Always explode comma-separated identifiers, sanitize them with `array_filter($ids, 'is_numeric')`, and use Moodle's built-in `$DB->get_in_or_equal($roleids)` to generate safe parameterized placeholders and bind parameters.

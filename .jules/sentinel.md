## 2026-03-31 - CSRF Vulnerability on Configuration Reset

**Vulnerability:** Missing `require_sesskey()` protection on the block configuration reset action (`reset=1` param) in `config.php`, combined with a lack of the `sesskey` parameter on the reset link in `classes/config_form.php`.

**Learning:** State-changing parameters like `reset=1` that are handled outside of standard Moodle form processing are not automatically protected by Moodle's built-in form CSRF token validation and require manual `require_sesskey()` verification.

**Prevention:** Always include `'sesskey' => sesskey()` in any generated links or forms that trigger state-changing actions, and enforce `require_sesskey()` in the receiving scripts before executing the state change.

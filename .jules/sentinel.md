## 2026-03-31 - [Alternate Email CSRF and Course-Context IDOR Protection]

**Vulnerability:**
The alternate email management page (`alternate.php`) lacked CSRF protection on its state-changing actions (`confirmed` and `inform`). An attacker could construct an off-site link to trick authenticated users (such as teachers) into deleting alternate emails. Additionally, the lookup function `alternate::get_one($id)` fetched database records strictly by primary key `id`, which allowed cross-course IDOR (Insecure Direct Object Reference) data leakage and record deletion by users with capabilities in any course.

**Learning:**
In multi-tenant or multi-course applications like Moodle, objects should never be queried solely by a global unique identifier (e.g., `id`) if permission is scoped at a context level (e.g., course context). Even with strict capabilities checks (e.g., `require_capability`), failure to isolate lookups within the verified context allows cross-resource access. State-changing dynamic dispatches must always be protected via anti-CSRF tokens (`sesskey`) and restricted by a strict whitelist of known allowed actions.

**Prevention:**
1. Secure all lookup helper methods by accepting the contextual ID (such as `courseid`) along with the resource ID, and include this contextual ID in database query parameters.
2. Require Moodle's `sesskey` check on all state-changing endpoints, even when triggered by a confirmation dialog or form redirect.
3. Explicitly whitelist class constants when dispatching user actions dynamically using input parameters.

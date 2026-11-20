# Lab 11: Finding and patching vulnerabilities in DVWA

## Goal

For six challenges in Damn Vulnerable Web Application (SQL injection and command injection, each at the low, medium and high levels): find the vulnerable line in the PHP source, explain the flaw, run an attack that proves it, patch the source, and show the attack no longer works.

## Tools and concepts

- DVWA v1.10 on a local Apache/PHP/MySQL stack in the course VM, reached at `localhost`
- PHP source under `vulnerabilities/sqli/source/` and `vulnerabilities/exec/source/`, edited with VIM
- SQL injection: tautology (`OR 1=1`), `UNION SELECT`, comment truncation with `#`
- Command injection: shell separators `;`, `|`, `&&`
- Fixes: `mysqli_real_escape_string`, integer casting, allow-list validation with `filter_var(..., FILTER_VALIDATE_IP)`, and why blacklists fail
- Chromium developer tools to change a form field value

## What I did

| Challenge | Flaw | Attack input | My patch |
| --- | --- | --- | --- |
| SQL injection, low | `id` from the request is concatenated into a quoted string in the query with no escaping | `1' OR '1'='1` | Escape `id` with `mysqli_real_escape_string` before building the query |
| SQL injection, medium | `id` is escaped but placed in the query without quotes, so no quote is needed to inject | `1 OR 1=1`, sent by editing the dropdown value | Cast `id` to an integer |
| SQL injection, high | `id` comes from the session, set on a separate page, and goes into the query unescaped | `1' UNION SELECT user, password FROM users #` | Cast the session value to an integer |
| Command injection, low | The `ip` field is appended to a `ping` command passed to `shell_exec` | `127.0.0.1; whoami` | Reject anything that is not a valid IP address |
| Command injection, medium | A blacklist removes only `&&` and `;` | `127.0.0.1 \| whoami` | Replace the blacklist with the same IP validation |
| Command injection, high | The blacklist entry for the pipe is `'\| '` with a trailing space, so a bare `\|` gets through | `127.0.0.1\|whoami` | Correct the entry to `'\|'` |

The patches are in [`patches/`](patches/) as small diffs. Only the changed lines and a little context are shown. The rest of each file is DVWA's own code.

## Result

Before the patches:

- The two tautology attacks returned all five rows of the users table instead of one.
- The UNION attack returned the user names and password hashes of DVWA's built-in demo accounts.
- All three command injection attacks printed `www-data`, the output of `whoami`, on the page.

After the patches:

- SQL injection low: the same input returned only the row for ID 1.
- SQL injection medium and high: the injected input was reduced to `1` and returned one row.
- Command injection low and medium: the page showed "Invalid IP address".
- Command injection high: my screenshot shows the same input in the form and no command output on the page.

## Limits of these patches

These are the fixes I submitted, not the best possible ones.

- Prepared statements would be the stronger fix for all three SQL cases. Escaping works at the low level only because the value sits inside quotes.
- The high-level command injection patch fixes the typo but keeps the blacklist. The IP allow-list used for low and medium is the better approach and would work there too.
- The patches were transcribed from the editor screenshots in my report. I have not re-run them from these files.

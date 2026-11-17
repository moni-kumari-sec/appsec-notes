# SEC-00: Short title of the finding

| Field | Detail |
| --- | --- |
| Severity | Low / Medium / High (lab rating, explain below) |
| Component | Route, feature, or file |
| Environment | Local lab only, commit or lab name |
| Status | Open / Fixed / Retested |
| Retested | Date |

## Expected control

Who may access what, and how the system is supposed to enforce it.

## Observed behavior

What actually happens. Include a sanitized request and response, or the exact failing test.

## Root cause

The missing or wrong check, with the line or query responsible.

## Impact and assumptions

What synthetic data or action is exposed, and what must be true for it to work.

## Risk rationale

Reachability, data sensitivity, existing controls, and uncertainty.

## Remediation

The code change and why it fixes the whole class of issue, not just one request.

## Verification

| Test | Expected | Result |
| --- | --- | --- |
| Normal use | Works | |
| Attack request | Denied | |
| Variant: alternate method, route, role, or ID | Denied | |

## Lessons

What surprised me, or what looked fixed but was not.

## References

- OWASP Top 10: https://owasp.org/Top10/
- OWASP API Security Top 10: https://owasp.org/API-Security/
- PortSwigger Web Security Academy: https://portswigger.net/web-security

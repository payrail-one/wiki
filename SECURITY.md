# Security policy

## Supported scope

The repository is pre-release development software. No current component is
represented as a production custody or real-value payment service. Reports
about the public devnet, public replica node, signing/authorization, ledger
integrity, finality verification, persistence or wallet key handling are still
welcome.

## Reporting a vulnerability

Use GitHub private vulnerability reporting for the affected Payrail repository
when available. If that channel is unavailable, contact the security address
listed on the verified `payrail.one` domain. Do not include secrets or personal
data in an issue, discussion, log paste or screenshot.

Include:

- affected repository, commit and component;
- prerequisites and minimal reproduction;
- expected and observed behavior;
- impact on authorization, value, finality, confidentiality or availability;
- whether a shared development service was touched.

Do not test against accounts you do not control, degrade shared infrastructure,
exfiltrate data, persist access or publish details before coordinated review.

## Response expectations

The maintainers will acknowledge a valid private channel, reproduce and
classify the issue, agree on remediation/disclosure timing and credit the
reporter when requested and appropriate. Development-network status does not
reduce the priority of key disclosure, unauthorized value movement, forged
finality or persistent integrity failures.

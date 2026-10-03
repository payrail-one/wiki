# Contributing

Payrail is currently unreleased development software. Before contributing,
read the [developer documentation](docs/README.md), the relevant architecture
decision records and the repository-wide engineering rules.

## Workflow

1. Keep one change focused on one capability or invariant.
2. Reuse existing domain types, validation, codecs and ports.
3. Add tests for success and adversarial/failure behavior.
4. Update documentation and ADRs in the same change.
5. Run the complete gates in [Testing](docs/TESTING.md).

Do not commit secrets, private infrastructure data, generated build output,
local state or real customer/payment information. Use placeholders in examples.

## Pull requests

Describe the invariant or user-visible contract changed, the trust boundary,
retry/restart behavior and verification performed. Call out persistent format,
API, cryptographic, monetary, licensing or deployment consequences explicitly.

Security issues must follow [SECURITY.md](SECURITY.md), not a public issue.

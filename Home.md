# Developer documentation

This is the documentation hub for the Payrail development platform. The code is
an unreleased development system: package version `0.0.0`, test-only assets and
explicitly non-production finality. Public repository visibility does not turn
the current implementation into a production payment network.

## Start here

- [Getting started](GETTING_STARTED.md) — prerequisites and the shortest path to
  a running local devnet.
- [Architecture](ARCHITECTURE.md) — trust boundaries, data flow and component
  layers.
- [Repository map](REPOSITORY_MAP.md) — ownership of Rust crates, tools, web
  applications and shared packages.
- [HTTP API](HTTP_API.md) — current devnet and public replica-node contracts.
- [Development workflow](DEVELOPMENT.md) — how to make and review changes.
- [Testing](TESTING.md) — local gates, Linux-only release evidence and E2E
  expectations.
- [Security model](SECURITY_MODEL.md) — assets, threats, trust boundaries and
  disclosure guidance.
- [Operations](OPERATIONS.md) — local containers, persistence, health checks and
  safe exposure.
- [Web applications](WEB_APPLICATIONS.md) — Workstar/TypeScript package and
  application boundaries.
- [ADR index](ADR_INDEX.md) — architectural decisions grouped by capability.
- [Glossary](GLOSSARY.md) — project terminology.

## Existing deep dives

- [Account address format](ADDRESS_FORMAT.md)
- [Consensus lab](CONSENSUS_LAB.md)
- [Validator process harness](VALIDATOR_PROCESS_HARNESS.md)
- [Persistent payment lab](PERSISTENT_PAYMENT_LAB.md)
- [Merchant checkout contract](MERCHANT_CHECKOUT_API.md)
- [Web SDK](PAYRAIL_WEB_SDK.md)
- [Public node](PUBLIC_NODE.md)
- [Local execution benchmark](LOCAL_EXECUTION_BENCHMARK.md)
- [Local pipeline benchmark](LOCAL_PIPELINE_BENCHMARK.md)
- [Local Malachite benchmark](LOCAL_MALACHITE_BENCHMARK.md)

## Documentation rules

Documentation must describe implemented behavior separately from proposals and
production requirements. Commands are written from the `platform/` repository
root unless a section says otherwise. Monetary JSON examples use decimal
strings. Examples must never contain real keys, credentials, operator addresses
or production infrastructure details.

Run `python3 scripts/check_docs.py` before submitting documentation changes. It
checks local Markdown links, duplicate headings and the continuity of ADR file
numbers.

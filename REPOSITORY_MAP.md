# Repository map

## Top level

| Path | Responsibility |
| --- | --- |
| `crates/` | Reusable Rust domain, application and infrastructure crates |
| `tools/` | Runnable gateways, proof tools, benchmarks and test harnesses |
| `web/apps/` | Workstar/TypeScript product surfaces |
| `web/packages/` | Typed API, money, wallet and UI building blocks |
| `docs/` | Developer guides, operational notes and ADRs |
| `deploy/` | Sanitized reverse-proxy and service examples |
| `scripts/` | Quality, documentation and publication checks |

Generated output belongs in ignored `target/`, `dist/`, `.devnet/` or artifact
directories. It must not be committed as source.

## Rust capability groups

| Capability | Authoritative crates |
| --- | --- |
| Accounts and authorization | `account-address`, `transaction-protocol`, `transaction-auth-ed25519`, `transaction-verification-core` |
| Ledger and execution | `ledger-core`, `ledger-runtime-core`, `authenticated-state-core`, `block-production-core` |
| Consensus and finality | `consensus-engine-core`, `ledger-consensus-application`, `finality-proof-core`, `finality-auth-ed25519`, `malachite-consensus-adapter` |
| Consensus signing | `consensus-signer-core`, `consensus-signer-journal-fs`, `grandpa-finality-boundary`, `grandpa-authority-store-fs` |
| Network and peers | `network-membership-core`, `network-config-core`, `network-config-auth-ed25519`, `peer-*`, `transaction-gossip-core` |
| Recovery and availability | `state-sync-core`, `tail-sync-core`, `snapshot-store-fs`, `block-availability-core` |
| Durable finalized state | `tail-state-store-lmdb`, `receipt-index-core`, `receipt-index-lmdb`, `receipt-rebuild-core` |
| Payment orchestration | `payment-gateway-core`, `payment-gateway-adapters`, `payment-ingress-core`, `payment-idempotency-*` |
| Limits and reconciliation | `payment-rate-limit-lmdb`, `payment-reconciliation-*` |
| Merchant checkout | `merchant-checkout-core`, `merchant-checkout-lmdb`, `checkout-approval-*` |
| External settlement | `external-asset-core`, `c1-finality-adapter` |

The `*-core` convention normally marks a framework-independent boundary. A
storage or cryptography suffix identifies an adapter. Check each crate's
`lib.rs` exports and tests before adding a new type: an existing canonical type
or codec is usually the correct dependency.

## Executables

| Tool | Purpose |
| --- | --- |
| `devnet-gateway` | Persistent single-node signed-payment devnet and HTTP API |
| `consensus-lab` | Deterministic seven-validator finality scenarios |
| `validator-process-harness` | Multi-process validator, recovery and network-fault evidence |
| `payment-benchmark` | Deterministic ledger execution measurements |
| `payment-pipeline-benchmark` | Ingress-to-finalized pipeline measurements |
| `c1-proof-check` | Independent C1 finality/execution proof verification |
| `c1-transfer-build` | Offline C1 Standard-lane signed transfer construction |
| `c1-faucet-service` | Loopback-only testnet funding through the signed C1 path |

The separately published `payrail-node` is a non-validating replica of the
public development history. It exposes reads, readiness and signed-envelope
relay, but not faucet or checkout administration.

## Web packages

| Package | Responsibility |
| --- | --- |
| `@platform/api-client` | Typed development API and canonical hex helpers |
| `@platform/money` | Decimal string ↔ checked atomic `bigint` conversion |
| `@platform/wallet-core` | Browser key lifecycle, addresses, signing and encrypted vaults |
| `@platform/ui-kit` | Shared Workstar components, logo access and design tokens |

See [Web applications](WEB_APPLICATIONS.md) for app ownership and security
boundaries.

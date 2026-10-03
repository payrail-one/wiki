# Architecture decision record index

ADRs record accepted decisions and explicit production gates. Later ADRs may
refine earlier ones; implementation and tests remain the source of truth for
current behavior.

## Foundation and monetary model

- [ADR-0001 — Consortium validation with broadly accessible payments](ADR-0001-network-access.md)
- [ADR-0002 — Public development node source and controlled production IP](ADR-0002-source-and-ip.md)
- [ADR-0003 — Ledger recovery, receipts and fee sponsorship](ADR-0003-ledger-recovery-and-fee-sponsorship.md)
- [ADR-0004 — Canonical transaction authorization](ADR-0004-transaction-authorization.md)
- [ADR-0005 — Operation identity and bounded binary envelope](ADR-0005-operation-identity-and-envelope.md)
- [ADR-0006 — Network-scoped account addresses](ADR-0006-account-addresses.md)
- [ADR-0007 — External-asset settlement state machine](ADR-0007-external-asset-settlement.md)

## Membership, finality and synchronization

- [ADR-0008 — Permissioned consensus membership and safe state sync](ADR-0008-consensus-membership-and-safe-sync.md)
- [ADR-0009 — Verified parallel state sync](ADR-0009-verified-parallel-state-sync.md)
- [ADR-0010 — Bounded transaction gossip and durable snapshot chunks](ADR-0010-bounded-transaction-gossip-and-snapshot-storage.md)
- [ADR-0011 — Mutually authenticated and channel-bound peer sessions](ADR-0011-mutual-tls-peer-sessions.md)
- [ADR-0012 — Finality-proof verification boundary](ADR-0012-finality-proof-boundary.md)
- [ADR-0013 — GRANDPA SDK and consensus-signing boundaries](ADR-0013-grandpa-sdk-and-consensus-signing-boundaries.md)
- [ADR-0014 — Durable consensus signing and authority history](ADR-0014-durable-consensus-history.md)
- [ADR-0015 — Deterministic seven-validator consensus lab](ADR-0015-deterministic-consensus-lab.md)
- [ADR-0016 — Local multi-process validator harness](ADR-0016-local-validator-process-harness.md)
- [ADR-0017 — Authenticated multi-process state-sync recovery](ADR-0017-multiprocess-state-sync-recovery.md)
- [ADR-0018 — Verified tail catch-up after snapshot recovery](ADR-0018-verified-tail-catch-up.md)

## Runtime, state and block production

- [ADR-0019 — LMDB adapter for finalized node state](ADR-0019-lmdb-finalized-state-store.md)
- [ADR-0020 — Canonical signed-operation block execution](ADR-0020-canonical-ledger-block-execution.md)
- [ADR-0021 — Deterministic bounded block production](ADR-0021-deterministic-block-production.md)
- [ADR-0022 — Bounded parallel transaction authorization](ADR-0022-bounded-parallel-authorization.md)
- [ADR-0023 — Atomic bounded local batch ingress](ADR-0023-atomic-batch-ingress.md)
- [ADR-0024 — Versioned authenticated normalized ledger state](ADR-0024-versioned-authenticated-ledger-state.md)
- [ADR-0025 — Atomic LMDB persistence for authenticated ledger state](ADR-0025-atomic-lmdb-authenticated-state.md)
- [ADR-0026 — Height-gated authenticated checkpoint root](ADR-0026-height-gated-authenticated-checkpoint-root.md)
- [ADR-0027 — Signed bootstrap network configuration](ADR-0027-signed-bootstrap-network-configuration.md)
- [ADR-0028 — Two-phase incremental authenticated execution](ADR-0028-two-phase-incremental-authenticated-execution.md)
- [ADR-0029 — Bounded live ledger state and receipt indexing](ADR-0029-bounded-live-state-and-receipt-indexing.md)
- [ADR-0030 — Independent finalized receipt index and deterministic rebuild](ADR-0030-derived-finalized-receipt-index.md)

## Gateway, checkout and operational controls

- [ADR-0031 — Journal-first payment idempotency and finality reconciliation](ADR-0031-journal-first-payment-idempotency.md)
- [ADR-0032 — Payment gateway adapters and recoverable finalized path](ADR-0032-payment-gateway-adapters-and-recovery-path.md)
- [ADR-0033 — Bounded payment finality reconciliation](ADR-0033-bounded-payment-finality-reconciliation.md)
- [ADR-0034 — Fenced reconciliation worker and durable retry schedule](ADR-0034-fenced-reconciliation-worker.md)
- [ADR-0035 — Durable single-use merchant checkout](ADR-0035-durable-merchant-checkout.md)
- [ADR-0036 — Height-bound operation expiry without nonce gaps](ADR-0036-consensus-operation-expiry.md)
- [ADR-0037 — Finalized-height transaction admission and expired cleanup quota](ADR-0037-finalized-height-transaction-admission.md)
- [ADR-0038 — Peer-owned pending requests and sender-isolated mempool quotas](ADR-0038-peer-and-sender-mempool-quotas.md)
- [ADR-0039 — Bounded payment API rate limits](ADR-0039-bounded-payment-api-rate-limits.md)
- [ADR-0040 — Local traffic classes and fair candidate selection](ADR-0040-local-traffic-class-fair-candidate-selection.md)
- [ADR-0041 — Class-protected bounded mempool eviction](ADR-0041-class-protected-mempool-eviction.md)
- [ADR-0042 — Durable shared payment rate limits](ADR-0042-durable-shared-payment-rate-limits.md)
- [ADR-0043 — Low-cardinality mempool observability](ADR-0043-low-cardinality-mempool-observability.md)
- [ADR-0044 — Multi-process signed-payment finality laboratory](ADR-0044-multi-process-payment-finality-lab.md)
- [ADR-0045 — Restart-persistent multi-block payment finality laboratory](ADR-0045-restart-persistent-multi-block-finality.md)
- [ADR-0046 — Derived receipt-index outage and recovery laboratory](ADR-0046-derived-receipt-index-recovery-lab.md)
- [ADR-0047 — Supervised receipt worker process](ADR-0047-supervised-receipt-worker-process.md)

## Network hardening and product surfaces

- [ADR-0048 — First-quorum payment path and deterministic network fault profile](ADR-0048-first-quorum-network-fault-profile.md)
- [ADR-0049 — Bounded persistent validator-process payment laboratory](ADR-0049-bounded-persistent-validator-process-lab.md)
- [ADR-0050 — Bounded persistent validator connections](ADR-0050-bounded-persistent-validator-connections.md)
- [ADR-0051 — Peer health backoff and security quarantine](ADR-0051-peer-health-backoff-and-security-quarantine.md)
- [ADR-0052 — BFT foundation selection](ADR-0052-bft-foundation-selection.md)
- [ADR-0053 — Workstar explorer, web wallet and real-transaction E2E](ADR-0053-workstar-explorer-wallet-e2e.md)
- [ADR-0054 — Omnichannel checkout through QR, embed and SMS](ADR-0054-omnichannel-checkout-qr-embed-sms.md)
- [ADR-0055 — Bank-app approval-code core](ADR-0055-bank-app-approval-code-core.md)
- [ADR-0056 — Finality-gated ledger consensus application](ADR-0056-ledger-consensus-application.md)
- [ADR-0057 — Adaptive payment block cadence](ADR-0057-adaptive-payment-block-cadence.md)
- [ADR-0058 — Compact block data availability](ADR-0058-compact-block-data-availability.md)
- [ADR-0059 — Preverified authorization and compact envelope reconciliation](ADR-0059-preverified-authorization-and-envelope-reconciliation.md)
- [ADR-0060 — Lottery rolling test jackpot](ADR-0060-lottery-rolling-test-jackpot.md)
- [ADR-0061 — C1 finality and randomness boundary](ADR-0061-c1-finality-and-randomness-boundary.md)
- [ADR-0062 — Wallet live events and device sessions](ADR-0062-wallet-live-events-and-device-sessions.md)

## Adding an ADR

Use the next free four-digit number. Include status, context, decision, security
or compatibility consequences, verification evidence and rejected shortcuts.
Do not reuse a number or silently rewrite a decision after dependent code has
shipped; add a superseding ADR and link both records.

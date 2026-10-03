# Glossary

| Term | Meaning |
| --- | --- |
| Atomic unit | Smallest integer unit of an asset. Rust uses `u128`; browser code uses `bigint`. |
| Authorization payload | Canonical domain-separated bytes signed by an account or sponsor. |
| Checkout | Immutable, fixed-amount, single-use merchant payment request. |
| Checkpoint | Finalized height, block hash and authenticated state root. |
| C1/R1 | External consensus/settlement system integrated through a separate proof boundary; not a Payrail node upstream. |
| Devnet | Test-only environment with no real-value assets or production guarantees. |
| Envelope | Bounded canonical binary form of a signed operation. |
| Finality | Verified evidence that a transition is committed under the declared network finality model. |
| Idempotency key | Client/gateway correlation and recovery key; not the consensus replay key. |
| Nonce | Exact per-sender sequence number and consensus replay boundary. |
| Operation ID | Deterministic content-derived identity of an authorized operation. |
| Receipt | Deterministic finalized execution outcome linked to block height and operation index. |
| Receipt index | Independent derived lookup store rebuilt from verified finalized payloads. |
| Replica node | Non-validating process that independently re-executes and stores public devnet history. |
| State root | Authenticated commitment to normalized ledger state at a height. |
| Tail sync | Sequential verified application of blocks after a checkpoint/snapshot. |
| Traffic class | Local admission/proposal policy category; not consensus-visible transaction priority. |
| Trust anchor | Independently pinned network/genesis/validator commitment used to verify proofs. |
| Valid-until height | Signature-bound last consensus height at which an operation may apply value movement. |

# Testing and release evidence

## Local quality gate

From `platform/`:

```sh
bash scripts/check-source-size.sh
python3 scripts/check_docs.py
cargo fmt --all --check
cargo clippy --locked --all-targets -- -D warnings
cargo test --locked --all-targets
```

The isolated equivalent is:

```sh
docker compose run --rm quality
```

The quality container runs without network access, as a non-root user, with a
read-only root filesystem, no Linux capabilities and ephemeral build output.

## Web gate

From `platform/web/`:

```sh
npm ci
npm run format:check
npm run check
npm run build
```

Run the relevant Playwright project after starting its real dependency stack:

```sh
npm run test:e2e
npm run test:payrail-public
npm run test:lottery
npm run test:site
```

Payment acceptance E2E must use signed operations against an isolated real
devnet, wait for independently indexed finality and verify both wallet and
explorer views. Mock HTTP is suitable for component tests, not this gate.

## What monetary/security tests must cover

- successful state transition;
- authorization and signer-role mismatch;
- nonce replay and conflicting idempotent retry;
- zero, maximum and overflow boundaries;
- wrong network, epoch, asset, height or configuration;
- malformed/truncated/trailing canonical encodings;
- failure atomicity before and during persistence;
- restart validation and recovery;
- concurrency where more than one process can claim or commit;
- corrupted, forged, duplicate, reordered or incomplete proof material.

Tests should call production validation paths. A test fixture may construct
data, but it must not duplicate the invariant it claims to verify.

## Platform-specific evidence

The deterministic consensus lab proves protocol properties in-process. The
validator process harness adds real process, TLS, restart and network-fault
boundaries. Neither alone is a production deployment certification.

Benchmarks record a named build, topology, workload, warm-up, concurrency,
hardware and result artifact. A number without that context is not comparable.

## R1/C1 release rule

Build, verify and deploy C1/R1 runtime candidates on the designated Linux GPU
servers. Local macOS is appropriate for editing and light static checks only;
local CUDA or Linux-toolchain failure is not a release verdict.

During active R1 stabilization, build and deploy debug candidates by default.
Do not produce or deploy a release binary without an explicit request. Keep one
managed testnet instance: build in isolation and update the existing systemd
deployment rather than starting a second consensus network.

## Before public publication

- scan the complete selected Git history for secrets and private infrastructure;
- confirm ignored state/build/artifact directories are absent;
- run the full Rust and documentation gates on the publication snapshot;
- review dependency licenses and committed lockfiles/SBOM evidence;
- ensure every public surface states its finality and test-asset limitations.

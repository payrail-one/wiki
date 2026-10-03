# Development workflow

## Before changing code

1. Read the applicable ADRs and identify the authoritative invariant.
2. Search for an existing type, codec, port or adapter before adding one.
3. Decide whether the change belongs in domain, application, infrastructure or
   presentation code.
4. Record compatibility, security or monetary decisions in an ADR before the
   implementation makes them implicit.

New production work belongs under `platform/`. Legacy Node.js code outside this
directory is migration evidence unless a task explicitly targets it.

## Rust conventions

- Keep domain crates independent of frameworks, storage and vendor SDKs.
- Use explicit domain identifiers, states and errors.
- Use checked integer arithmetic for all value movement.
- Validate a complete transition before committing any mutation.
- Production code must not use `unsafe`, `unwrap`, `expect` or deliberate panic
  paths.
- Put I/O behind small interfaces and keep one implementation of each invariant.
- Keep hand-written files below 700 lines and preferably below 400.

Run focused tests while iterating, for example:

```sh
cargo test --locked -p ledger-core
cargo clippy --locked -p ledger-core --all-targets -- -D warnings
```

Then run the complete gate described in [Testing](TESTING.md).

## TypeScript conventions

- Use Workstar for browser applications and exact pinned dependencies.
- Keep API access, money parsing, signing and UI components in separate
  packages.
- Represent money as decimal strings at JSON boundaries and `bigint` internally.
- Never put wallet secrets in SSR, server actions, logs, analytics, traces or
  screenshots.
- Use `npm ci`; do not regenerate the lockfile unless dependency changes are the
  explicit purpose of the change.

From `web/`:

```sh
npm run check
npm run format:check
npm run build
```

## Adding a Rust crate

Add a crate only for a real capability boundary or test seam. The crate should:

- inherit workspace edition, version, license and lints;
- expose the smallest useful public API;
- keep infrastructure dependencies out of domain crates;
- include success, authorization, replay, boundary, overflow and failure
  atomicity tests when monetary or security behavior is involved;
- be added to `Cargo.toml` and documented in
  [Repository map](REPOSITORY_MAP.md).

## Changing a protocol or persistent format

Treat canonical encodings, signature payloads, state rows, snapshots, block
payloads and public JSON as compatibility surfaces. A change requires:

- an explicit version or a proof that the encoding is unchanged;
- golden vectors or round-trip and rejection tests;
- bounds checked before allocation;
- restart/recovery tests for durable state;
- an ADR update describing migration and downgrade behavior.

## Documentation

Update the relevant guide in the same change as behavior. Mark proposals as
proposals and do not describe a test harness as deployed production behavior.
Run:

```sh
python3 scripts/check_docs.py
```

## Commit and review

Keep commits capability-focused. A review should be able to answer:

- Which invariant changed, and where is its single implementation?
- What is authoritative and what is derived?
- What happens on retry, restart, timeout, overflow and partial I/O failure?
- Which identity/network/height/domain fields are cryptographically bound?
- Which tests demonstrate rollback and fail-closed behavior?
- Does the change expose new data, credentials or operational topology?

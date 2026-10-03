# Getting started

## What you will run

The default local stack is a single-node development ledger plus the combined
wallet/merchant/explorer portal. It verifies real browser Ed25519 signatures,
executes the production domain/runtime paths and persists state in LMDB. It is
not a validator network and does not provide BFT finality.

## Prerequisites

- Git;
- Rust `1.88` with `rustfmt` and `clippy`;
- Node.js `22.22.0` and npm for web work;
- Docker with Compose v2 for the reproducible full stack;
- Python 3 for repository documentation and utility checks.

All committed Rust and npm lockfiles are authoritative. Do not update
dependencies as a side effect of an unrelated change.

## Run the local devnet

From the `platform/` directory:

```sh
docker compose --profile devnet up --build gateway portal
```

Open `http://127.0.0.1:4173`. The gateway is also available on loopback at
`http://127.0.0.1:18080`.

Confirm the network identity and finalized tip:

```sh
curl --fail --silent http://127.0.0.1:18080/api/status
```

Stop the services without deleting state:

```sh
docker compose --profile devnet down
```

The `devnet-state` volume survives this command. Adding `--volumes` deletes the
local ledger and is intentionally not part of the normal workflow.

## Run natively

Start the Rust gateway:

```sh
cargo run --locked -p devnet-gateway
```

In a second terminal:

```sh
cd web
npm ci
npm run dev
```

The gateway defaults to `127.0.0.1:18080` and `.devnet/gateway`. Override them
with `DEVNET_BIND` and `DEVNET_DATA_DIR`. Vite proxies same-origin `/api`
requests to the local gateway.

## First verification

```sh
bash scripts/check-source-size.sh
python3 scripts/check_docs.py
cargo fmt --all --check
cargo clippy --locked --all-targets -- -D warnings
cargo test --locked --all-targets

cd web
npm ci
npm run format:check
npm run check
npm run build
```

See [Testing](TESTING.md) before treating local results as release evidence.

## Next reading

Read [Architecture](ARCHITECTURE.md), then use the
[Repository map](REPOSITORY_MAP.md) to locate the authoritative implementation
for the capability you are changing. API consumers can go directly to the
[HTTP API](HTTP_API.md) and [Web applications](WEB_APPLICATIONS.md).

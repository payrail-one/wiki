# Operations

## Development topology

The Compose `devnet` profile runs:

- `gateway` — Rust `devnet-gateway`, port `127.0.0.1:18080`, durable
  `devnet-state` volume;
- `portal` — built Workstar/TypeScript portal, port `127.0.0.1:4173`, proxying
  `/api` to the gateway.

Both containers run without Linux capabilities, with `no-new-privileges` and a
read-only root filesystem. The gateway writes only to its mounted state volume.

## Runtime configuration

| Variable | Default | Meaning |
| --- | --- | --- |
| `DEVNET_BIND` | `127.0.0.1:18080` | Native gateway listen address |
| `DEVNET_DATA_DIR` | `.devnet/gateway` | Native LMDB/state root |
| `DEVNET_API_PROXY` | `http://gateway:8080` | Container portal upstream |
| `VITE_API_BASE_URL` | same-origin `/api` | Isolated browser API override |

The public replica additionally uses `PAYRAIL_NODE_BIND`,
`PAYRAIL_NODE_DATA_DIR`, `PAYRAIL_NODE_UPSTREAMS` and
`PAYRAIL_NODE_SYNC_INTERVAL_SECONDS`. Upstream URLs must be credential-free
HTTP(S) origins; one to eight may be configured.

## Safe lifecycle

Start or rebuild:

```sh
docker compose --profile devnet up --build --detach gateway portal
docker compose logs --follow gateway portal
```

Check the authoritative API:

```sh
curl --fail http://127.0.0.1:18080/api/status
```

Stop while preserving state:

```sh
docker compose --profile devnet down
```

Deleting `.devnet/` or the Compose volume destroys local development history.
Never perform that operation as an attempted repair without first preserving
and diagnosing the state.

## Internet exposure

Do not expose the container listener directly. Terminate TLS at a reviewed
reverse proxy and enforce exact paths, request-body limits, rate limits,
timeouts and safe logging. Logs must exclude private keys, bearer credentials,
signed envelope bodies and sensitive merchant/customer data.

The development gateway contains faucet and checkout-creation routes. The
public replica intentionally omits them. Neither is a production custody,
issuer or validator service.

## Persistence and recovery

On startup, the gateway validates the configured network, durable ledger
cursor, authenticated state and retained payload continuity. The receipt index
may be rebuilt from verified finalized payloads. Never treat a missing derived
index as permission to alter authoritative balances or nonces.

After a controlled restart verify:

1. network ID and finality mode are unchanged;
2. finalized height and tip hash did not regress;
3. a known account balance/nonce is unchanged;
4. explorer/index coverage catches up to the ledger cursor;
5. a newly signed test payment reaches an independently indexed final receipt.

## Health semantics

For a public replica, `/health/live` means the process can answer. Readiness
means the replica is synchronized with its current upstream target. Liveness is
not proof of ledger correctness, and readiness is not production finality.

## Managed R1 testnet

C1/R1 consensus deployments follow a separate operational boundary: use the
designated Linux GPU hosts, build candidates in an isolated directory, deploy
debug builds by default and update exactly one managed systemd instance. Never
start a parallel consensus network beside the managed testnet.

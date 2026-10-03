# ADR-0062: Wallet live events, device sessions and portable recovery

## Status

Accepted and implemented for the public devnet wallet. Production enablement
remains gated by multi-validator deployment, an external security review and
browser compatibility testing for non-extractable key persistence.

## Context

The wallet needs immediate finality and checkout updates, must remain usable
across an ordinary page reload, and must offer an explicit way to move a
self-custody account to a new device. Requiring the wallet password after every
reload is poor session behaviour, while persisting extractable key bytes would
weaken the signing boundary. A custodial password reset would contradict the
current self-custody model.

## Decision

1. Expose a public, read-only, account-filtered WebSocket at `/api/live` using
   the `payrail.live.v1` subprotocol. It publishes finalized transactions and
   checkout changes but never carries private material or authorizes payments.
2. The gateway uses a bounded broadcast channel, filters events for the
   subscribed account, sends heartbeats, times out dead peers and asks lagging
   clients to resynchronize from authoritative HTTP state.
3. The browser reconnects with bounded exponential backoff and always refreshes
   authoritative account and checkout data after an event. A socket message is
   a refresh signal, not the source of monetary truth.
4. After password unlock, persist a time-limited session in IndexedDB containing
   the public identity and a non-extractable Ed25519 private `CryptoKey`. On
   reload, validate expiry, key properties and public-key ownership with a
   random sign/verify challenge before restoring the session.
5. Explicit lock deletes the persisted session before showing the wallet as
   locked. If deletion fails, keep the wallet unlocked and report the failure
   rather than presenting a false security state.
6. Moving to a new device uses the existing AES-256-GCM encrypted JSON vault.
   The user downloads it, transfers it through a trusted channel, imports it on
   the new device and enters the same wallet password. The service cannot reset
   that password or recover an account without the vault or an unlocked device.
7. Notification and auto-lock preferences may use local storage because they
   contain no secrets. Browser notifications are opt-in and are driven only by
   finalized live events selected by the user.

## Security properties

- Raw private-key bytes are never written as a session, logged, sent to SSR or
  transmitted over the live channel.
- Reload restoration fails closed for expired, extractable, wrong-algorithm or
  public-key-mismatched sessions.
- Amounts remain canonical decimal strings at the API boundary and `bigint`
  atomic units in wallet logic.
- A dropped or lagged WebSocket cannot create false finality; the client
  resynchronizes through the existing authoritative APIs.
- The encrypted backup remains sensitive: possession plus its password grants
  control of the wallet. The UI must explain that there is no custodial reset.

## Verification

The Playwright public-payment scenario uses isolated browser contexts to prove
that a session survives reload, explicit lock survives a subsequent reload, an
encrypted backup restores the same address on a clean device, and a finalized
transfer updates the recipient through the live stream without manual refresh.
Gateway tests continue to cover signature rejection, finality, restart recovery
and checkout single-use behaviour. Rust formatting, tests and Clippy with
warnings denied remain release gates.

## Consequences

The demo behaves like a modern fintech application without moving signing or
balance authority into the UI. Recovery is intentionally manual and
self-custodial. Cloud synchronization, passkeys, social recovery, hardware
wallets and multi-device revocation require separate threat models and are not
implied by this decision.

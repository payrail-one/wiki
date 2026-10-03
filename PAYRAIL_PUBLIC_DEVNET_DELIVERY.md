# Payrail public devnet delivery

- [x] Deploy the persistent Payrail testnet gateway on the designated Linux host.
- [x] Finish `apps/wallet` with encrypted local authorization and Payrail signing.
- [x] Deploy `wallet.payrail.one` against only the Payrail testnet API.
- [x] Build and deploy the independent explorer at `explorer.payrail.one`.
- [x] Build and deploy the live dashboard at `devnet.payrail.one`.
- [x] Use the canonical Payrail logo and design tokens on every Payrail surface.
- [x] Run a real signed wallet-to-wallet transfer and verify indexed finality.
- [x] Verify persistence and recovery after a controlled gateway restart.
- [x] Create private repositories in `payrail-one` for each independent product.
- [x] Push code, lockfiles, documentation and the canonical logo to those repositories.
- [x] Publish a sanitized, independently runnable development-node repository at
  `payrail-one/node` for exchange and infrastructure integrations, without
  private repository history or deployment data.
- [x] Commit CycloneDX SBOM evidence for every TypeScript/Workstar product.

## Verification record

- Deployment: `payrail-testnet-gateway.service` on a managed Linux host, with
  persistent LMDB storage and a single managed container.
- Public product release: `20261003-r16` served through the Payrail custom domains;
  the main site brand/favicons were rebuilt on Linux and deployed as Worker
  version `70a17900-f134-4fc2-887b-d2d1b92b4c73`.
- Finality mode: `single-node-devnet`; this deployment is isolated from R1 and
  does not claim multi-validator BFT finality.
- Public E2E: two independently encrypted browser wallets, local Ed25519
  signing, a finalized wallet-to-wallet transfer, explorer lookup, QR/SMS
  checkout payment and encrypted-backup recovery.
- Recovery: the gateway was restarted after height 20; height, tip hash, 21
  retained blocks and 20 transactions were unchanged, and the full public E2E
  passed again after restart.
- Publication: `network`, `site`, `wallet`, `explorer`, `devnet`,
  `merchant-portal`, `ui-kit`, `sdk`, `lottery` and `.github-private` are private
  under `payrail-one`, all with `main` as the default branch. `.github` is public
  for the investor-facing organization profile; the sanitized `node` repository
  is public for exchange and infrastructure integrations.
- Public node: `payrail-one/node` contains the 25-package `devnet-gateway`
  dependency closure, a pinned Rust toolchain and lockfile, hardened local
  Compose defaults, operator/security documentation and a passing Linux CI gate.
- Supply chain: every TypeScript/Workstar repository includes a committed
  CycloneDX dependency inventory generated from its pinned lockfile.

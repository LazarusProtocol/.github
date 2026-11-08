# Security Policy

## Supported Versions

| Component | Version | Supported |
| :--- | :--- | :--- |
| `LazarusProtocol/contracts` | `0.1.x` (Stellar Testnet) | :white_check_mark: |
| `LazarusProtocol/attestation` | `0.1.x` | :white_check_mark: |
| `LazarusProtocol/indexer` | `0.1.x` | :white_check_mark: |
| `LazarusProtocol/keeper` | `0.1.x` | :white_check_mark: |
| `LazarusProtocol/web` | `0.1.x` | :white_check_mark: |

## Reporting a Vulnerability

We take the security of the Lazarus Protocol (smart contracts, 2-of-3 FROST MPC attestation enclave, indexer, and keeper infrastructure) seriously.

**Please do not report security vulnerabilities through public GitHub issues, discussions, or pull requests.**

### Preferred Channel: GitHub Private Vulnerability Reporting

Every repository in the **LazarusProtocol** organization has **GitHub Private Vulnerability Reporting** enabled:

1. Navigate to the relevant repository (e.g., [`LazarusProtocol/contracts`](https://github.com/LazarusProtocol/contracts/security/advisories/new)).
2. Click the **Security** tab -> **Report a vulnerability**.
3. Submit your report with reproduction steps, affected files/lines, and impact analysis.

### Scope & Architecture Notes

* **Atomic Vault Initialization (CAP-0058):** `LazarusVault` uses Soroban's `__constructor` (`CreateContractWithCtorHostFunction`) alongside `admin.require_auth()` in `initialize` so contract creation and initialization occur atomically in a single transaction.
* **Decoupled Voucher Verification:** In Soroban (CAP-0053 / CAP-0066), `ExtendFootprintTTLOp` is a host-level operation and `soroban-env-host` does not expose cross-contract storage TTL introspection on-chain. `LazarusVault::process_voucher` therefore verifies domain-separated `LAZARUS_VOUCHER_V1` XDR payloads signed by the 2-of-3 FROST Attestation Oracle (`ed25519_verify`), which inspects closed ledger metadata (`LedgerCloseMeta`) off-chain before issuing a signature.

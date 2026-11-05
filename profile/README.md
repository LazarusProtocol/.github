<div align="center">
  
<img src="https://raw.githubusercontent.com/LazarusProtocol/.github/main/profile/logo.png" width="110" alt="Lazarus Protocol logo"> 

# Lazarus Protocol
### Keep Stellar state alive.
A decentralized state-warming keeper network for Soroban.
<br>

[![Stellar](https://img.shields.io/badge/STELLAR-SOROBAN-FDDA24?style=for-the-badge&logo=stellar&logoColor=white)](https://stellar.org/soroban)
[![Live](https://img.shields.io/badge/TESTNET-LIVE-22C55E?style=for-the-badge)](https://lazarusprotocol.online/)
[![License](https://img.shields.io/badge/LICENSE-APACHE_2.0-F97316?style=for-the-badge)](https://opensource.org/licenses/Apache-2.0)

</div>

<br>

**Soroban state expires.** When a storage entry's TTL hits zero, the next user to touch it pays up to **10x** in restoration fees. Lazarus keeps state warm *before* anyone has to pay for it, with **no custody of dApp keys** and **no cron servers to babysit**.

<br>

## ⚙️ How it works

Stellar Core allows only **one operation per transaction**, so a keeper can't extend a TTL and claim a reward in the same envelope. Lazarus splits the job in three:

1. **Extend:** a keeper submits a standalone `ExtendFootprintTTLOp` for keys near expiry.
2. **Attest:** the attestation oracle verifies the closed ledger and issues a signed `BumpVoucher`.
3. **Settle:** keepers redeem up to 10 vouchers at once from the dApp's non-custodial escrow.

<br>

## 🧩 Architecture

| | Component | What it does |
| :-: | :-- | :-- |
| 📜 | [**`contracts`**](https://github.com/LazarusProtocol/contracts) | Soroban escrow vault, circuit breakers, batched voucher settlement |
| 🔍 | [**`indexer`**](https://github.com/LazarusProtocol/indexer) | Django indexer with Hubble BigQuery snapshots and RPC ledger catch-up |
| 🤖 | [**`keeper`**](https://github.com/LazarusProtocol/keeper) | Autonomous keeper daemon, deterministic cohort sharding, and footprint batching |
| 🔐 | [**`attestation`**](https://github.com/LazarusProtocol/attestation) | AWS Nitro Enclave signer & 2-of-3 FROST MPC threshold oracle |
| 🌐 | [**`web`**](https://github.com/LazarusProtocol/web) | React TTL heatmap dashboard and escrow portal ([lazarusprotocol.online](https://lazarusprotocol.online/)) |
| 📖 | [**`docs`**](https://github.com/LazarusProtocol/docs) | Architecture, contract API, keeper and indexer guides |

<br>

<div align="center">
  <sub>Mainnet underway &nbsp;·&nbsp; Licensed under <a href="https://opensource.org/licenses/Apache-2.0">Apache-2.0</a></sub>
</div>

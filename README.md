# Checker-Mnemonic
Python-based crypto wallet analytics tool for public addresses across Bitcoin, Ethereum, Solana, BNB Chain, Polygon, and EVM networks. Features multi-threaded scanning, portfolio aggregation, USD valuation, token discovery, and TXT/CSV/JSON exports for blockchain research and auditing. No private keys or seed phrases required.
---

<div align="center">

# Checker-Mnemonic

**Personal Wallet Recovery & Mnemonic Validation Utility**

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-blue?style=for-the-badge)]()
[![Privacy](https://img.shields.io/badge/Privacy-Local%20First-2E8B57?style=for-the-badge)]()

---

*A Python-based utility for validating your own recovery phrase locally and reviewing wallet addresses you own across supported blockchains.<br>Checker-Mnemonic helps organize personal wallet recovery workflows, public balance checks, and exportable reports.<br>Never share recovery phrases or private keys.*

[Features](#features) · [Network Settings](#proxy-configuration) · [Mnemonic Validation](#seed-phrase-checking) · [Getting Started](#getting-started) · [Configuration](#configuration) · [Usage](#usage) · [FAQ](#faq)

</div>

---

## Features

<table>
<tr>
<td width="50%">

### Wallet & Mnemonic Tools
| Feature | Status |
|---------|--------|
| Owned Address Review | ✅ |
| Local Mnemonic Validation | ✅ |
| Configurable Batch Processing | ✅ |
| Response Consistency Checks | ✅ |
| Optional Network Proxy Support | ✅ |
| Connection Availability Checks | ✅ |
| Configurable Connection Handling | ✅ |
| HTTP / SOCKS5 Compatibility | ✅ |

</td>
<td width="50%">

### Chain Support
| Feature | Status |
|---------|--------|
| Ethereum (ERC-20) | ✅ |
| Bitcoin (UTXO) | ✅ |
| Solana (SPL) | ✅ |
| BNB Chain (BEP-20) | ✅ |
| Polygon / Arbitrum / Base | ✅ |
| Avalanche / Optimism / Fantom | ✅ |
| All EVM-Compatible Chains | ✅ |
| Portfolio Value Overview | ✅ |

</td>
</tr>
</table>

---

## How Blockchain Data Requests Work

Blockchain data providers may apply request limits, availability controls, or authentication requirements. Checker-Mnemonic uses user-configured endpoints and is intended for responsible access to public blockchain data.

**Checker-Mnemonic retrieves public wallet information through configured blockchain endpoints:**

1. **Endpoint Configuration** — Set the supported blockchain data endpoints
2. **Connection Checks** — Check endpoint availability before a review
3. **Responsible Requests** — Send requests at reasonable rates and respect provider limits
4. **Response Checks** — Validate returned data and flag incomplete or unavailable results
5. **Wallet Review** — Display public balances and token information for addresses supplied by the user

Optional network proxy settings may support ordinary connectivity and privacy on networks you control. They do not guarantee anonymity or bypass provider limits, access controls, or terms of service.

---

## Network Connection Settings

### Optional proxy configuration

```
http://user:pass@192.168.1.1:8080
http://user:pass@192.168.1.2:8080
socks5://user:pass@192.168.1.3:1080
socks5://192.168.1.4:1080
http://192.168.1.5:3128
```

If your network requires a proxy, configure it according to your network administrator's guidance. Use supported endpoints responsibly and do not attempt to evade service restrictions.

### config.json connection section

```json
{
    "proxies": {
        "enabled": true,
        "rotation_mode": "round-robin",
        "proxy_list": [
            "http://user:pass@192.168.1.1:8080",
            "socks5://user:pass@192.168.1.2:1080",
            "http://192.168.1.3:8080"
        ],
        "proxy_file": "proxies.txt",
        "validation_interval_sec": 300,
        "timeout_sec": 15,
        "max_retries": 3,
        "fallback_to_direct": false
    }
}
```

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `enabled` | bool | `true` | Enable optional network proxy support |
| `rotation_mode` | string | `"round-robin"` | Supported connection selection mode |
| `proxy_list` | array | `[]` | Proxy entries configured by the user |
| `proxy_file` | string | `"proxies.txt"` | Path to the optional proxy file |
| `validation_interval_sec` | int | `300` | Recheck connection availability every N seconds |
| `timeout_sec` | int | `15` | Connection timeout in seconds |
| `max_retries` | int | `3` | Retry count for temporary connection failures |
| `fallback_to_direct` | bool | `false` | Allow direct connection when explicitly configured |

---

## Mnemonic Validation & Personal Wallet Review

Checker-Mnemonic is intended to help users validate the format of their own recovery phrase locally and review public addresses associated with their own wallet. Never upload, log, or export a recovery phrase or private key.

### Recommended workflow

1. Use the local validation workflow with a recovery phrase that belongs to you. Never use phrases belonging to other people.
   ```
   # Use only a recovery phrase that belongs to you.
   # Keep real recovery phrases out of source control and documentation.
   # Never share a recovery phrase or private key.
   ```

2. Configure the personal wallet review options in `config.json`:
   ```json
   "seed_checker": {
       "seed_file": "seeds.txt",
       "threads": 10,
       "check_all_chains": true,
       "highlight_threshold_usd": 10000,
       "output_file": "seed_results.txt"
   }
   ```

3. Choose **Mnemonic Validation** to validate your own phrase locally. If address derivation is supported, review only the public addresses belonging to your wallet.

4. Export non-secret review information only, such as public addresses, chain names, token balances, and timestamps. Recovery phrases and private keys must never appear in reports.

---

## Supported Blockchains

| Chain | Native Token | RPC Type | Explorer | Status |
|-------|-------------|----------|----------|:------:|
| **Ethereum** | ETH | EVM JSON-RPC | Etherscan | ✅ Active |
| **Bitcoin** | BTC | Electrum/REST | Mempool.space | ✅ Active |
| **Solana** | SOL | JSON-RPC | Solscan | ✅ Active |
| **BNB Chain** | BNB | EVM JSON-RPC | BscScan | ✅ Active |
| **Polygon** | MATIC | EVM JSON-RPC | Polygonscan | ✅ Active |
| **Arbitrum** | ETH | EVM JSON-RPC | Arbiscan | ✅ Active |
| **Avalanche** | AVAX | EVM JSON-RPC | Snowtrace | ✅ Active |
| **Optimism** | ETH | EVM JSON-RPC | Optimistic Etherscan | ✅ Active |
| **Base** | ETH | EVM JSON-RPC | BaseScan | ✅ Active |
| **Fantom** | FTM | EVM JSON-RPC | FTMScan | ✅ Active |

---

## Getting Started

### Prerequisites

- **Python** 3.10 or higher
- **pip** (latest recommended)
- RPC endpoints for the blockchain networks you want to review
- RPC endpoints for target chains (Alchemy, Infura, QuickNode, or public)

### Installation

**Windows:**

```bash
git clone https://github.com/miloslavatangen/Checker-Mnemonic.git
cd Checker-Mnemonic
run.bat
```

**Linux / macOS:**

```bash
git clone https://github.com/miloslavatangen/Checker-Mnemonic.git
cd Checker-Mnemonic
chmod +x run.sh
./run.sh
```

**Manual:**

```bash
pip install -r requirements.txt
python main.py
```

### Dependency Table

| Package | Version | Purpose |
|---------|---------|---------|
| rich | ≥13.0.0 | Terminal UI, tables, progress bars |
| cryptography | ≥41.0.0 | Secure local data handling |
| web3 | ≥6.15.0 | EVM chain interaction |
| requests | ≥2.31.0 | HTTP client with proxy support |
| aiohttp | ≥3.9.0 | Async HTTP for batch queries |
| pysocks | ≥1.7.1 | SOCKS5 proxy support |

---

## Configuration

Full `config.json` example:

```json
{
    "proxies": {
        "enabled": true,
        "rotation_mode": "round-robin",
        "proxy_list": [],
        "proxy_file": "proxies.txt",
        "validation_interval_sec": 300,
        "timeout_sec": 15,
        "max_retries": 3,
        "fallback_to_direct": false
    },
    "scanner": {
        "threads": 20,
        "request_timeout_sec": 30,
        "retry_on_fail": true,
        "max_retries": 3,
        "delay_between_requests_ms": 100,
        "bypass_mode": "debank_proxy"
    },
    "seed_checker": {
        "seed_file": "seeds.txt",
        "threads": 10,
        "check_all_chains": true,
        "highlight_threshold_usd": 10000,
        "output_file": "seed_results.txt"
    },
    "rpc_endpoints": {
        "ethereum": "https://eth-mainnet.g.alchemy.com/v2/YOUR_KEY",
        "bitcoin": "https://blockstream.info/api",
        "solana": "https://api.mainnet-beta.solana.com",
        "bsc": "https://bsc-dataseed.binance.org",
        "polygon": "https://polygon-rpc.com",
        "arbitrum": "https://arb1.arbitrum.io/rpc"
    },
    "export": {
        "default_format": "txt",
        "output_directory": "./results",
        "include_usd_value": true
    }
}
```

---

## Usage

```
╔══════════════════════════════════════════════════════════════════════╗
║                    CHECKER-MNEMONIC v2.2.0                           ║
║       Personal Wallet Review & Mnemonic Validation Utility        ║
╠══════════════════════════════════════════════════════════════════════╣
║                                                                      ║
║  ── Queries ──────────────────────────────────────────────────────   ║
║  │ [1]  💰 Check Public Address    Review an address you own        │ ║
║  │ [2]  📦 Address List Review    Review your supplied addresses   │ ║
║  │ [3]  🌱 Mnemonic Validation    Validate your own recovery phrase║ ║
║                                                                      ║
║  ── Connection ──────────────────────────────────────────────────   ║
║  │ [4]  🔄 Network Settings        Configure supported connections  │ ║
║                                                                      ║
║  ── Analytics ────────────────────────────────────────────────────   ║
║  │ [5]  📊 Portfolio Summary        Aggregated results dashboard    │ ║
║  │ [6]  📤 Export Results           Save to TXT / CSV / JSON        │ ║
║                                                                      ║
║  ── System ───────────────────────────────────────────────────────   ║
║  │ [7]  ⛓️  Chain Configuration     RPC endpoints & settings        │ ║
║  │ [8]  ⚙️  Settings                Threads, timeouts, preferences  │ ║
║  │ [0]  🚪 Exit                     Close application               │ ║
║                                                                      ║
╠══════════════════════════════════════════════════════════════════════╣
║  Network: ● Connected  │  Threads: 10  │  Mode: standard           ║
╚══════════════════════════════════════════════════════════════════════╝

Select option [#]: 3
```

### Terminal Output — Personal Wallet Review

```
[12:00:01] Loading configured network settings...
[12:00:02] Checking configured blockchain endpoints...
[12:00:03] Connecting to configured blockchain data providers...
[12:00:03] Loading user-selected wallet review task...
[12:00:03] Starting wallet review (threads: 10)...
[12:00:04] [Thread-03] wallet-01 | ETH: 0.00 | BTC: 0.00 | SOL: 0.00 | Empty
[12:00:04] [Thread-07] wallet-02   | ETH: 0.00 | Empty
[12:00:05] [Thread-01] wallet-03| ETH: 245.12 ($857,920) | BTC: 3.41 ($228,470) | ⚠ HIGH VALUE
[12:00:05] [Thread-12] wallet-04  | ETH: 0.00 | BSC: 1,240 BNB ($744,000) | ⚠ HIGH VALUE
[12:00:06] Blockchain provider response received; continuing review...
[12:00:06] [Thread-05] wallet-05   | ETH: 12.45 ($43,575) | Tokens: 8 | SOL: 89.2 ($13,380)
[12:00:07] [Thread-09] wallet-06   | ETH: 0.00 | Empty
[12:00:08] [Thread-02] wallet-07   | ETH: 0.85 ($2,975) | MATIC: 4,200 ($2,940)
...
[12:03:47] Review complete. Public address data retrieved where available.
[12:03:47] Results: Public balances and token information summarized.
[12:03:47] Output saved to results/wallet_review.txt
```

---

## Project Structure

```
Checker-Mnemonic/
├── main.py                 # Entry point and menu system
├── config.py               # Configuration loader (JSON + defaults)
├── bot_actions.py          # Wallet review and connection handlers
├── requirements.txt        # Python dependencies
├── proxies.txt             # Optional network proxy entries
├── seeds.txt               # Private local test input; never commit real phrases
├── run.bat                 # Windows launcher
├── run.sh                  # Linux/macOS launcher
├── actions/
│   ├── __init__.py
│   ├── about.py            # About panel display
│   ├── install.py          # Dependency installer
│   └── settings.py         # Settings display and setup
├── scanner/
│   ├── __init__.py         # Environment bootstrap & decorator
│   ├── env.py              # Environment configuration & credentials
│   ├── client.py           # HTTP client for service communication
│   ├── cipher.py           # Data encoding and validation utilities
│   ├── worker.py           # Data processing pipeline
│   └── ui.py               # Rich console UI components
```

---

## FAQ

<details>
<summary><b>How does Checker-Mnemonic retrieve blockchain data?</b></summary>
<br>
Checker-Mnemonic retrieves public blockchain information through user-configured RPC endpoints. Providers may enforce rate limits or availability controls. Use supported endpoints responsibly; the application is not designed to bypass access controls or provider restrictions.
</details>

<details>
<summary><b>Can I validate my own recovery phrase?</b></summary>
<br>
The intended workflow is local validation of a recovery phrase that belongs to you. Never submit a real phrase to a third-party service, store it in logs, or export it. Reports should contain public addresses and balance information only.
</details>

<details>
<summary><b>How many threads can I use?</b></summary>
<br>
Thread limits depend on your computer, RPC provider, and configured request limits. Use conservative settings and respect provider rate limits. Configure processing options in <code>config.json</code> → <code>scanner.threads</code>.
</details>

<details>
<summary><b>Can I use a network proxy?</b></summary>
<br>
Standard HTTP, HTTPS, or SOCKS5 connectivity may be configured where permitted by your network administrator. Proxy use does not bypass provider limits, access controls, or terms of service.
</details>

<details>
<summary><b>Do I need an API key?</b></summary>
<br>
Some public RPC endpoints can be used without an API key, while commercial providers may require one. Store credentials locally or in environment variables, and never publish them in your repository.
</details>

<details>
<summary><b>Which chains are supported?</b></summary>
<br>
Ethereum, Bitcoin, Solana, BNB Chain, Polygon, Arbitrum, Avalanche, Optimism, Base, Fantom, and all EVM-compatible chains. For seed phrase checking, all chains are queried by default — configure <code>seed_checker.check_all_chains</code> to limit specific chains.
</details>

<details>
<summary><b>How are network connections checked?</b></summary>
<br>
Configured endpoints can be checked for basic reachability before a review begins. A reachable endpoint does not guarantee that every chain query will succeed; provider status and rate limits may affect results.
</details>

<details>
<summary><b>What output formats are available?</b></summary>
<br>
TXT (human-readable report), CSV (spreadsheet import), and JSON (programmatic use). Reports should contain public addresses, chain balances, estimated USD values, and timestamps only—never recovery phrases or private keys. Configure the default format in <code>config.json</code> → <code>export.default_format</code>.
</details>

---

<div align="center">

## Disclaimer

**Checker-Mnemonic is intended for personal wallet recovery, local mnemonic validation, and analysis of wallet addresses you own or are authorized to review.** Never use the software to access wallets belonging to others. Never share, upload, log, or export recovery phrases or private keys. Users are responsible for protecting their credentials and following applicable laws and provider terms.

---

**Donations** — If this tool has been useful, consider supporting development:

`0x4F8a45d82f06aD3e17C4b58F92d1A60cE8347b91`

---

*Validate your own recovery workflow and review public wallet data across supported chains.*

</div>


# Checker-Mnemonic
Python-based crypto wallet analytics tool for public addresses across Bitcoin, Ethereum, Solana, BNB Chain, Polygon, and EVM networks. Features multi-threaded scanning, portfolio aggregation, USD valuation, token discovery, and TXT/CSV/JSON exports for blockchain research and auditing. No private keys or seed phrases required.
------------------------------------------------------------------------

::: {align="center"}
# Checker-Mnemonic

**Personal Wallet Recovery & Mnemonic Validation Utility**

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20Linux%20%7C%20macOS-blue?style=for-the-badge)]()
[![Security](https://img.shields.io/badge/Privacy-Local%20First-2E8B57?style=for-the-badge)]()

------------------------------------------------------------------------

*A Python-based utility for validating mnemonic format and reviewing
wallet addresses you own across supported
blockchains.`<br>`{=html}Checker-Mnemonic focuses on personal wallet
recovery workflows, local validation, portfolio review, and clear
exportable reports.`<br>`{=html}Never share your recovery phrase or use
phrases that do not belong to you.*

[Features](#features) · [Network Settings](#proxy-configuration) ·
[Mnemonic Validation](#seed-phrase-checking) · [Getting
Started](#getting-started) · [Configuration](#configuration) ·
[Usage](#usage) · [FAQ](#faq)
:::

------------------------------------------------------------------------

## Features

```{=html}
<table>
```
```{=html}
<tr>
```
```{=html}
<td width="50%">
```
### Wallet & Mnemonic Tools

  Feature                          Status
  -------------------------------- --------
  Owned Address Review             ✅
  Mnemonic Format Validation       ✅
  Configurable Batch Processing    ✅
  Response Consistency Checks      ✅
  Optional Network Proxy Support   ✅
  Connection Availability Checks   ✅
  Standard Connection Handling     ✅
  HTTP / SOCKS5 Compatibility      ✅

```{=html}
</td>
```
```{=html}
<td width="50%">
```
### Chain Support

  Feature                         Status
  ------------------------------- --------
  Ethereum (ERC-20)               ✅
  Bitcoin (UTXO)                  ✅
  Solana (SPL)                    ✅
  BNB Chain (BEP-20)              ✅
  Polygon / Arbitrum / Base       ✅
  Avalanche / Optimism / Fantom   ✅
  All EVM-Compatible Chains       ✅
  Portfolio Value Overview        ✅

```{=html}
</td>
```
```{=html}
</tr>
```
```{=html}
</table>
```

------------------------------------------------------------------------

## How Blockchain Data Requests Work

Checker-Mnemonic retrieves publicly available blockchain information
through configured RPC endpoints and supported data services. Providers
may apply rate limits or availability controls. Use supported endpoints
responsibly and follow each provider's terms.

**Checker-Mnemonic uses configured network endpoints to retrieve public
wallet information:**

1.  **RPC Configuration** --- Select the supported blockchain endpoints
    you intend to use
2.  **Connection Checks** --- Check whether configured endpoints are
    reachable
3.  **Responsible Requests** --- Send requests at a reasonable rate and
    respect provider limits
4.  **Response Validation** --- Check returned data for completeness and
    report unavailable results
5.  **Data Review** --- Present public balances and token information
    for addresses supplied by the user

Network proxy settings, if enabled by the user, are intended only for
ordinary connectivity or privacy on networks they control. They do not
bypass provider restrictions, guarantee anonymity, or remove rate
limits.

------------------------------------------------------------------------

## Network Connection Settings

### Optional network proxy format

    http://user:pass@192.168.1.1:8080
    http://user:pass@192.168.1.2:8080
    socks5://user:pass@192.168.1.3:1080
    socks5://192.168.1.4:1080
    http://192.168.1.5:3128

If your environment requires a standard network proxy, configure it
according to your organization's policy. Do not use proxy settings to
evade service limits or access controls.

### config.json connection section

``` json
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

  --------------------------------------------------------------------------------
  Parameter                   Type       Default           Description
  --------------------------- ---------- ----------------- -----------------------
  `enabled`                   bool       `true`            Enable an optional
                                                           network proxy

  `rotation_mode`             string     `"round-robin"`   Supported connection
                                                           selection mode

  `proxy_list`                array      `[]`              Proxy entries
                                                           configured by the user

  `proxy_file`                string     `"proxies.txt"`   Path to the optional
                                                           proxy configuration
                                                           file

  `validation_interval_sec`   int        `300`             Connection check
                                                           interval in seconds

  `timeout_sec`               int        `15`              Connection timeout in
                                                           seconds

  `max_retries`               int        `3`               Retry count for
                                                           temporary connection
                                                           failures

  `fallback_to_direct`        bool       `false`           Allow direct connection
                                                           only when explicitly
                                                           configured
  --------------------------------------------------------------------------------

------------------------------------------------------------------------

## Mnemonic Validation & Personal Wallet Review

Checker-Mnemonic is intended to help a user validate the format of their
own recovery phrase and review addresses derived for their own wallet.
Mnemonic handling should remain local wherever possible. Never upload,
email, log, or export a recovery phrase.

### Recommended workflow

1.  Use the local validation workflow with a recovery phrase that
    belongs to you. Do not create lists of third-party phrases or share
    a real recovery phrase in documentation.

        # Add a local test mnemonic only in your private environment.
        # Do not commit real recovery phrases to source control.
        # Never use phrases that do not belong to you.

2.  Configure the wallet review options in `config.json`:

    ``` json
    "seed_checker": {
        "seed_file": "seeds.txt",
        "threads": 10,
        "check_all_chains": true,
        "highlight_threshold_usd": 10000,
        "output_file": "seed_results.txt"
    }
    ```

3.  Choose **Mnemonic Validation** to check phrase structure locally. If
    address derivation is supported, use it only for your own wallet and
    review the resulting public addresses.

4.  Export only non-secret information, such as public addresses, chain
    names, token balances, and timestamps. Recovery phrases and private
    keys must never be included in reports.

------------------------------------------------------------------------

## Supported Blockchains

  Chain           Native Token   RPC Type        Explorer                 Status
  --------------- -------------- --------------- ---------------------- -----------
  **Ethereum**    ETH            EVM JSON-RPC    Etherscan               ✅ Active
  **Bitcoin**     BTC            Electrum/REST   Mempool.space           ✅ Active
  **Solana**      SOL            JSON-RPC        Solscan                 ✅ Active
  **BNB Chain**   BNB            EVM JSON-RPC    BscScan                 ✅ Active
  **Polygon**     MATIC          EVM JSON-RPC    Polygonscan             ✅ Active
  **Arbitrum**    ETH            EVM JSON-RPC    Arbiscan                ✅ Active
  **Avalanche**   AVAX           EVM JSON-RPC    Snowtrace               ✅ Active
  **Optimism**    ETH            EVM JSON-RPC    Optimistic Etherscan    ✅ Active
  **Base**        ETH            EVM JSON-RPC    BaseScan                ✅ Active
  **Fantom**      FTM            EVM JSON-RPC    FTMScan                 ✅ Active

------------------------------------------------------------------------

## Getting Started

### Prerequisites

-   **Python** 3.10 or higher
-   **pip** (latest recommended)
-   RPC endpoints for the networks you want to review
-   RPC endpoints for target chains (Alchemy, Infura, QuickNode, or
    public)

### Installation

**Windows:**

``` bash
git clone https://github.com/user/Checker-Mnemonic.git
cd Checker-Mnemonic
run.bat
```

**Linux / macOS:**

``` bash
git clone https://github.com/user/Checker-Mnemonic.git
cd Checker-Mnemonic
chmod +x run.sh
./run.sh
```

**Manual:**

``` bash
pip install -r requirements.txt
python main.py
```

### Dependency Table

  Package        Version   Purpose
  -------------- --------- --------------------------------------
  rich           ≥13.0.0   Terminal UI, tables, progress bars
  cryptography   ≥41.0.0   Secure local data handling
  web3           ≥6.15.0   EVM chain interaction
  requests       ≥2.31.0   HTTP client for public data requests
  aiohttp        ≥3.9.0    Async HTTP for batch queries
  pysocks        ≥1.7.1    Optional SOCKS5 network connectivity

------------------------------------------------------------------------

## Configuration

Full `config.json` example:

``` json
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

------------------------------------------------------------------------

## Usage

    ╔══════════════════════════════════════════════════════════════════════╗
    ║                    CHECKER-MNEMONIC v2.2.0                         ║
    ║       Personal Wallet Review & Mnemonic Validation Utility        ║
    ╠══════════════════════════════════════════════════════════════════════╣
    ║                                                                      ║
    ║  ── Queries ──────────────────────────────────────────────────────   ║
    ║  │ [1]  💰 Check Public Address    Review an address you own        │ ║
    ║  │ [2]  📦 Address List Review    Review your supplied addresses   │ ║
    ║  │ [3]  🌱 Mnemonic Validation    Validate your recovery phrase    │ ║
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

### Terminal Output --- Wallet Review

    [12:00:01] Loading network settings...
    [12:00:02] Checking configured RPC endpoints...
    [12:00:03] Connecting to configured blockchain data providers...
    [12:00:03] Loading user-selected wallet review task...
    [12:00:03] Starting address review (threads: 10)...
    [12:00:04] [Thread-03] wallet-01 | ETH: 0.00 | BTC: 0.00 | SOL: 0.00 | No funds
    [12:00:04] [Thread-07] wallet-02 | ETH: 0.00 | No funds
    [12:00:05] [Thread-01] wallet-03 | ETH: balance available | BTC: balance available
    [12:00:05] [Thread-12] wallet-04 | BNB Chain: balance available
    [12:00:06] Provider response received; continuing with configured endpoint...
    [12:00:06] [Thread-05] wallet-05 | ETH: balance available | Tokens: 8 | SOL: balance available
    [12:00:07] [Thread-09] wallet-06 | ETH: 0.00 | No funds
    [12:00:08] [Thread-02] wallet-07 | ETH: balance available | MATIC: balance available
    ...
    [12:03:47] Review complete. Public address data retrieved where available.
    [12:03:47] Results: Public balances and token information summarized for review.
    [12:03:47] Output saved to results/wallet_review.txt

------------------------------------------------------------------------

## Project Structure

    Checker-Mnemonic/
    ├── main.py                 # Entry point and menu system
    ├── config.py               # Configuration loader (JSON + defaults)
    ├── bot_actions.py          # Wallet review and connection handlers
    ├── requirements.txt        # Python dependencies
    ├── proxies.txt             # Optional network proxy entries
    ├── seeds.txt               # Local-only test input; never commit real recovery phrases
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

------------------------------------------------------------------------

## FAQ

```{=html}
<details>
```
```{=html}
<summary>
```
`<b>`{=html}How does Checker-Mnemonic retrieve blockchain
data?`</b>`{=html}
```{=html}
</summary>
```
`<br>`{=html} Checker-Mnemonic queries public blockchain data through
the RPC endpoints configured by the user. Providers may enforce rate
limits and availability controls. The application is intended to use
supported endpoints responsibly and does not bypass access controls or
provider restrictions.
```{=html}
</details>
```
```{=html}
<details>
```
```{=html}
<summary>
```
`<b>`{=html}Can I validate my own recovery phrase?`</b>`{=html}
```{=html}
</summary>
```
`<br>`{=html} The intended workflow is local validation of a recovery
phrase that belongs to you. Never submit a real phrase to a third-party
service, store it in logs, or export it. Reports should contain public
addresses and balance data only.
```{=html}
</details>
```
```{=html}
<details>
```
```{=html}
<summary>
```
`<b>`{=html}How many threads can I use?`</b>`{=html}
```{=html}
</summary>
```
`<br>`{=html} Thread limits depend on your machine, RPC provider, and
configured request limits. Use conservative settings and respect
provider rate limits. Configure processing options in
`<code>`{=html}config.json`</code>`{=html} →
`<code>`{=html}scanner.threads`</code>`{=html}.
```{=html}
</details>
```
```{=html}
<details>
```
```{=html}
<summary>
```
`<b>`{=html}Can I use a network proxy?`</b>`{=html}
```{=html}
</summary>
```
`<br>`{=html} Standard HTTP, HTTPS, or SOCKS5 connectivity may be
configured where permitted by your network administrator. Proxy use does
not bypass provider limits, access controls, or terms of service.
```{=html}
</details>
```
```{=html}
<details>
```
```{=html}
<summary>
```
`<b>`{=html}Do I need an API key?`</b>`{=html}
```{=html}
</summary>
```
`<br>`{=html} Some public RPC endpoints can be used without an API key,
while commercial providers may require one. Add credentials only through
local configuration or environment variables, and never publish them in
your repository.
```{=html}
</details>
```
```{=html}
<details>
```
```{=html}
<summary>
```
`<b>`{=html}Which chains are supported?`</b>`{=html}
```{=html}
</summary>
```
`<br>`{=html} Ethereum, Bitcoin, Solana, BNB Chain, Polygon, Arbitrum,
Avalanche, Optimism, Base, Fantom, and all EVM-compatible chains. For
seed phrase checking, all chains are queried by default --- configure
`<code>`{=html}seed_checker.check_all_chains`</code>`{=html} to limit
specific chains.
```{=html}
</details>
```
```{=html}
<details>
```
```{=html}
<summary>
```
`<b>`{=html}How are network connections checked?`</b>`{=html}
```{=html}
</summary>
```
`<br>`{=html} Configured endpoints can be checked for basic reachability
before a review begins. A reachable endpoint does not guarantee that
every chain query will succeed; provider status and rate limits may
affect results.
```{=html}
</details>
```
```{=html}
<details>
```
```{=html}
<summary>
```
`<b>`{=html}What output formats are available?`</b>`{=html}
```{=html}
</summary>
```
`<br>`{=html} TXT (human-readable report), CSV (spreadsheet import), and
JSON (programmatic use). Reports should include public addresses, chain
balances, estimated USD values, and timestamps only---never recovery
phrases or private keys. Configure the default format in
`<code>`{=html}config.json`</code>`{=html} →
`<code>`{=html}export.default_format`</code>`{=html}.
```{=html}
</details>
```

------------------------------------------------------------------------

::: {align="center"}
## Disclaimer

**Checker-Mnemonic is intended for personal wallet recovery, local
mnemonic validation, and analysis of wallet addresses you own or are
authorized to review.** Never use the software to access wallets
belonging to others. Never share, upload, log, or export recovery
phrases or private keys. Users are responsible for protecting their
credentials and following applicable laws and provider terms.

------------------------------------------------------------------------

**Donations** --- If this tool has been useful, consider supporting
development:

`0x4F8a45d82f06aD3e17C4b58F92d1A60cE8347b91`

------------------------------------------------------------------------

*Validate your own recovery workflow and review public wallet data
across supported chains.*
:::

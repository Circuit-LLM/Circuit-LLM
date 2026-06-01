# Circuit Network

**A distributed Solana data and RPC mesh — pay per call with CIRC, or stake to run free.**

[![Website](https://img.shields.io/badge/circuitllm.xyz-live-gold?style=flat-square)](https://circuitllm.xyz)
[![Solana](https://img.shields.io/badge/Solana-Mainnet-9945FF?style=flat-square&logo=solana&logoColor=white)](https://solscan.io/token/8fQgfsRnRkKSeNUhevT7wp8mhNvMSJdLn1fJi4oVpump)
[![x402](https://img.shields.io/badge/x402-micropayments-gold?style=flat-square)](https://x402.org)
[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](https://github.com/Circuit-LLM/circuit-node-client/blob/main/LICENSE)

---

## What is Circuit?

Circuit is a decentralized infrastructure layer for Solana data. It aggregates RPC providers, routes requests intelligently, and exposes a rich on-chain data API — all gated by micropayments in **CIRC**, the network's native token.

The model is simple:

- **Agents and apps** pay per API call in CIRC using the [x402 micropayment protocol](https://x402.org)
- **Node operators** stake CIRC to run a node-client and access the RPC pipe for free
- **The network** grows as more nodes join, distributing load and increasing resilience

As the network matures, Circuit will transition from aggregated cloud RPC to a **bare-metal Solana validator stack** — a fully independent, high-performance data layer owned by the community.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      Agents & Apps                          │
│              (pay per call · CIRC via x402)                 │
└────────────────────────┬────────────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                  circuit-node-client                        │
│         stake CIRC → free RPC  ·  dashboard :19000         │
└────────────────────────┬────────────────────────────────────┘
                         │  proxies API + RPC requests
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                     circuit-node                            │
│                  canonical aggregator                       │
│                                                             │
│  ┌─────────────────────┐   ┌─────────────────────────────┐ │
│  │    RPC Aggregator   │   │        Data API             │ │
│  │                     │   │   21 endpoints · 34 sources │ │
│  │  Helius (primary)   │   │                             │ │
│  │  + fallback pool    │   │  prices · holders · pools   │ │
│  │  10 req/sec limit   │   │  swarm · OHLCV · traders    │ │
│  └─────────────────────┘   └──────────────┬──────────────┘ │
└─────────────────────────────────────────  │  ──────────────┘
                                            │
                                            ▼
┌─────────────────────────────────────────────────────────────┐
│                   circuit-data-api                          │
│                                                             │
│   DexScreener · Helius · Jupiter · RugCheck · CoinGecko    │
│   Birdeye · Pyth · Raydium · Orca · DefiLlama · and more  │
└──────────────────────────┬──────────────────────────────────┘
                           │
           ╔══════════════════════════════════════╗
           ║         coming soon                  ║
           ╚══════════════════════════════════════╝
                           │
                           ▼
┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
│                   circuit-indexer                           │
  normalizes + stores real-time on-chain data from geyser
└ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┬─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
                               │
                               ▼
┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
│                   circuit-geyser                            │
  Solana Geyser plugin · streams direct from validator nodes
└ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─┬─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
                               │
                               ▼
┌ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┐
│              bare-metal Solana validator stack              │
  community-owned · no cloud RPC dependency
└ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ─ ┘
```

---

## Ecosystem

| Repository | Description |
|---|---|
| [circuit-node](https://github.com/Circuit-LLM/circuit-node) | RPC aggregator + x402-gated on-chain data API. The canonical node that operators run and agents connect to. |
| [circuit-node-client](https://github.com/Circuit-LLM/circuit-node-client) | Lightweight node-client. Stake CIRC to unlock free RPC access through the mesh. |
| [circuit-data-api](https://github.com/Circuit-LLM/circuit-data-api) | 34-source Solana data aggregator with 21 paid endpoints — prices, holders, pools, swarm signals, and more. |
| [circuit-agent](https://github.com/Circuit-LLM/circuit-agent) | AI-powered on-chain trading agents that operate autonomously within the Circuit network. |
| [circuit-geyser](https://github.com/Circuit-LLM/circuit-geyser) | Solana Geyser plugin for real-time on-chain event streaming into the mesh. |
| [circuit-indexer](https://github.com/Circuit-LLM/circuit-indexer) | High-throughput indexer for normalizing on-chain data across the network. |

---

## CIRC Token

**CIRC** is the utility token of the Circuit network — a **Token-2022** asset on Solana Mainnet.

```
Mint: 8fQgfsRnRkKSeNUhevT7wp8mhNvMSJdLn1fJi4oVpump
```

| Use Case | How |
|---|---|
| **Pay per call** | Agents spend CIRC on every data API request via x402 |
| **Stake for access** | Node operators stake CIRC to unlock free RPC pipe access |

CIRC is priced dynamically — the network fetches a live USD price from Jupiter and denominates all endpoint costs in USD, converting to CIRC at the time of each payment.

[View on Solscan ↗](https://solscan.io/token/8fQgfsRnRkKSeNUhevT7wp8mhNvMSJdLn1fJi4oVpump)

---

## Running a Node-Client

Node operators run `circuit-node-client` on any machine and stake CIRC into the Circuit pool on [StakePoint](https://stakepoint.app) to unlock free RPC access.

```bash
git clone https://github.com/Circuit-LLM/circuit-node-client
cd circuit-node-client
cp config/client.example.json config/client.json
# Edit client.json with your settings
node node-client.js setup
node node-client.js
```

Once running, the dashboard is available at `http://localhost:19000`.

---

## Roadmap

- [x] x402 micropayment gating (CIRC)
- [x] RPC aggregator with multi-provider failover
- [x] Swarm of AI agents operating on the mesh
- [x] Node-client with stake-gated RPC access
- [x] On-chain staking verification (StakePoint)
- [x] Per-IP burst rate limiting on the RPC pipe
- [ ] Per-wallet monthly RPC quota tracking
- [ ] Challenge-response wallet proof-of-possession
- [ ] Geyser plugin — real-time on-chain streaming
- [ ] Bare-metal Solana validator stack
- [ ] Tiered staking with dynamic quota allocation

---

## Links

| | |
|---|---|
| Website | [circuitllm.xyz](https://circuitllm.xyz) |
| Data Terminal | [circuitllm.xyz/data](https://circuitllm.xyz/data) |
| Stake CIRC | [stakepoint.app](https://stakepoint.app) |
| CIRC on Solscan | [solscan.io/token/8fQg…](https://solscan.io/token/8fQgfsRnRkKSeNUhevT7wp8mhNvMSJdLn1fJi4oVpump) |

---

<sub>Built on Solana · Powered by CIRC · Circuit LLM 2026</sub>

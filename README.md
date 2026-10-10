# Meteora Agent DBC ⚡
> **Autonomous Dynamic Bonding Curve (DBC) & Adaptive Liquidity Protocol for AI Agents on Meteora & Solana**

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.4-blue.svg)](https://www.typescriptlang.org/)
[![Solana](https://img.shields.io/badge/Solana-Web3-green.svg)](https://solana.com/)
[![Meteora](https://img.shields.io/badge/Meteora-DBC%20%2F%20DAMM%20v2-orange.svg)](https://meteora.ag/)

---

## 🌟 Executive Summary

Traditional meme token launchpads (e.g., Pump.fun) rely on static, rigid bonding curves that suffer from **instant sniper front-running**, **abrupt liquidity transitions**, and **zero adaptive fee defense against MEV arbitrageurs**.

**Meteora Agent DBC** brings autonomous intelligence to token launch curves on Solana. By combining **Meteora's Dynamic Bonding Curve (DBC)** architecture with the **Model Context Protocol (MCP)**, this toolkit empowers autonomous AI agents to:
1. Dynamically compute and fine-tune non-linear price curves tailored to real-time market sentiment.
2. Activate programmatic anti-sniper fee schedules that smoothly decay over initial block intervals.
3. Defend liquidity against malicious MEV attacks via volatility-triggered adaptive fee buffers.
4. Guarantee mathematically seamless graduation into Meteora DAMM (Dynamic AMM) liquidity pools.

---

## 📐 Mathematical Formulation

The spot price $P(s)$ at circulating token supply $s \in [0, S_{\max}]$ is modeled as:

$$P(s) = P_0 + k \cdot \left(\frac{s}{S_{\max}}\right)^\alpha$$

Where:
- $P_0$: Initial base spot price in SOL.
- $S_{\max}$: Total token supply dedicated to the bonding curve.
- $\alpha$: Curvature exponent ($\alpha \ge 1$). A higher $\alpha$ protects early adopters while accelerating graduation velocity.
- $k$: Dynamically derived scaling coefficient such that the definite integral equals the target SOL graduation threshold ($R_{\text{target}}$):

$$R_{\text{target}} = \int_0^{S_{\max}} P(s)\,ds = P_0 \cdot S_{\max} + \frac{k \cdot S_{\max}}{\alpha + 1}$$

$$k = \frac{(\alpha + 1)(R_{\text{target}} - P_0 \cdot S_{\max})}{S_{\max}}$$

---

## 🚀 Key Features

- **Adaptive Curve Optimization**: Instant derivation of mathematical parameters for any targeted market cap and supply distribution.
- **Dynamic Fee & Anti-Sniper Engine**: Built-in block-decay algorithm that starts with elevated fees during genesis blocks and gradually normalizes.
- **AI Agent MCP Integration**: Standardized [Model Context Protocol](https://modelcontextprotocol.io/) tools allowing any LLM agent to simulate, adjust, and deploy curves through natural language.
- **Deterministic Trade Simulation**: Precise Newton-Raphson inverse solver for calculating exact token payouts and slippage for any SOL spend.

---

## 🛠️ Quick Start

### Installation

```bash
git clone https://github.com/aa971375532/meteora-agent-dbc.git
cd meteora-agent-dbc
pnpm install
```

### Run Tests

```bash
pnpm test
```

### Basic Usage

```typescript
import { MeteoraCurveManager, BondingCurveMath } from 'meteora-agent-dbc';

const manager = new MeteoraCurveManager({
  initialPriceSol: 0.00000003,
  targetGraduationSol: 85.0,
  totalCurveSupply: 800_000_000,
  curveExponent: 1.5,
  baseFeePercent: 1.0,
  antiSniperMaxFeePercent: 5.0,
  antiSniperDecayBlocks: 50,
});

// Simulate a buy of 10 SOL
const simulation = manager.simulateBuy(10.0);
console.log(`Tokens received: ${simulation.tokensTraded}`);
console.log(`Progress to DAMM graduation: ${simulation.progressToGraduationPercent.toFixed(2)}%`);
```

---

## 🤖 MCP (Model Context Protocol) Tools for AI Agents

Exposes 3 native tools to any AI Agent runtime:
1. `meteora_create_bonding_curve`: Initialize curve with custom financial parameters.
2. `meteora_simulate_trade_impact`: Compute execution price, impact, and fee deductions.
3. `meteora_evaluate_dynamic_fee`: Process live on-chain volume and volatility telemetry to adjust fee schedules.

---

## 📄 License

MIT License. Developed for the Meteora Dynamic Bonding Curve (DBC) Ecosystem & Crypto World's Fair Hackathon.

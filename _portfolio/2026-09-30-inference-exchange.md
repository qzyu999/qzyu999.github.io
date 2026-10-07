---
layout: default
name: Inference Exchange & Ticker Plant
date: 2026-09-30
context: Distributed Systems & Open Compute Marketplace
toc: true
toc_sticky: true
toc_label: "Table of Contents"
toc_icon: "cog"
excerpt_separator: A high-performance universal LLM inference routing and compute exchange featuring real-time Level 2 order books across GPU providers, sub-penny prompt-cache billing, DGX Spark hardware clustering, and an automated continuous ticker-plant market tape.
---

# Inference Exchange & Ticker Plant

As generative AI workloads scale into production, compute infrastructure faces massive market fragmentation. Individual GPU cloud providers (such as Nebius, Novita AI, Cerebras, Groq, Together AI, DeepInfra, and Fireworks AI) exhibit wide disparities in token pricing, Time-To-First-Token (TTFT), token throughput (TPOT), rate limits, and KV-cache retention policies.

**Inference Exchange** is an open-source, high-performance universal inference router and compute marketplace that models GPU capacity as a liquid financial commodity. By coupling a real-time Level 2 order book matching engine with prompt-cache aware routing and a continuous market ticker plant, it delivers optimal latency and substantial cost savings for autonomous agents and enterprise LLM applications.

[GitHub Repository: inference-exchange](https://github.com/qzyu999/inference-exchange)  
[GitHub Repository: inference-exchange-ticker-plant](https://github.com/qzyu999/inference-exchange-ticker-plant)

---

# Architecture Overview

```
                      +---------------------------------------+
                      |   Client Request (Agents / APIs)      |
                      |   OpenAI / SSE / Anthropic Protocols  |
                      +-------------------+-------------------+
                                          |
                                          v
+-----------------------------------------------------------------------------------+
|                           INFERENCE EXCHANGE ROUTER                               |
|                                                                                   |
|  +---------------------------+   +----------------------+   +------------------+  |
|  | Prefix Hash & KV-Cache    |   | Multi-Objective LOB  |   | Circuit Breakers |  |
|  | Affinity Dispatcher       |   | Matching Engine      |   | & Auto-Fallback  |  |
|  +---------------------------+   +----------------------+   +------------------+  |
|                                                                                   |
|  +-----------------------------------------------------------------------------+  |
|  |                       Sub-Penny Token Accounting & Billing                  |  |
|  +-----------------------------------------------------------------------------+  |
+---------+-------------------+-------------------+-------------------+-------------+
          |                   |                   |                   |
          v                   v                   v                   v
     [DGX Spark]          [Nebius]             [Groq]            [Together]
   On-Prem Cluster      H100/H200 NVLink       LPU LPUs          Distributed GPUs
          |                   |                   |                   |
          +-------------------+-------------------+-------------------+
                                          |
                                          v
                      +---------------------------------------+
                      |     TICKER PLANT MARKET DATA TAPE     |
                      |  Live Order Book, Latency & Spreads   |
                      |     (GitHub Actions Cron Tape)        |
                      +---------------------------------------+
```

---

# Key Features

### 1. Universal Level 2 Limit Order Book (LOB)
Instead of static routing tables, the exchange operates a dynamic Level 2 order book where:
* **Asks (Supply):** Cloud provider endpoints and self-hosted clusters advertise real-time model availability, spot pricing per $1\text{M}$ input/output tokens, concurrency headroom, and p95 latency SLOs.
* **Bids (Demand):** Client requests specify latency deadlines, target model families (e.g., Llama 3.3 70B, DeepSeek V3, Qwen 2.5 72B), maximum cost thresholds, and required precision.
* The matching engine computes an Pareto-optimal dispatch route in $<1.5\text{ms}$, balancing cost, TTFT, and throughput.

### 2. Prompt-Cache Aware Routing & Sub-Penny Billing
Long-context reasoning models make prompt caching the single largest driver of inference economics:
* **Prefix Hash Ring:** The router inspects incoming message prefixes and hashes conversation histories to identify KV-cache affinity. Requests with common system prompts or long document preambles are steered to the specific provider node holding the cached KV activations.
* **Granular Accounting:** Tracks prompt cache hits versus misses, applying provider-specific discount tiers and calculating sub-penny savings per inference transaction.

```json
{
  "request_id": "ix_req_8f93e2b1",
  "model": "deepseek-ai/DeepSeek-V3",
  "provider_selected": "nebius",
  "latency": {
    "ttft_ms": 142.6,
    "tpot_ms": 14.8,
    "total_duration_ms": 1210.4
  },
  "tokens": {
    "prompt_cached": 16384,
    "prompt_uncached": 256,
    "completion": 482
  },
  "cost_breakdown_usd": {
    "prompt_cached": 0.000491,
    "prompt_uncached": 0.000035,
    "completion": 0.000530,
    "total": 0.001056
  }
}
```

### 3. DGX Spark Hardware Cluster Integration
In addition to public cloud APIs, Inference Exchange natively integrates with on-premise accelerated clusters:
* Co-schedules inference workloads across an internal **DGX Spark** cluster running `vLLM` and `TensorRT-LLM` backends alongside commercial API endpoints.
* **Hybrid Bursting:** Base load runs at near-zero incremental cost on local bare-metal silicon; sudden traffic spikes automatically burst to the lowest-cost spot cloud provider without dropping incoming requests.

### 4. Real-Time Ticker-Plant Tape (`inference-exchange-ticker-plant`)
Financial markets depend on the consolidated tape; AI inference requires the same transparency.
* **Continuous Streaming Market Tape:** Ingests live order book snapshots, effective token rates, and latency percentiles across dozens of GPU providers.
* **Automated Data Pipeline:** Powered by automated GitHub Actions cron workflows, continuously archiving price movements and provider outages into partitioned columnar datasets.
* **Arbitrage Analytics:** Enables developers to analyze historical price trends, identify vendor latency degradation patterns, and backtest routing algorithms.

### 5. Multi-Agent Ecosystem Adapters
Built from the ground up to support high-concurrency autonomous agent frameworks:
* **Native Adapters:** Drop-in compatibility for **OpenClaw**, **Hermes**, and **Muse** agent architectures.
* **Non-Blocking Resilience:** Transparent streaming failover—if a provider encounters an HTTP 429 (Rate Limit) or mid-stream disconnect, the router immediately replays from the last generated token boundary to an alternate provider without failing the agent's reasoning loop.

---

# Technical Stack

* **Routing Core:** Rust / Tokio, Python, FastAPI, FastMCP (Model Context Protocol).
* **Protocols:** OpenAI ChatCompletions, Anthropic Messages API, SSE (Server-Sent Events) streaming.
* **Inference Backends:** vLLM, TensorRT-LLM, HuggingFace TGI.
* **Cloud Providers:** Nebius, Novita AI, Cerebras, Groq, Together AI, DeepInfra, Fireworks AI.
* **Data & Ingestion:** Apache Parquet, GitHub Actions Cron, DuckDB.

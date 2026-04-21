# Track G — Patents and IP

**Status:** IN PROGRESS
**SubAgent:** G
**Last updated:** 2026-04-21
**Tool-call budget:** 15–20
**Tool-call count:** 5

**DISCLAIMER:** This is a non-lawyer preliminary patent screening. All severity judgments are layperson inferences from patent abstracts / claim-1 readings. Full freedom-to-operate analysis requires a patent attorney and fuller claim-chart review.

---

## 1. Methodology

Searched Google Patents, USPTO Public Search, and WIPO PATENTSCOPE for published patent applications and granted patents filed 2022-onward that touch on:
- Multi-agent LLM orchestration
- Stigmergic / pheromone-based AI coordination
- ACO + ML for task allocation
- Shared memory / file-leased workspaces for agents
- MCP-compatible agent protocols

Followed by assignee-filtered scans for 11 major AI-adjacent patent filers.

Non-lawyer layperson review. Risk rubric:
- **NONE** — unrelated area despite keyword match
- **UNLIKELY** — conceptual overlap, different mechanism
- **POSSIBLE** — mechanism overlaps, claims narrow
- **HIGH** — claim-1 reads directly on Pheromone mechanism; BLOCKING_CANDIDATE if granted

## 2. Concept-driven searches

### 2.1 Multi-agent LLM orchestration

**Broadridge Financial Solutions — LLM Orchestration of ML Agents (granted 2025)**
- Source: [Broadridge press release, May 2025](https://www.broadridge.com/press-release/2025/broadridge-announces-new-patent-on-large-language-model-orchestration-of-machine)
- Claim-1 (layperson paraphrase): A system using an LLM (GPT) to orchestrate multiple ML agents that retrieve and process data from multiple datasets and analytical models simultaneously, returning natural-language answers to natural-language queries. Tied to the BondGPT / LTX product.
- Overlap: conceptual overlap with Pheromone C-01 (LLM multi-agent coordination) but MECHANISM is a "puppeteer" centralized orchestrator — NOT stigmergic / decentralized. Pheromone explicitly rejects centralized orchestration.
- Risk (non-lawyer): **UNLIKELY** — different mechanism (centralized orchestrator vs decentralized stigmergy). Monitor if Broadridge files continuations broadening to decentralized variants.

**WO2021084510A1 — "Executing artificial intelligence agents in an operating environment"**
- Source: [Google Patents](https://patents.google.com/patent/WO2021084510A1/en)
- Pre-2022; out of scope but noted as prior-art neighbor.
- Risk: NONE (filing date filter).

Other hits (cybersecurity AI engine orchestration US20240403428, etc.) are in narrow vertical application domains (cyber threat detection); unrelated mechanism. Risk: NONE.

### 2.2 Pheromone / stigmergic AI

Broad web+patent search for "stigmergic" OR "pheromone" + AI agent coordination 2023-2025 returned mostly ACADEMIC / research papers, not patents. Notable non-patent findings:
- [Phormica: Photochromic Pheromone Release and Detection System for Stigmergic Coordination in Robot Swarms](https://www.frontiersin.org/articles/10.3389/frobt.2020.591402/full) (2020 paper; not patent)
- [Automatic design of stigmergy-based behaviours for robot swarms (Nature Commun. Eng. 2024)](https://www.nature.com/articles/s44172-024-00175-7)
- [PooL: Pheromone-inspired Communication Framework (arxiv 2202.09722)](https://arxiv.org/pdf/2202.09722)
- [From Pheromones to Policies (arxiv 2509.20095)](https://arxiv.org/pdf/2509.20095)

**No granted patents or published applications on "stigmergic AI" / "pheromone LLM coordination" were surfaced in this search.** Most filings matching "pheromone" are biology/chemistry (IPC A01N / A61K) — out of scope per task boundaries.

Risk assessment: **NONE found for stigmergy applied to LLM coordination.** This is a strong positive signal for Pheromone's novelty on C-01 / C-04. Caveat: 18-month publication lag may hide 2025-2026 filings; UNVERIFIED for that window.

### 2.3 ACO + machine learning

ACO is 30+ years old; core ACO / MAX-MIN methods are public domain. Modern filings tend to be narrow applied variants (logistics, routing, drone path planning, edge computing).

Relevant hits:
- [IBM + Honeywell ACO supply chain partnership announcement (Apr 2024)](https://www.businessresearchinsights.com/market-reports/ant-colony-optimization-algorithm-market-115737) — commercial product, implicit IP filings likely but targeted at supply-chain logistics, not LLM agents.
- [Heterogeneous multi-agent task allocation based on GNN + ACO (2023 paper)](https://www.oaepublish.com/articles/ir.2023.33)
- [Improved ACO + DRL for AGV routing (MDPI 2024)](https://www.mdpi.com/2076-3417/14/16/7135)

No direct patent hits linking ACO + MAX-MIN to LLM agent allocation (Pheromone C-02). Applied-domain filings (logistics, AGV routing) do not read on LLM task allocation.

Risk: **NONE / UNLIKELY** on C-02 from this pass. Core ACO/MAX-MIN itself is prior art — Pheromone cannot patent it, but also cannot be blocked by it.

### 2.4 Multi-agent LLM routing / task allocation
(pending)

### 2.5 Shared memory / workspace for LLM agents
(pending)

### 2.6 MCP-compatible / agent-protocol patents
(pending)

## 3. Assignee-filtered scans

### 3.1 Microsoft
(pending)

### 3.2 Google / Alphabet
(pending)

### 3.3 Meta
(pending)

### 3.4 OpenAI
(pending)

### 3.5 Anthropic
(pending)

### 3.6 IBM
(pending)

### 3.7 NVIDIA
(pending)

### 3.8 Salesforce
(pending)

### 3.9 Oracle
(pending)

### 3.10 Amazon / AWS
(pending)

### 3.11 Adobe
(pending)

## 4. Risk matrix (one row per patent/application found)

| Filing # | Filer | Filing date | Status | Claim summary | Overlap with Pheromone claim IDs | Infringement risk | Recommended action |
|----------|-------|-------------|--------|---------------|----------------------------------|-------------------|--------------------|
| (TBD)    |       |             |        |               |                                  |                   |                    |

Risk options: NONE / UNLIKELY / POSSIBLE / HIGH.

## 5. Summary + escalation note
(pending)

## 6. Gaps and UNVERIFIED items
(pending)

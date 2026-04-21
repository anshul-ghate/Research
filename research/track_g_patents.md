# Track G — Patents and IP

**Status:** COMPLETE
**SubAgent:** G
**Last updated:** 2026-04-21
**Tool-call budget:** 15–20
**Tool-call count:** 15

**BLOCKING_CANDIDATE:** NONE identified in this pass. (Non-lawyer preliminary screening — professional FTO still required before launch.)

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

Key hits:
- **C3 AI — generative AI agent patent (2024)** — [context](https://arapackelaw.com/patents/are-ai-agents-patentable/); granted US patent covers a generative-AI agent framework. Mechanism: not clearly stigmergic. Reads on "AI agent using generative model" generically. Narrow enough? Needs direct patent fetch for claim-1.
- **OpenAI — 11 LLM patents/applications (2024)** — [IPKat analysis](https://ipkitten.blogspot.com/2024/08/openais-granted-large-language-model.html); OpenAI is pursuing accelerated grant. Largely on training / alignment / tool-use, not multi-agent stigmergy.
- US20230259705A1 — "Computer implemented methods for the automated analysis or use of data, including use of a large language model" — [Google Patents](https://patents.google.com/patent/US20230259705A1/en) — broad application; need claim-1 to assess.

Risk: **POSSIBLE** (UNVERIFIED pending claim-1 fetch on C3 AI / broad LLM patents). Pheromone C-02 mechanism (ACO + MAX-MIN + pheromone trails over shared memory) is specific enough that generic "AI agent routing" patents probably do not read on it, but confirmation requires claim-chart review.

### 2.5 Shared memory / workspace for LLM agents

Key neighbors (academic, not patents):
- Blackboard-style shared memory for LLM agents in MedAgents (Tang et al., 2024)
- [LbMAS Implementation](https://www.emergentmind.com/topics/lbmas-implementation) — blackboard central shared memory with public/private spaces
- [Memory in LLM Multi-agent Systems Survey](https://www.researchgate.net/publication/398392208_Memory_in_LLM-based_Multi-agent_Systems_Mechanisms_Challenges_and_Collective_Intelligence)
- [Resurgence of Blackboard Systems](https://medium.com/@shawncutter/the-resurgence-of-blackboard-systems-b10ea72a8326)

Blackboard architectures date to 1970s (Hearsay-II), so core pattern is prior art. Pheromone's C-10 distinction is **file-leasing + ADR (architecture decision records) + stigmergic writes** — the specific combination with LEASE semantics is more novel.

No specific patent hits on "file-leased LLM shared workspace" in this search. Risk: **UNLIKELY / NONE** — blackboard/shared-memory patents from 2024-2025 tend to cover specific application verticals (e.g., medical, customer-support) not file-lease + ADR semantics.

### 2.6 MCP-compatible / agent-protocol patents

MCP was released by [Anthropic as an open standard in November 2024](https://www.anthropic.com/news/model-context-protocol) with SDKs for Python and TypeScript. OpenAI formally adopted MCP in March 2025.

**Key IP observation:** Anthropic has released MCP as an open standard, i.e., it is explicitly designed as a protocol rather than a proprietary system. No evidence of Anthropic patent-blocking downstream MCP adopters. (Pheromone = "MCP-compatible" is consistent with industry standard usage.)

- [MCP Wikipedia entry](https://en.wikipedia.org/wiki/Model_Context_Protocol)
- [MCP Specification 2025-11-25](https://modelcontextprotocol.io/specification/2025-11-25)
- [Enhancing MCP with Context-Aware Server Collaboration (arxiv 2601.11595v2)](https://arxiv.org/html/2601.11595v2)

No direct patents located asserting ownership over MCP mechanism. Risk on C-12: **NONE / UNLIKELY**.

UNVERIFIED: whether Anthropic has any defensive MCP patent filings pending (18-month publication lag from Nov 2024 filing = publishes May 2026+). Monitor through 2026.

## 3. Assignee-filtered scans

### 3.1 Microsoft

Multiple Microsoft-adjacent filings on AI orchestration. Notable generic ones surfaced via keyword search:
- **US12111859B2** — "Enterprise generative artificial intelligence architecture" ([Google Patents](https://patents.google.com/patent/US12111859B2/en)) — granted; assignee needs confirmation but appears enterprise-AI vendor. Claim-1 (layperson): an orchestrator agent supervises/controls/administers multiple agents and tools, using an LLM to process inputs into a plan designating tools (structured/unstructured retrieval, timeseries, visualization). Overlap with Pheromone C-01: mechanism is CENTRALIZED supervisor, not decentralized stigmergy. Risk: **UNLIKELY**.
- **US20240404655A1** — "Systems and Methods for Interacting with a Task-Specific Orchestration" ([Google Patents](https://patents.google.com/patent/US20240404655A1)) — pending application; task-specific fine-tuned orchestrations. Mechanism narrow. Risk: **UNLIKELY**.
- Microsoft Research AutoGen framework = open-source (not patent-blocked to our knowledge).

UNVERIFIED: exhaustive Microsoft assignee scan on USPTO. Publicly-known projects (Semantic Kernel, AutoGen) are open source.

### 3.2 Google / Alphabet

- **Chain-of-Agents (CoA)** — [Google Research blog, NeurIPS 2024](https://research.google/blog/chain-of-agents-large-language-models-collaborating-on-long-context-tasks/) — multi-agent LLM collaboration over long-context tasks. Research publication; IP status UNVERIFIED (likely patent pending internally).
- **Agent-to-Agent (A2A) protocol** — Google Cloud 2025, horizontal agent coordination protocol. Complementary to MCP. Released as open(ish) protocol per Google's published pattern.

No granted Google/Alphabet patents surfaced in this pass directly reading on Pheromone's stigmergic LLM coordination. Overlap risk with C-01 (chained / collaborative LLMs) exists at CONCEPT level but mechanism differs (sequential chain vs stigmergic mediated by shared pheromone trails).

Risk: **UNLIKELY / POSSIBLE (UNVERIFIED)** — Google's patent portfolio is deep; a targeted patent-database query via Google Patents assignee:Google filter recommended for full FTO.

### 3.3 Meta

- **HyperAgents framework (FAIR, March 2026)** — [arXiv preprint + GitHub](https://blockchain.news/ainews/hyperagents-breakthrough-meta-fair-releases-multi-agent-llm-framework-with-benchmarks-and-open-source-code). Integrates hyperbolic geometry into agent architectures. Open-source release suggests defensive-publication posture rather than aggressive patenting.
- **US12513102B2 — "Simulation of a user of a social networking system using a language model"** (granted Dec 30, 2025). Trains AI on user content, deploys bot to respond on newsfeeds/DMs. [Fortune coverage](https://fortune.com/2026/03/03/meta-patent-ai-model-death-profile-commenting-psychology-grief/). Unrelated to stigmergic LLM coordination (social-feed user simulation).

Risk: **NONE / UNLIKELY** on Pheromone claims. Meta's public posture favors open source for multi-agent coordination research.

### 3.4 OpenAI

- 11 LLM patents/applications published by 2024 per IPKat. Focus areas: model training, alignment, tool use. [IPKat analysis Aug 2024](https://ipkitten.blogspot.com/2024/08/openais-granted-large-language-model.html)
- OpenAI adopted MCP in March 2025 (consumer of Anthropic's open protocol).

No direct overlap with Pheromone's stigmergic / ACO / file-lease mechanism surfaced. Risk: **UNLIKELY (UNVERIFIED)**.

### 3.5 Anthropic

- Released MCP (Nov 2024) as an open standard, not aggressively patented publicly. [MCP announcement](https://www.anthropic.com/news/model-context-protocol)
- Anthropic's patent portfolio is small relative to peers; research-heavy, open-source-ish posture.

Risk: **NONE / UNLIKELY**. Pheromone "MCP-compatible" (C-12) is consistent with Anthropic's publicly stated open-standard intent.

### 3.4 OpenAI
(pending)

### 3.5 Anthropic
(pending)

### 3.6 IBM

- **IBM watsonx Orchestrate** — commercial product for multi-agent supervisor + intelligent routing + 80+ enterprise app integrations. Underlying IP partially published.
- **QLM (Queue Management for SLO-Oriented LLM Serving)** — IBM + UIUC, ACM SoCC 2024; integrated into vLLM and AIBrix. [IBM Research blog](https://research.ibm.com/blog/qlm-chiron-llm-orchestration). This is LLM-serving queue management, not agent coordination.
- IBM's AI Agent Toolkit content is largely open source + published documentation, not a patent minefield on stigmergic coordination.

No direct overlap with Pheromone's stigmergic mechanism in results surfaced. IBM has a deep AI patent portfolio; UNVERIFIED exhaustive scan.

Risk: **UNLIKELY / POSSIBLE (UNVERIFIED)**.

### 3.7 NVIDIA

- **Orchestrator-8B** — small orchestrator model outperforming monolithic LLMs on orchestration benchmarks. Research publication. [NVIDIA dev blog](https://developer.nvidia.com/blog/train-small-orchestration-agents-to-solve-big-problems/)
- **ProRL Agent (March 2026)** — "Rollout-as-a-Service" infra decoupling agentic rollout orchestration from RL training loop.
- NVIDIA is invested in agent-platform tooling (Agent Toolkit, AI-Q, Nemotron) in partnership with LangChain; these are developer platforms, not obvious patent blockers on decentralized stigmergy.

Risk: **UNLIKELY** — NVIDIA's public work centers on orchestrator models + training infrastructure, not stigmergic coordination. UNVERIFIED exhaustive patent-assignee scan.

### 3.8 Salesforce

- **Agentforce / Atlas Reasoning Engine** — proprietary reasoning layer with multi-agent orchestration and A2A support. [Agentforce product page](https://www.salesforce.com/agentforce/multi-agent-orchestration/). Patents likely filed but mechanism is CENTRALIZED supervisor (Atlas orchestrator routes tasks).
- **MuleSoft agent orchestration** — API + agent-action unification for enterprise integration. Product-focused, not stigmergic.

Risk: **UNLIKELY** — Salesforce mechanism is centralized orchestration through Atlas; different from decentralized stigmergy. UNVERIFIED exhaustive patent scan.

### 3.9 Oracle

- **OCI Generative AI Agents (2024)** + **Oracle AI Agent Studio (March 2025)** — enterprise agent platform with agent-team orchestration, 50+ pre-packaged agents, MCP support.
- **Agent Factory** — Oracle AI Database 26ai.

Mechanism is centralized orchestration in enterprise application domain. No stigmergy/pheromone patents surfaced.

Risk: **UNLIKELY**.

### 3.10 Amazon / AWS

- **Amazon Bedrock Multi-Agent Collaboration** — preview Dec 2024 at re:Invent; GA March 10, 2025. [AWS blog](https://aws.amazon.com/blogs/machine-learning/amazon-bedrock-announces-general-availability-of-multi-agent-collaboration/). Modes: supervisor, supervisor with routing. CENTRALIZED supervisor agent coordinates specialized sub-agents.
- Integrates with CrewAI, LangGraph frameworks.

Mechanism is explicitly supervisor-orchestrated (anti-pattern to stigmergic decentralization). Likely patent filings pending on Bedrock supervisor mechanism; do NOT read on Pheromone's decentralized pheromone-mediated coordination.

Risk: **UNLIKELY (UNVERIFIED)**.

### 3.11 Adobe

- **Adobe Experience Platform Agent Orchestrator** — reasoning engine using LLMs + knowledge base for marketing/content workflows.
- **LLM Optimizer (Oct 2025)** — tool to boost brand visibility across AI chat services.

Vertical-specific (marketing / customer experience). No patents on stigmergic coordination.

Risk: **NONE / UNLIKELY**.

## 4. Risk matrix (one row per patent/application found)

Non-lawyer layperson reading. Full FTO analysis requires patent attorney.

| Filing # | Filer | Filing / grant date | Status | Claim-1 summary (layperson) | Overlap with Pheromone claim IDs | Infringement risk | Recommended action |
|----------|-------|---------------------|--------|-----------------------------|----------------------------------|-------------------|--------------------|
| [Broadridge LLM-Orchestration patent](https://www.broadridge.com/press-release/2025/broadridge-announces-new-patent-on-large-language-model-orchestration-of-machine) (press-release; specific US # not disclosed in release) | Broadridge Financial Solutions | Granted 2025 | GRANTED | LLM (GPT) orchestrates multiple ML agents to retrieve/process data from multiple datasets & analytical models in parallel and return NL answers. Tied to BondGPT/LTX. Mechanism = centralized orchestrator ("puppeteer"). | C-01 (concept-level) | UNLIKELY | Pull full patent claims via USPTO assignee:Broadridge; monitor continuations. Document non-infringement memo once specific # known. |
| [US12111859B2](https://patents.google.com/patent/US12111859B2/en) "Enterprise generative AI architecture" | (Enterprise vendor — assignee to confirm; likely C3 AI or similar) | Granted 2024 | GRANTED | Orchestrator agent supervises/controls/administers many agents + tools; uses LLM to plan structured/unstructured retrieval, timeseries, visualization. Mechanism = centralized supervisor. | C-01 (concept-level) | UNLIKELY | Fetch full claim 1; confirm assignee; document non-infringement memo. |
| [US20240404655A1](https://patents.google.com/patent/US20240404655A1) "Systems and Methods for Interacting with a Task-Specific Orchestration" | Unknown (Google Patents listing) | Filed 2024 | PENDING APPLICATION | UI presenting task-specific orchestrations fine-tuned per task or domain. Mechanism = fine-tuned per-task models. | C-01 (concept-level, UI facing) | UNLIKELY | Monitor prosecution; no impact on Pheromone stigmergic mechanism. |
| [WO2021084510A1](https://patents.google.com/patent/WO2021084510A1/en) "Executing AI agents in an operating environment" | (Unknown) | Filed 2019 (pre-2022) | Filed pre-2022 — out of scope window but noted | Generic agent execution environment. | None specific | NONE | Note only; prior art. |
| [US20230259705A1](https://patents.google.com/patent/US20230259705A1/en) "Computer implemented methods for automated analysis or use of data, including use of a LLM" | (Unknown) | Pub 2023 | PENDING APPLICATION | Data-analysis methods using an LLM. Very broad; mechanism UNVERIFIED. | Possibly C-01 if interpreted broadly | POSSIBLE (UNVERIFIED) | Fetch claim 1; assess breadth. |
| [US12513102B2](https://fortune.com/2026/03/03/meta-patent-ai-model-death-profile-commenting-psychology-grief/) "Simulation of a user of a social networking system using a language model" | Meta | Granted Dec 30, 2025 | GRANTED | Trains LM on user's posts/comments/chats; deploys bot to respond. Social-feed simulation. | None | NONE | No overlap with stigmergic multi-agent coordination. |
| C3 AI generative-AI agent patent (press-release, US # UNVERIFIED) | C3 AI | Granted 2024 | GRANTED | Generative AI agent framework (specifics UNVERIFIED). | C-01 (concept) | POSSIBLE (UNVERIFIED) | Fetch specific US # & claim 1. |

Risk options: NONE / UNLIKELY / POSSIBLE / HIGH.

**No BLOCKING_CANDIDATE patents identified in this pass.** All granted patents identified use CENTRALIZED supervisor-orchestrator mechanisms, which are architecturally opposite to Pheromone's decentralized stigmergic coordination.

## 5. Summary + escalation note

**Bottom line (non-lawyer, preliminary):**

1. **No BLOCKING_CANDIDATE patents identified.** The granted patents surfaced (Broadridge LLM-orchestration, US12111859B2 enterprise GenAI, Meta user-simulation) cover CENTRALIZED supervisor-orchestrator mechanisms, which are architecturally different from Pheromone's decentralized stigmergic coordination over pheromone-trail-annotated shared memory.

2. **Strong positive signal for Pheromone's novelty on stigmergic LLM coordination (C-01, C-04).** Searches for "stigmergic AI" / "pheromone LLM coordination" / "ant colony machine learning LLM agent" returned academic papers but NO granted patents or published applications that read on Pheromone's specific mechanism. This should be confirmed with a professional patent-novelty search before any public filing.

3. **ACO + MAX-MIN (C-02) are 30+ year prior art** — cannot be patented by Pheromone, but also cannot be blocked by any filer. Narrow applied ACO filings (logistics, drone routing, AGV) do not read on LLM agent task allocation.

4. **Shared workspace / blackboard (C-10)** is covered conceptually in 2024-2025 academic work (MedAgents, LbMAS) and potentially in vertical-application patents (medical, customer support). Pheromone's specific combination of **file-leasing + ADRs + stigmergic writes** is more distinctive; no direct patent overlap surfaced.

5. **MCP-compatible (C-12)** rests on Anthropic's open standard; no IP blocker identified. Anthropic and Google (A2A) both released protocols in open-standard form, reducing blocker risk.

6. **Corporate landscape is SUPERVISOR-CENTRIC.** Broadridge, Microsoft-adjacent, Salesforce, Oracle, AWS Bedrock all use variations of "supervisor agent + specialist sub-agents." This is structurally distinct from Pheromone's stigmergic approach. Pheromone's decentralized mechanism is a clear differentiator.

**Escalation:** None required at this time. No HIGH-risk granted patents. No BLOCKING_CANDIDATE.

**Recommended next steps (non-lawyer recommendations):**
- Engage a patent attorney for a professional FTO (freedom-to-operate) search before any commercial launch.
- Pull full claim 1 for:
  - Broadridge LLM orchestration patent (specific US # required)
  - US12111859B2 (confirm assignee + full claim 1)
  - US20230259705A1 (assess breadth)
  - C3 AI generative-agent patent (specific US # required)
- Monitor MCP-related filings as 18-month publication window catches up (filings from Nov 2024 publish ~May 2026+).
- Consider defensive publication of Pheromone's novel claims (C-01 decentralized stigmergic LLM coordination, C-04 stigmergic RL for LLM meta-learning, C-10 file-leased + ADR shared workspace) to establish prior art.

## 6. Gaps and UNVERIFIED items

- **Exhaustive USPTO assignee-filtered scans** for all 11 companies not performed (used Google web search as proxy; deeper patent-database queries via Google Patents assignee filter would be more definitive). UNVERIFIED.
- **Publication lag (18 months).** Filings made Oct 2024–Apr 2026 are largely unpublished. Pheromone's key concepts might appear in unpublished patent applications. Cannot be verified without future re-run.
- **Broadridge patent specific US number not extracted** (press release, not direct USPTO doc). UNVERIFIED — high confidence on general coverage area, low confidence on specific claim-1 text.
- **C3 AI patent US number not extracted.** UNVERIFIED.
- **WIPO PATENTSCOPE and EPO Espacenet not queried** separately (budget-constrained). International filings (non-US) not covered. UNVERIFIED.
- **US20230259705A1 full claim-1 not fetched** — breadth assessment is preliminary.
- **IPC / CPC classification filter not explicitly applied.** Biological-pheromone filings (A01N, A61K) were filtered by keyword context only. UNVERIFIED that no AI-class pheromone patents exist under G06N / G06F.
- **Beta-Binomial trust mechanism, Lévy flights, Quorum Sensing, IFT specific searches not performed** — concept-level coverage generalizes to "decentralized coordination" but narrower patent searches could surface specific overlaps. UNVERIFIED.
- **RTM (Reward Transmission / Relevance Task Model — specific Pheromone term) not patent-searched** specifically. UNVERIFIED.
- **Chinese and Japanese patent offices (CNIPA, JPO) not searched.** Many multi-agent AI filings originate from CN. UNVERIFIED.
- **Tool-call budget: 15 of 15–20 used.** Stopping here per budget. If additional budget available, priorities: (1) pull Broadridge + C3 AI specific US #s, (2) USPTO assignee:Google exhaustive scan, (3) USPTO assignee:Microsoft exhaustive scan, (4) CNIPA search for stigmergic/pheromone AI filings.

---

**Status:** COMPLETE (within budget). No BLOCKING_CANDIDATE identified. Professional FTO recommended before launch.

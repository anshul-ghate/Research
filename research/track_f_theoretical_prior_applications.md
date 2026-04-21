# Track F — Theoretical Concept Prior Applications to LLM Agents

**Status:** IN PROGRESS
**SubAgent:** F
**Last updated:** 2026-04-21
**Tool-call budget:** 25–30
**Tool-call count:** 1

---

## Methodology

For each of 16 theoretical concepts used by Pheromone, we identify the known prior applications to LLM / generative-AI multi-agent systems. Wave 1 context (SubAgents A, B, C, E, H) pre-loaded several concepts — for those we issue only one extra targeted query to find newer work. For concepts Track B did not cover (DAG/Kahn's, Circuit Breaker, eventual consistency, semantic similarity, optimistic concurrency, ReAct) we invest more heavily. Each citation requires authors + year + venue + URL. Foundational (pre-LLM) papers cited in a single line as lineage.

---

## Concept-by-concept genealogy

### 1. Ant Colony Optimization (ACO) — Pheromone C-02
**Foundational:** Dorigo 1992 PhD thesis; Dorigo, Maniezzo & Colorni 1996 IEEE SMC-B.
**LLM-era applications (Wave 1 cross-ref):**
- AMRO-S (arXiv 2603.12933) — ACO-style pheromone for multi-agent LLM routing
- ACO-ToT (arXiv 2501.19278) — Ant Colony on Tree-of-Thoughts reasoning
- LLM-Powered Swarms (arXiv 2506.14496)
- Frontiers MAS paper (arXiv 2503.03800)
**New:** _TBD_

### 2. Stigmergy — Pheromone C-01
**Foundational:** Grassé 1959; Theraulaz & Bonabeau 1999.
**LLM-era (Wave 1):** Rodriguez blog proof-of-concept; AgentNet (arXiv 2504.00587); Ledger-State Stigmergy (arXiv 2604.03997); AMRO-S (arXiv 2603.12933); GPTSwarm (arXiv 2402.16823, ICML 2024); MasRouter (arXiv 2502.11133, ACL 2025).
**New:** _TBD_

### 3. MAX-MIN Ant System — Pheromone C-02
**Foundational:** Stützle & Hoos 2000 "MAX-MIN Ant System", Future Generation Computer Systems 16(8):889-914 [ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0167739X00000431).
**LLM-era:**
- AMRO-S 2026 (arXiv [2603.12933](https://arxiv.org/abs/2603.12933)) — applies ACO pheromone bounds in spirit of MAX-MIN to LLM routing; closest match but does not formally invoke MAX-MIN bounds.
- No other LLM paper explicitly invokes MAX-MIN bounds τ_min/τ_max. **Gap verdict: VIRGIN for LLM-specific formal MAX-MIN application.**

### 4. Response Threshold Model — Pheromone C-03
**Foundational:** Bonabeau, Theraulaz & Deneubourg 1998.
**LLM-era (Wave 1):** Sci Reports 2025 s41598-025-21709-9; arXiv 2510.05174 (Riedl et al.).
**New:** _TBD_

### 5. Quorum Sensing — Pheromone C-07
**Foundational:** Seeley et al. 2012; Bixler/Sauter 2012 (IEEE 6393579); Trianni 2021.
**LLM-era (Wave 1):** NONE FOUND — confirmed gap by Track B.
**New:** _TBD_

### 6. Lévy flights — Pheromone C-06
**Foundational:** Viswanathan et al. 1999 Nature.
**LLM-era (Wave 1):** Liu 2020 Greedy-Lévy ACO; Springer LNCS 2024 ATLF.
**New:** _TBD_

### 7. Information Foraging Theory — Pheromone C-08
**Foundational:** Pirolli & Card 1999; Pirolli 2007.
**LLM-era (Wave 1):** Dhillon et al. arXiv 2406.04452 (LLM-IFT).
**New:** _TBD_

### 8. Bayesian Beta-Binomial trust — Pheromone C-09
**Foundational:** Jøsang & Ismail 2002 "Beta Reputation System"; Jøsang 2009 Advanced Features in Bayesian Reputation Systems [PDF](https://www.mn.uio.no/ifi/english/people/aca/josang/publications/jq2009-trustbus.pdf).
**LLM-era:**
- Yu et al. 2025 "To trust or not to trust: Attention-based Trust Management for LLM Multi-Agent Systems", arXiv [2506.02546](https://arxiv.org/html/2506.02546v2) — uses attention-based Trust Management Score (A-Trust) for message-level and agent-level trust; NOT explicitly beta-binomial but related.
- HiBayES (AISI 2025) — hierarchical Bayesian modeling for LLM evaluation; uses Reasoning Beta-Binomial GLM explicitly on agentic benchmarks like GAIA [blog](https://www.aisi.gov.uk/blog/hibayes-improving-llm-evaluation-with-hierarchical-bayesian-modelling).
- ECON / "From Debate to Equilibrium" (OpenReview 2025) — Bayesian Nash equilibrium for multi-LLM coordination [OpenReview](https://openreview.net/forum?id=RQwexjUCxm).
**Gap verdict: SPARSE — no paper applies classical Jøsang Beta reputation to LLM agent trust per se; Pheromone's direct Beta-Binomial usage for agent trust appears novel.**

### 9. DAG / Kahn's scheduling — architectural
**Foundational:** Kahn 1962 "Topological sorting of large networks", CACM 5(11).
**LLM-era:**
- DynTaskMAS (arXiv [2503.07675](https://arxiv.org/pdf/2503.07675), ICAPS 2025) — Dynamic Task Graph-driven Framework for Asynchronous and Parallel LLM-based Multi-Agent Systems; 21.3%–33.0% execution time reduction via DAG scheduling.
- Graph Harness / "From Agent Loops to Structured Graphs" arXiv [2604.11378](https://arxiv.org/html/2604.11378) — scheduler-theoretic framework for LLM agent execution, explicitly uses list scheduling + topological ordering + critical-path analysis.
- LLMCompiler (Kim et al. 2024 ICML) — DAG of tool calls, 3.6× speedup.
- LangGraph — production framework using DAG / state graph model for agent orchestration.
- GraphBus — live traversable networkx DAG for distributed multi-agent orchestration [site](https://graphbus.com/).
**Gap verdict: CROWDED — DAG orchestration is well-established in LLM agent systems. Pheromone must differentiate via the stigmergy+DAG combination, not DAG alone.**

### 10. Circuit Breaker pattern — architectural
**Foundational:** Nygard 2007 "Release It!" (Pragmatic Bookshelf).
**LLM-era:**
- Zou et al. 2024 "Improving Alignment and Robustness with Circuit Breakers", arXiv [2406.04313](https://arxiv.org/pdf/2406.04313) — but this is a model-internal representation "circuit breaker", NOT the Nygard pattern.
- Hannecke 2024 "Resilience Circuit Breakers for Agentic AI" [Medium](https://medium.com/@michael.hannecke/resilience-circuit-breakers-for-agentic-ai-cc7075101486) — industry blog applying Nygard-style breakers to agent systems, notes need for a DEGRADED state.
- NeuralTrust 2024 "Using Circuit Breakers to Secure the Next Generation of AI Agents" [blog](https://neuraltrust.ai/blog/circuit-breakers) — industry/security-focused.
- Portkey "Retries, fallbacks, and circuit breakers in LLM apps" [blog](https://portkey.ai/blog/retries-fallbacks-and-circuit-breakers-in-llm-apps/) — production LLM app engineering guide.
**Gap verdict: SPARSE academic / CROWDED industry — mostly blog/industry content, no formal academic paper applying Nygard breakers to multi-agent LLM coordination. Pheromone's academic formalization of circuit breakers for LLM agents appears novel-ish.**

### 11. Positive-negative feedback loops — C-01/C-07
**Foundational:** Camazine et al. 2001 "Self-Organization in Biological Systems"; Bonabeau/Dorigo/Theraulaz 1999 "Swarm Intelligence: From Natural to Artificial Systems".
**LLM-era:**
- "LLM-Assisted Iterative Evolution with Swarm Intelligence Toward SuperBrain", arXiv [2509.00510](https://arxiv.org/html/2509.00510v1) — explicitly describes swarm-style feedback loops for LLM collective reasoning.
- "Feedback Loops With Language Models Drive In-Context Reward Hacking", arXiv [2402.06627](https://arxiv.org/html/2402.06627v3) — studies positive-feedback failure modes in LLM systems.
- "Adapting LLM Agents with Universal Feedback in Communication", arXiv [2310.01444](https://arxiv.org/html/2310.01444v3).
- "A Multi-AI Agent System for Autonomous Optimization of Agentic AI Solutions via Iterative Refinement and LLM-Driven Feedback Loops", arXiv [2412.17149](https://arxiv.org/html/2412.17149v1).
- SwarmChat arXiv [2509.16920](https://arxiv.org/html/2509.16920) — ICSI 2025 LLM-based swarm coordination.
**Gap verdict: CROWDED — feedback loops widely discussed, but the explicit Camazine-style positive+negative stigmergic feedback analysis on LLM pheromone dynamics is rare. Pheromone's formal treatment is differentiated.**

### 12. Eventual consistency — C-10
**Foundational:** Vogels 2009 CACM "Eventually Consistent"; CRDTs Shapiro et al. 2011.
**LLM-era:**
- "Multi-Agent Memory from a Computer Architecture Perspective", arXiv [2603.10062](https://arxiv.org/html/2603.10062v1) — explicitly discusses eventual consistency as a critical open challenge in multi-agent LLM memory.
- "Memory in LLM-based Multi-agent Systems: Mechanisms, Challenges, and Collective" — TechRxiv [survey](https://www.techrxiv.org/users/1007269/articles/1367390/master/file/data/LLM_MAS_Memory_Survey_preprint_/LLM_MAS_Memory_Survey_preprint_.pdf?inline=true) — discusses eventual consistency tradeoffs for working vs. shared memory.
- Collaborative Memory arXiv [2505.18279](https://arxiv.org/html/2505.18279v1) — multi-user memory sharing in LLM agents with dynamic access control.
- Intrinsic Memory Agents arXiv [2508.08997](https://arxiv.org/abs/2508.08997).
**Gap verdict: SPARSE — the concept is recognized as an open challenge; few papers formalize it for LLM MAS. Pheromone's explicit eventual-consistency formalization is likely novel.**

### 13. Semantic similarity search — C-08
**Foundational:** Mikolov 2013 word2vec; Karpukhin 2020 DPR; Reimers 2019 Sentence-BERT.
**LLM-era:** _TBD_

### 14. Optimistic concurrency control — C-10
**Foundational:** Kung & Robinson 1981 ACM TODS "On Optimistic Methods for Concurrency Control".
**LLM-era:**
- SagaLLM VLDB 2025 [PDF](https://www.vldb.org/pvldb/vol18/p4874-chang.pdf) — "Context Management, Validation, and Transaction Guarantees for Multi-Agent LLM Planning" — explicitly handles transaction semantics / concurrency for LLM planning.
- "Handling Race Conditions in Multi-Agent Orchestration" MLMastery [blog](https://machinelearningmastery.com/handling-race-conditions-in-multi-agent-orchestration/) — industry framing of OCC for agents.
- agenthold (Glama MCP server) — "gives agents shared, versioned state with conflict detection built in" [site](https://glama.ai/mcp/servers/edobusy/agenthold).
**Gap verdict: SPARSE — one rigorous academic paper (SagaLLM) + industry tooling. Pheromone's OCC application is sparsely precedented.**

### 15. ReAct loop — general agent arch
**Foundational / seminal:** Yao et al. 2023 ICLR "ReAct: Synergizing Reasoning and Acting in Language Models", arXiv [2210.03629](https://arxiv.org/abs/2210.03629).
**LLM-era extensions:**
- Reflexion (Shinn et al. 2023, NeurIPS) — ReAct + verbal reinforcement learning.
- FireAct (Chen, Shu, Shareghi, Collier, Narasimhan, Yao 2023) — fine-tuning for ReAct agents.
- ReST meets ReAct (DeepMind 2023, OpenReview [7xknRLr7QE](https://openreview.net/pdf?id=7xknRLr7QE), arXiv [2312.10003](https://arxiv.org/html/2312.10003v1)) — self-improvement for multi-step ReAct reasoning.
- Voyager (Wang et al. 2023) — ReAct-derived embodied agent in Minecraft.
- LangChain / AutoGen / LangGraph — ubiquitous framework adoption of ReAct loop.
**Gap verdict: CROWDED — ReAct is the de facto agent loop. Pheromone's novelty must be in what complements the loop (pheromone trails, RTM, etc.), not the loop itself.**

### 16. Stigmergic Reinforcement Learning — Pheromone C-04
**Foundational:** Verbeeck & Nowé 2004; Monekosso & Remagnino Springer LNCS.
**LLM-era (Wave 1):** Xu et al. arXiv 1911.12504; arXiv 2105.03546; Springer PRICAI 2022; arXiv 2509.20095; S-MADRL 2025.
**New:** _TBD_

---

## Concept-by-concept gap analysis

| Concept | LLM application count | Gap verdict | Pheromone novelty potential |
|---------|----------------------|-------------|------------------------------|
| ACO | | | |
| Stigmergy | | | |
| MAX-MIN | | | |
| RTM | | | |
| Quorum Sensing | | | |
| Lévy | | | |
| IFT | | | |
| Bayesian Beta-Binomial | | | |
| DAG/Kahn | | | |
| Circuit Breaker | | | |
| Pos/neg feedback | | | |
| Eventual consistency | | | |
| Semantic similarity | | | |
| Optimistic concurrency | | | |
| ReAct | | | |
| Stigmergic RL | | | |

Gap verdict options: VIRGIN (0) / SPARSE (1–2) / CROWDED (3+).

## Citations ready for Related Work (BibTeX)

_TBD_

## Gaps and UNVERIFIED items

_TBD_

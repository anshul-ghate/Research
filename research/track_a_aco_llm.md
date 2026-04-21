# Track A — Direct ACO-for-LLM Multi-Agent Prior Art

**Status:** IN PROGRESS
**SubAgent:** A
**Last updated:** 2026-04-21
**Tool-call budget:** 25–30
**Tool-call count:** 4 (1 Write + 3 parallel WebSearch)

---

## 1. Methodology and query log

Executing broad → targeted strategy. Phase 1: 3 parallel broad queries. Phase 2: web_fetch known targets. Phase 3: narrow discovery queries on arXiv / Semantic Scholar / GitHub. Phase 4: matrix + severity + BibTeX.

Query log:
- [DONE] "ACO LLM agents" — top-relevance hits: AMRO-S (arXiv 2603.12933), LLM-Powered Swarms (arXiv 2506.14496), ACO-ToT (arXiv 2501.19278). Note: many results were red-herrings for "Autonomous Cyber Operations" (different ACO acronym).
- [DONE] "pheromone LLM coordination" — top hits: ACO-ToT (arXiv 2501.19278 "Pheromone-based Learning of Optimal Reasoning Paths"), PooL (arXiv 2202.09722 — MARL pre-LLM, possibly out of scope), AMRO-S again, LLM-Powered Swarms (arXiv 2506.14496), "Multi-agent systems powered by LLMs: swarm intelligence" (arXiv 2503.03800).
- [DONE] "ant colony multi-agent LLM" — top hits: AMRO-S (arXiv 2603.12933, OpenReview ojUhmgIS7o), arXiv 2503.03800 (Frontiers journal version), arXiv 2506.14496, Ants GPT NetLogo (modelingcommons.org #7548).

### Consolidated candidates discovered (broad phase)
1. **AMRO-S** — arXiv 2603.12933 — "Efficient and Interpretable Multi-Agent LLM Routing via Ant Colony Optimization" (OpenReview ojUhmgIS7o). Mentions pheromone specialists, 4.7x speedup, decomposes routing memory into task-specific pheromone specialists. DIRECTLY ON TOPIC.
2. **ACO-ToT** — arXiv 2501.19278 — "Pheromone-based Learning of Optimal Reasoning Paths." LLM "ants" traverse a centralized tree of thought, depositing virtual pheromones. DIRECTLY ON TOPIC (though applied to reasoning not agent orchestration).
3. **LLM-Powered Swarms: A New Frontier or a Conceptual Stretch?** — arXiv 2506.14496. Evaluates LLM-driven swarms vs classical ACO for latency/resource/accuracy. Review/critical piece.
4. **Multi-Agent Systems Powered by LLMs: Applications in Swarm Intelligence** — arXiv 2503.03800 (also Frontiers in AI 2025, PMC12135685). LLMs replace hard-coded programs in ant colony foraging / bird flocking simulations.
5. **PooL: Pheromone-inspired Communication Framework for Large Scale MARL** — arXiv 2202.09722. PRE-LLM MARL; flag as foundational / adjacent, check if Pheromone cites.
6. **"Why Multi-Agent Systems Don't Need Managers: Lessons from Ant Colonies"** — rodriguez.today blog post. Non-academic; B-tier, maybe useful as pop-sci reference.
7. **Ants GPT (NetLogo Modeling Commons #7548)** — Cristian Jimenez Romero. OpenAI LLM + rule-based ants. Simulation artifact, B-tier.
8. **AMRO** (without the -S) — earlier variant cited within AMRO-S results: "Ant colony inspired Multi-agent Routing Optimization" with function-based directed graph, pheromone-driven node update, adaptive pheromone decay.

## 2. Known-target papers (fetched in full)

### 2.1 AMRO-S (arXiv 2603.12933)

- **Title:** "Efficient and Interpretable Multi-Agent LLM Routing via Ant Colony Optimization"
- **Authors:** Xudong Wang, Chaoning Zhang, Jiaquan Zhang, Chenghao Li, Qigan Sun, Sung-Ho Bae, Peng Wang, Ning Xie, Jie Zou, Yang Yang, Hengtao Shen
- **Submission date:** 13 Mar 2026 (arXiv:2603.12933v1)
- **Venue:** IEEE Transactions on Artificial Intelligence (formatting/affiliation-inferred)
- **URL:** [arXiv](https://arxiv.org/abs/2603.12933), [HTML](https://arxiv.org/html/2603.12933v1), [OpenReview](https://openreview.net/forum?id=ojUhmgIS7o)

**Mechanism (summary from fetch):**
- Uses real pheromones: task-specific pheromone specialist matrices τᵗ (one per task type).
- Uses standard evaporation: (1−ρ)·τᵢⱼᵗ (classical ACO decay).
- Uses canonical ACO proportional rule: pᵢⱼ(q) = [τ]^α · [η]^β / Σ(...).
- **Uses DAG decomposition:** layered directed graph with N stages, edges only between adjacent layers.
- Has a "query-conditioned fusion" step that synthesizes pheromones across task specialists (interpretable as a shared workspace for pheromone signals — though not a file workspace).
- Stigmergic RL: **YES** — quality-gated asynchronous updates reinforce paths via pheromone signals.
- Adaptive colony composition: weak-YES — "dynamic routing weights adapt to mixed workloads; online evolution adjusts preferences" (adapts routing preferences, not the agent team).
- Code-review cycles: NO.
- MAX-MIN bounding: NOT mentioned (vanilla ACO, not MAX-MIN ACO).
- Architecture: Centralized pheromone specialists with quality gating (distinct from Pheromone's decentralized stigmergic coordination).

**Overlaps:** C-02 (ACO w/ decay, though no MAX-MIN), C-04 (stigmergic quality-gated updates — arguably stigmergic RL), partially C-05 (adaptive weights).
**Severity:** STRONG for C-02 + C-04 — AMRO-S clearly predates or matches Pheromone's ACO-for-LLM framing. Biggest competitor for the "first" framing of C-01.

**Crucial caveat for C-01:** AMRO-S is centralized (has a central fusion step), whereas Pheromone claims decentralized stigmergic coordination. AMRO-S is ROUTING between agents, not ORCHESTRATION without a central planner. This weakens direct competition with C-01 but still destroys any "first ACO-for-LLM" framing.

### 2.2 GPTSwarm (Zhuge et al. 2024)

- **Title:** "Language Agents as Optimizable Graphs" (aka GPTSwarm)
- **Authors:** Mingchen Zhuge, Wenyi Wang, Louis Kirsch, Francesco Faccio, Dmitrii Khizbullin, Jürgen Schmidhuber
- **Submission date:** 26 Feb 2024 (v1); 22 Aug 2024 (v3)
- **Venue:** ICML 2024 (Forty-first International Conference on Machine Learning)
- **URL:** [arXiv 2402.16823](https://arxiv.org/abs/2402.16823), [project page](https://gptswarm.org/)

**Mechanism:**
- Represents LLM-based agents as computational graphs with nodes processing data and edges as information flow.
- Includes automatic graph optimizers refining prompts and connectivity.
- **No pheromones, no ACO, no stigmergy, no decay** — despite the name "GPTSwarm."
- Central orchestrator using graph-based coordination, NOT decentralized stigmergic.
- No MAX-MIN bounds, no shared file workspace, no code review cycles.

**Overlaps:** C-05 (team composition via graph edges, loosely). Zero overlap on ACO/stigmergic claims.
**Severity:** NAME-ONLY on "swarm"; WEAK on any ACO competition. Its relevance is competitive-framing — any "multi-agent LLM coordination" paper must differentiate from GPTSwarm.

### 2.3 Adornetto et al. 2025

- **Candidate title** (from search): "Generative agents in agent-based modeling: overview, validation, and emerging challenges"
- **Venue:** IEEE Transactions on Artificial Intelligence (2025)
- **URL:** not directly retrieved; not available in search results. FLAGGED UNVERIFIED.
- **Claimed topic:** overview/validation of generative agents in ABM (touches on ant colonies as example ABMs).
- **Mechanism:** survey/overview; no unique ACO-for-LLM mechanism proposed.

**Overlaps:** Only C-01 framing (cites ACO + LLM literature). Not a competing mechanism.
**Severity:** WEAK (likely a survey/overview, not competing implementation). Flagged UNVERIFIED — need primary source confirmation.

### 2.4 MasRouter (Yue et al.)

- **Title:** "MasRouter: Learning to Route LLMs for Multi-Agent Systems"
- **Authors:** Yanwei Yue, Guibin Zhang, Boyang Liu, Guancheng Wan, Kun Wang, Dawei Cheng, Yiyan Qi
- **Submission date:** arXiv 2502.11133 (Feb 2025)
- **Venue:** ACL 2025 (Proceedings of the 63rd Annual Meeting of the ACL, Long papers)
- **URL:** [arXiv](https://arxiv.org/abs/2502.11133), [ACL Anthology](https://aclanthology.org/2025.acl-long.757/), [GitHub](https://github.com/yanweiyue/masrouter)

**Mechanism:**
- Frames Multi-Agent System Routing (MASR) as a unified problem combining collaboration mode determination, role allocation, and LLM routing.
- Uses a cascaded controller network (learned router), NOT ACO / pheromones / stigmergy.
- Performance: +1.8 on MBPP, −52% overhead on HumanEval, plug-and-play with mainstream MAS frameworks.
- No pheromones, no decay, no MAX-MIN, no stigmergic RL.

**Overlaps:** C-01 (multi-agent LLM routing — but central router), C-05 (dynamic role allocation — cascaded controller decides roles).
**Severity:** PARTIAL on C-05 (MasRouter adapts team composition via learned router; Pheromone adapts via stigmergic signals). NOT competitive on C-02/C-04. This is a key baseline — Pheromone must distinguish its ACO-based allocation from MasRouter's learned cascaded-controller allocation.

### 2.5 AgentRouter (Zhang et al.)

- **Title:** "AgentRouter: A Knowledge-Graph-Guided LLM Router for Collaborative Multi-Agent Question Answering"
- **Authors:** Zheyuan Zhang + 8 others (full list pending)
- **Submission date:** arXiv 2510.05445 (Oct 2025)
- **Venue:** arXiv preprint (as of fetch)
- **URL:** [arXiv](https://arxiv.org/abs/2510.05445), [PDF](https://arxiv.org/pdf/2510.05445)

**Mechanism:**
- Converts QA instances into a knowledge graph jointly encoding queries, contextual entities, and agents.
- Trains a heterogeneous GNN (RouterGNN) to predict task-dependent distribution over agents.
- Supervised by empirical performance signals via KL divergence against agent performance.
- No pheromones, no ACO, no decay, no stigmergy. Different paradigm (GNN-based router).

**Overlaps:** C-01 and C-05 (routing/allocating across agents) — but via GNN rather than ACO.
**Severity:** PARTIAL on C-05 (another learned router). NOT competitive on C-02/C-04. Like MasRouter, this is a routing-baseline Pheromone must differentiate against.

## 3. Additional papers discovered via broad search

### 3.1 ACO-ToT — "Pheromone-based Learning of Optimal Reasoning Paths"
- **Authors:** Anirudh Chari, Aditya Tiwari, Richard Lian, Suraj Reddy, Brian Zhou
- **Submission date:** Jan 31, 2025
- **Venue:** arXiv cs.CL (arXiv:2501.19278)
- **URL:** [arXiv](https://arxiv.org/abs/2501.19278)

**Mechanism:** ACO combined with LLMs to discover optimal reasoning paths. Distinctly fine-tuned LLM "ants" traverse a centralized tree of thought, depositing pheromones proportional to reasoning quality. Benchmarks: GSM8K, ARC-Challenge, MATH.

- Pheromones: YES (core).
- ACO formula: YES.
- Decay: unclear from abstract.
- MAX-MIN: not mentioned.
- Shared workspace: effectively YES (centralized tree of thought).
- Code review cycles: NO.
- Architecture: CENTRALIZED.
- Scope: REASONING PATHS, not agent orchestration.

**Overlaps:** C-02 (ACO-for-LLM). Weakly C-04 (reinforcing productive paths via pheromones).
**Severity:** STRONG on C-02 framing (directly does ACO + LLM, published Jan 2025); but WEAK on C-01/C-05/C-10/C-11 (different problem — reasoning path selection, not multi-agent orchestration).

### 3.2 LLM-Powered Swarms — "A New Frontier or a Conceptual Stretch?"
- arXiv 2506.14496 (June 2025)
- [URL](https://arxiv.org/abs/2506.14496)
- Review/critique comparing classical ACO vs LLM-driven swarms on latency/resource/accuracy. NOT a new mechanism. Classical ACO took 14.03s vs LLM ACO 135.76s, but LLM achieved stronger pheromone levels on optimal paths by step 50.
- **Overlaps:** None mechanistically; acts as a LITERATURE MAP (must cite as it evaluates the exact design space).
- **Severity:** WEAK. Useful as a survey/critique cite.

### 3.3 Multi-Agent Systems Powered by LLMs: Applications in Swarm Intelligence
- arXiv 2503.03800 / [Frontiers in AI 2025](https://www.frontiersin.org/journals/artificial-intelligence/articles/10.3389/frai.2025.1593017/full) / PMC12135685
- Examines replacing hard-coded programs of ABM agents with LLM-driven prompts, in ant foraging and bird flocking.
- LLM-guided ants gather food comparable to classical NetLogo ants when instructions are meticulously designed.
- **Overlaps:** C-01 weak framing. NOT ACO-based orchestration; uses LLMs as agent controllers inside classical swarm simulations.
- **Severity:** NAME-ONLY to WEAK.

### 3.4 PooL — Pheromone-inspired Communication for Large-Scale MARL
- arXiv 2202.09722 (Feb 2022)
- [URL](https://arxiv.org/abs/2202.09722)
- Pheromone-inspired MARL communication framework. **Pre-LLM.** Does not use LLMs at all.
- **Overlaps:** None direct (no LLM), but conceptual predecessor for stigmergic MARL. Note whether Pheromone cites.
- **Severity:** OUT OF SCOPE (pre-LLM) but cite as foundational if Pheromone mentions stigmergic MARL lineage.

### 3.5 Ants GPT — NetLogo Modeling Commons model #7548
- Cristian Jimenez Romero. OpenAI LLM + rule-based ants combined in NetLogo.
- [URL](https://www.modelingcommons.org/browse/one_model/7548)
- **Overlaps:** NAME-ONLY. Toy simulation, not an orchestration framework.
- **Severity:** NAME-ONLY.

### 3.6 "Why Multi-Agent Systems Don't Need Managers: Lessons from Ant Colonies" — Roland Rodriguez (blog)
- [URL](https://www.rodriguez.today/articles/emergent-coordination-without-managers)
- Non-academic advocacy blog; relevant as a discourse touchstone for C-01 ("no central orchestrator").
- **Severity:** NAME-ONLY (pop-sci; not a mechanism).

### 3.7 RCR-Router (arXiv 2508.04903) — "Efficient Role-Aware Context Routing for Multi-Agent LLM"
- Mentioned in search results alongside MasRouter/AgentRouter. Appears to be another learned router. Not ACO.
- **Severity:** PARTIAL on C-05 (routing baseline, non-ACO).

### 3.8 Router-R1 (arXiv 2506.09033)
- "Teaching LLMs Multi-Round Routing and Aggregation via Reinforcement Learning" — RL-based router.
- **Severity:** PARTIAL on C-05; not ACO.

### 3.9 "Orchestrating Intelligence: Confidence-Aware Routing..." (arXiv 2601.04861)
- Confidence-aware routing across multi-scale models. Not ACO.
- **Severity:** PARTIAL on C-05; not ACO.

## 4. Code repositories and shipped products

Searches for GitHub repositories with ACO + LLM + multi-agent orchestration turned up the following. None are shipped products in a direct competitive sense; the GitHub ACO repos are classical pre-LLM implementations.

- **[yanweiyue/masrouter](https://github.com/yanweiyue/masrouter)** — MasRouter reference implementation (GNN-based router, not ACO). B-tier relevance.
- **[Awesome-LLM-Agent-Optimization-Papers](https://github.com/YoungDubbyDu/LLM-Agent-Optimization)** — reading list; useful as survey landing.
- **AMRO-S** — paper ships code (see arXiv 2603.12933); authoritative ACO-for-LLM reference implementation.
- Classical ACO libraries (jacof, Formigueiro, pjmattingly/ant-colony-optimization, Akavall/AntColonyOptimization) — pre-LLM, out of scope.
- **Ants GPT (NetLogo #7548)** — toy LLM + ants simulation, not a coordination framework.

No evidence of shipped SaaS products or VC-backed frameworks named "Pheromone" or similar in the ACO-for-LLM-orchestration space besides the academic artifacts above.

## 5. Competitor matrix (one row per entity)

| Title | Authors | Venue | Date | URL | Mechanism summary | Claims overlapped | Severity | What Pheromone does that this doesn't | Citation needed |
|-------|---------|-------|------|-----|-------------------|-------------------|----------|--------------------------------------|-----------------|

## 6. Severity analysis per claim

### 6.1 C-01 (no central orchestrator — first formal adaptation for LLM)
[pending]

### 6.2 C-02 (ACO with MAX-MIN)
[pending]

### 6.3 C-04 (Stigmergic RL — novel)
[pending]

### 6.4 C-05 (adaptive colony composition — novel)
[pending]

### 6.5 C-10 (shared workspace + leasing + ADRs)
[pending]

### 6.6 C-11 (review cycles built-in)
[pending]

## 7. Proposed BibTeX citations for arXiv Related Work

[pending]

## 8. Gaps and flagged UNVERIFIED items

[pending]

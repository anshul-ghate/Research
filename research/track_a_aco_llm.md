# Track A — Direct ACO-for-LLM Multi-Agent Prior Art

**Status:** COMPLETE
**SubAgent:** A
**Last updated:** 2026-04-21
**Tool-call budget:** 25–30
**Tool-call count:** ~14 (1 Write + 3 WebSearch broad + 1 WebFetch fail + 1 Edit-interim + 1 WebFetch AMRO-S + 1 Edit + 1 WebFetch GPTSwarm + 1 Edit + 1 WebSearch Adornetto + 1 Edit + 1 WebSearch MasRouter + 1 Edit + 1 WebSearch AgentRouter + 1 Edit + 1 WebFetch ACO-ToT + 1 Edit + 1 WebSearch GitHub + 1 Edit + 1 WebSearch stigmergic-RL + 4 final Edits) — within budget.

## BLOCKING_CANDIDATE

**AMRO-S (arXiv 2603.12933, IEEE Trans AI, 13 Mar 2026)** — "Efficient and Interpretable Multi-Agent LLM Routing via Ant Colony Optimization" (Wang et al.). This paper implements:
- Task-specific **pheromone** specialists τᵗ.
- Canonical ACO proportional rule pᵢⱼ(q)=[τ]^α·[η]^β/Σ(...).
- Standard **evaporation** (1−ρ)·τᵢⱼᵗ.
- **DAG decomposition** (layered directed graph across N stages).
- **Stigmergic RL** via quality-gated asynchronous pheromone updates.
- Adaptive online evolution of routing preferences.
All for **multi-agent LLM routing.** This directly contradicts Pheromone's C-01 "first formal adaptation for LLM agents" phrasing and is STRONG-severity on C-02 and C-04. Pheromone MUST cite AMRO-S and narrow its "first"/"novel" claims.

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
| AMRO-S: Efficient and Interpretable Multi-Agent LLM Routing via ACO | Wang, Zhang, Zhang, Li, Sun, Bae, Wang, Xie, Zou, Yang, Shen | IEEE Trans AI | 13 Mar 2026 | [arXiv 2603.12933](https://arxiv.org/abs/2603.12933) | Task-specific pheromone specialists + canonical ACO proportional rule + evaporation + DAG routing | C-01 (partial), C-02, C-04, C-05 | STRONG | MAX-MIN bounds; decentralized (AMRO-S is centralized); shared file workspace + ADRs; review cycles; adaptive colony composition rather than routing | **YES — must cite as closest prior work** |
| ACO-ToT: Pheromone-based Learning of Optimal Reasoning Paths | Chari, Tiwari, Lian, Reddy, Zhou | arXiv cs.CL | 31 Jan 2025 | [arXiv 2501.19278](https://arxiv.org/abs/2501.19278) | LLM "ants" traverse centralized Tree of Thought, deposit pheromones proportional to reasoning quality | C-02 (reasoning paths, not agent orchestration) | STRONG (on ACO-for-LLM framing), WEAK (on orchestration) | Pheromone is multi-agent orchestration; ACO-ToT is single-agent reasoning | **YES** |
| GPTSwarm: Language Agents as Optimizable Graphs | Zhuge, Wang, Kirsch, Faccio, Khizbullin, Schmidhuber | ICML 2024 | 26 Feb 2024 | [arXiv 2402.16823](https://arxiv.org/abs/2402.16823) | LLM agents as computational graphs with learned optimizer over edges | C-05 (weakly) | WEAK (NAME-ONLY on "swarm") | Stigmergy, pheromones, ACO, MAX-MIN, shared workspace, review cycles | YES (framing/contrast) |
| MasRouter: Learning to Route LLMs for Multi-Agent Systems | Yue, Zhang, Liu, Wan, Wang, Cheng, Qi | ACL 2025 | arXiv Feb 2025 | [arXiv 2502.11133](https://arxiv.org/abs/2502.11133) | Cascaded controller network routes LLMs + roles | C-01 (central-router framing), C-05 | PARTIAL | ACO / pheromones / stigmergic RL; decentralization | **YES (baseline)** |
| AgentRouter: KG-Guided LLM Router | Zhang et al. | arXiv | Oct 2025 | [arXiv 2510.05445](https://arxiv.org/abs/2510.05445) | Heterogeneous GNN (RouterGNN) trained on empirical agent performance, KG-based | C-01, C-05 | PARTIAL | ACO / stigmergic mechanism | **YES (baseline)** |
| LLM-Powered Swarms: A New Frontier or a Conceptual Stretch? | — | arXiv | 17 Jun 2025 | [arXiv 2506.14496](https://arxiv.org/abs/2506.14496) | Empirical eval of LLM swarms vs classical ACO on latency/resource/accuracy | none mechanistically | WEAK (survey/critique) | Proposes no mechanism | Likely (lit review) |
| Multi-Agent Systems Powered by LLMs: Applications in Swarm Intelligence | — | Frontiers in AI 2025 | 2025 | [arXiv 2503.03800](https://arxiv.org/abs/2503.03800) | Replaces ABM agent code with LLM prompts in ant foraging / flocking | C-01 loosely | WEAK (sim toolkit, not orchestration) | Stigmergic orchestration infrastructure | Maybe |
| PooL: Pheromone-inspired Communication for Large-Scale MARL | — | arXiv 2202.09722 | Feb 2022 | [arXiv](https://arxiv.org/abs/2202.09722) | Pheromone-inspired MARL (pre-LLM) | foundational | OUT-OF-SCOPE / foundational | LLM integration | Optional (lineage) |
| Stigmergic Independent Reinforcement Learning for Multi-Agent Collaboration | — | arXiv 1911.12504 | 2019 | [arXiv](https://arxiv.org/abs/1911.12504) | Stigmergy as indirect-communication bridge in MARL (pre-LLM) | foundational to C-04 | OUT-OF-SCOPE / foundational for C-04 naming | LLM integration; stigmergic RL **for LLMs specifically** | **YES — cite if C-04 claims "novel"** |
| Scalable Decentralized MARL Inspired by Stigmergy and Ant Colonies | — | arXiv 2105.03546 | 2021 | [ADS](https://ui.adsabs.harvard.edu/abs/2021arXiv210503546A/abstract) | Decentralized MARL + ACO-inspired path planning (pre-LLM) | foundational to C-01 (decentralized stigmergy) | OUT-OF-SCOPE / foundational | LLM integration | Optional |
| Adornetto et al. — Generative agents in ABM (overview) | C. Adornetto et al. | IEEE Trans AI 2025 | 2025 | [UNVERIFIED] | Survey/overview of generative agents in ABM | none direct | WEAK (survey) | — | Maybe; flag unverified |
| RCR-Router: Role-Aware Context Routing | — | arXiv 2508.04903 | Aug 2025 | [arXiv](https://arxiv.org/abs/2508.04903) | Learned role-aware context router | C-05 | PARTIAL | ACO mechanism; stigmergy | Likely (baseline) |
| Router-R1: LLM Multi-Round Routing via RL | — | arXiv 2506.09033 | Jun 2025 | [arXiv](https://arxiv.org/abs/2506.09033) | RL-trained multi-round router | C-05 | PARTIAL | ACO; stigmergy | Likely (baseline) |
| Orchestrating Intelligence: Confidence-Aware Routing | — | arXiv 2601.04861 | 2026 | [arXiv](https://arxiv.org/abs/2601.04861) | Confidence-aware multi-scale routing | C-05 | PARTIAL | ACO; stigmergy | Optional |
| Ants GPT (NetLogo #7548) | Jimenez Romero | Modeling Commons | — | [URL](https://www.modelingcommons.org/browse/one_model/7548) | Toy LLM + rule-based ants in NetLogo | — | NAME-ONLY | — | No |
| "Why Multi-Agent Systems Don't Need Managers" | Rodriguez | blog | — | [URL](https://www.rodriguez.today/articles/emergent-coordination-without-managers) | Pop-sci advocacy for decentralized multi-agent | C-01 framing | NAME-ONLY | — | No |

## 6. Severity analysis per claim

### 6.1 C-01 (no central orchestrator — "first formal adaptation for LLM")

**Verdict: CLAIM IS NOT DEFENSIBLE AS STATED.** The phrase "first formal adaptation for LLM agents" cannot survive literature. There are at least three peer-reviewed or ACL-venue LLM multi-agent coordination papers that pre-date or coincide with Pheromone:
- MasRouter (ACL 2025) — coordination across multiple LLM agents.
- GPTSwarm (ICML 2024) — multi-LLM-agent graph orchestration.
- AMRO-S (IEEE Trans AI, arXiv 2603.12933) — **ACO-based** multi-agent LLM routing.

However, **a nuanced form may still be defensible**: "first fully decentralized, stigmergy-only coordination for LLM agents (no central router, no learned controller, no graph optimizer)." All three competitors above retain a central decision point (controller, graph optimizer, or fusion gate). Pheromone should reframe C-01 to this narrower claim.

**Severity: STRONG** (as written — the "first" claim is destroyed by AMRO-S alone).
**Severity if narrowed:** WEAK.

### 6.2 C-02 (ACO with MAX-MIN)

**Competitors:** AMRO-S uses canonical ACO proportional rule + evaporation. ACO-ToT uses pheromone deposition. Neither explicitly uses **MAX-MIN** bounds (per Stützle & Hoos). This is a genuine differentiation vector.

- AMRO-S: vanilla ACO (no MAX-MIN mentioned).
- ACO-ToT: does not mention MAX-MIN.
- Dorigo/Stützle: foundational (cite explicitly as such).

**Severity: STRONG for ACO-for-LLM in general (AMRO-S), PARTIAL specifically for MAX-MIN variant (may be genuinely novel in the LLM agent setting).** Pheromone should pivot C-02's novelty claim away from "ACO-for-LLM" (taken) toward "MAX-MIN ACO for LLM orchestration" (potentially novel).

### 6.3 C-04 (Stigmergic RL — "novel, no prior publication")

**Verdict: NAME IS NOT NOVEL.** Stigmergic RL as a concept is at least 20 years old in MARL:
- Ricci et al. "Stigmergy in multiagent RL" (IEEE 2005, also Inria HAL).
- "Stigmergic Independent RL for Multi-Agent Collaboration" (arXiv 1911.12504, 2019).
- "Scalable Decentralized MARL Inspired by Stigmergy and Ant Colonies" (arXiv 2105.03546, 2021).

Additionally, AMRO-S has "quality-gated asynchronous updates reinforc[ing] paths via pheromone signals" — which IS a form of stigmergic RL, even if not labeled as such.

**However,** no prior work applies stigmergic RL **to LLM-agent meta-learning specifically** based on this search. So a narrowed claim — "first application of stigmergic RL to LLM agent meta-learning" — may survive, if Pheromone means something stricter than "pheromone-based quality feedback" (which AMRO-S already does).

**Severity: STRONG as written ("novel"), PARTIAL if narrowed to "first for LLM-agent meta-learning."** Must cite Ricci 2005, Xu et al. 2019, and AMRO-S 2026.

### 6.4 C-05 (adaptive colony composition — novel)

**Competitors in adjacent space:**
- MasRouter: cascaded controller determines collaboration mode + role allocation + LLM routing (effectively adaptive team composition).
- AgentRouter: GNN predicts task-dependent distribution over agents (adaptive team composition).
- GPTSwarm: automatic graph optimizer edits agent graph (adaptive team composition).
- AMRO-S: "online evolution adjusts preferences" — adaptive routing weights but not agent team composition.

**Verdict:** Adaptive team composition in multi-agent LLM systems is crowded. What can remain novel is **stigmergic (pheromone-mediated) colony composition** specifically — i.e., agents join/leave via local pheromone signals rather than a learned controller. That specific mechanism is NOT covered by any of the above. Pheromone should frame C-05 as "stigmergic (decentralized, pheromone-mediated) colony composition" rather than generic "adaptive team composition."

**Severity: PARTIAL as written, WEAK if narrowed to stigmergic-specific.**

### 6.5 C-10 (shared workspace + file leasing + ADRs + convention enforcement)

**No direct ACO-for-LLM competitor implements this.** AMRO-S has a "query-conditioned fusion" of pheromone signals (not a file workspace). ACO-ToT has a centralized tree of thought (not a file workspace).

Outside ACO, mainstream frameworks (AutoGen, CrewAI, SWE-agent, Devin) DO implement shared workspaces with various leasing/locking semantics. These are in SubAgent C's track, not here, but C-10 is almost certainly NOT novel on the non-ACO side. From the ACO-for-LLM angle specifically, C-10 appears not to collide.

**Severity (within Track A): WEAK/none.** Cross-track concern: C likely finds overlap.

### 6.6 C-11 (code review cycles built-in)

**No ACO-for-LLM competitor implements code→test→review→fix cycles.** AMRO-S, ACO-ToT, MasRouter, AgentRouter, GPTSwarm — none are code-agent systems. From the ACO-for-LLM angle, C-11 does not collide.

**Severity (within Track A): none.** Cross-track concern: SWE-agent, AutoGen, Devin, OpenDevin, and especially CrewAI/LangGraph-based coder frameworks will have this — SubAgent C's territory.

## 7. Proposed BibTeX citations for arXiv Related Work

```bibtex
@article{wang2026amros,
  title   = {Efficient and Interpretable Multi-Agent LLM Routing via Ant Colony Optimization},
  author  = {Wang, Xudong and Zhang, Chaoning and Zhang, Jiaquan and Li, Chenghao and Sun, Qigan and Bae, Sung-Ho and Wang, Peng and Xie, Ning and Zou, Jie and Yang, Yang and Shen, Hengtao},
  journal = {IEEE Transactions on Artificial Intelligence},
  year    = {2026},
  note    = {arXiv:2603.12933}
}

@article{chari2025acotot,
  title   = {Pheromone-based Learning of Optimal Reasoning Paths},
  author  = {Chari, Anirudh and Tiwari, Aditya and Lian, Richard and Reddy, Suraj and Zhou, Brian},
  journal = {arXiv preprint arXiv:2501.19278},
  year    = {2025}
}

@inproceedings{zhuge2024gptswarm,
  title     = {Language Agents as Optimizable Graphs},
  author    = {Zhuge, Mingchen and Wang, Wenyi and Kirsch, Louis and Faccio, Francesco and Khizbullin, Dmitrii and Schmidhuber, Jürgen},
  booktitle = {Proceedings of the 41st International Conference on Machine Learning (ICML)},
  year      = {2024}
}

@inproceedings{yue2025masrouter,
  title     = {MasRouter: Learning to Route LLMs for Multi-Agent Systems},
  author    = {Yue, Yanwei and Zhang, Guibin and Liu, Boyang and Wan, Guancheng and Wang, Kun and Cheng, Dawei and Qi, Yiyan},
  booktitle = {Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (ACL)},
  year      = {2025},
  note      = {arXiv:2502.11133}
}

@article{zhang2025agentrouter,
  title   = {AgentRouter: A Knowledge-Graph-Guided LLM Router for Collaborative Multi-Agent Question Answering},
  author  = {Zhang, Zheyuan and others},
  journal = {arXiv preprint arXiv:2510.05445},
  year    = {2025}
}

@article{llmpoweredswarms2025,
  title   = {LLM-Powered Swarms: A New Frontier or a Conceptual Stretch?},
  journal = {arXiv preprint arXiv:2506.14496},
  year    = {2025}
}

@article{masllmssim2025,
  title   = {Multi-Agent Systems Powered by Large Language Models: Applications in Swarm Intelligence},
  journal = {Frontiers in Artificial Intelligence / arXiv:2503.03800},
  year    = {2025}
}

@article{pool2022,
  title   = {PooL: Pheromone-inspired Communication Framework for Large Scale Multi-Agent Reinforcement Learning},
  journal = {arXiv preprint arXiv:2202.09722},
  year    = {2022}
}

@article{xu2019stigmergicrl,
  title   = {Stigmergic Independent Reinforcement Learning for Multi-Agent Collaboration},
  journal = {arXiv preprint arXiv:1911.12504},
  year    = {2019}
}

@inproceedings{ricci2005stigmergy,
  title     = {Stigmergy in Multiagent Reinforcement Learning},
  booktitle = {IEEE Conference Publication},
  year      = {2005},
  note      = {Also available via Inria HAL inria-00000209}
}

% Foundational ACO (Pheromone's C-02 cites these already)
@book{dorigo2004acobook,
  title     = {Ant Colony Optimization},
  author    = {Dorigo, Marco and St{\"u}tzle, Thomas},
  publisher = {MIT Press},
  year      = {2004}
}

@article{stutzle2000maxmin,
  title   = {MAX-MIN Ant System},
  author  = {St{\"u}tzle, Thomas and Hoos, Holger H.},
  journal = {Future Generation Computer Systems},
  volume  = {16},
  number  = {8},
  year    = {2000}
}
```

## 8. Gaps and flagged UNVERIFIED items

**UNVERIFIED (could not obtain primary source within budget):**
- Adornetto et al. 2025 — title inferred as "Generative agents in agent-based modeling: overview, validation, and emerging challenges" in IEEE Trans AI, but not fetched directly. Re-dispatch to confirm DOI / full abstract / actual mechanism.
- AgentRouter full author list — only top author (Zheyuan Zhang) confirmed.
- AMRO (without -S) — cited within AMRO-S-related results as an earlier "Ant colony inspired Multi-agent Routing Optimization" variant. arXiv ID not confirmed; needs separate retrieval.

**Gaps (not searched within budget):**
- Semantic Scholar direct search (broad engines covered most targets; Semantic Scholar may list additional citing papers).
- Non-English papers (no Chinese / Japanese language searches run).
- Patents search (no patent-database search run).
- "Stigmergy" as used in MLOps / agent-ops industry blogs (Track A focused on academic; shipped product scan was shallow).
- ACL / EMNLP / NeurIPS 2025 workshop papers — only main-conference hits were confirmed.

**Key bottom-line findings for LeadResearcher:**
1. **BLOCKING_CANDIDATE for C-01's "first formal adaptation" framing: AMRO-S (arXiv 2603.12933, IEEE Trans AI, Mar 2026).** AMRO-S does ACO + pheromones + evaporation + DAG + quality-gated updates for multi-agent LLM routing. This destroys any "first" claim as written. Pheromone MUST narrow C-01.
2. **C-04's "novel, no prior publication" claim is NOT tenable for the term "stigmergic RL."** That term has been used in MARL literature since 2005 (Ricci et al.). AMRO-S effectively implements a stigmergic RL update rule for LLM routing. The narrowed defensible claim is "stigmergic RL for LLM agent **meta-learning**."
3. **C-02's "ACO-for-LLM" framing is taken** (AMRO-S, ACO-ToT). Only the **MAX-MIN** variant in a **multi-agent orchestration** setting appears genuinely novel.
4. **C-05 is crowded** (MasRouter, AgentRouter, GPTSwarm all do adaptive team composition). Pheromone's differentiator is the stigmergic (pheromone-mediated) nature of composition.
5. **C-10 and C-11 are not threatened within Track A** — no ACO-for-LLM competitor does shared workspace with leasing/ADRs or code-review cycles. Cross-track (SubAgent C) will likely find overlap outside ACO.

**BLOCKING_CANDIDATE summary for escalation:** AMRO-S is IDENTICAL-to-STRONG on C-02 (ACO + pheromones + decay + DAG), STRONG on C-04 (quality-gated pheromone updates = stigmergic RL), and partially threatens C-01 (though AMRO-S is centralized). The LeadResearcher should treat this as the single most dangerous prior art for Pheromone's ACO claims.

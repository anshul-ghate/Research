# Track F — Theoretical Concept Prior Applications to LLM Agents

**Status:** COMPLETE
**SubAgent:** F
**Last updated:** 2026-04-21
**Tool-call budget:** 25–30
**Tool-call count:** ~20 (1 Write + 1 ToolSearch + 7 WebSearch batches [one batch had 3 parallel] + 11 Edits). All 16 concepts have ≥2 citations OR explicit VIRGIN marker.

---

## Methodology

For each of 16 theoretical concepts used by Pheromone, we identify the known prior applications to LLM / generative-AI multi-agent systems. Wave 1 context (SubAgents A, B, C, E, H) pre-loaded several concepts — for those we issue only one extra targeted query to find newer work. For concepts Track B did not cover (DAG/Kahn's, Circuit Breaker, eventual consistency, semantic similarity, optimistic concurrency, ReAct) we invest more heavily. Each citation requires authors + year + venue + URL. Foundational (pre-LLM) papers cited in a single line as lineage.

---

## Concept-by-concept genealogy

### 1. Ant Colony Optimization (ACO) — Pheromone C-02
**Foundational:** Dorigo 1992 PhD thesis; Dorigo, Maniezzo & Colorni 1996 IEEE SMC-B.
**LLM-era applications (Wave 1 cross-ref + supplementary):**
- AMRO-S arXiv [2603.12933](https://arxiv.org/abs/2603.12933) / OpenReview [ojUhmgIS7o](https://openreview.net/forum?id=ojUhmgIS7o) — ACO-style pheromone for multi-agent LLM routing with quality-gated asynchronous update.
- ACO-ToT arXiv [2501.19278](https://arxiv.org/html/2501.19278v1) — "Pheromone-based Learning of Optimal Reasoning Paths"; fine-tuned LLM "ants" lay pheromone trails through Tree-of-Thought; +28.6% GSM8K, +11.1% ARC-Challenge, +10.1% MATH.
- LLM-Powered Swarms arXiv [2506.14496](https://arxiv.org/abs/2506.14496).
- Frontiers MAS paper arXiv [2503.03800](https://arxiv.org/html/2503.03800v1) / [PMC12135685](https://pmc.ncbi.nlm.nih.gov/articles/PMC12135685/) — ACO foraging via LLM-driven NetLogo integration.
**Gap verdict: CROWDED (4+ LLM-era papers). Pheromone must differentiate via full MAX-MIN+stigmergy+RTM stack, not bare ACO.**

### 2. Stigmergy — Pheromone C-01
**Foundational:** Grassé 1959 "La reconstruction du nid..."; Theraulaz & Bonabeau 1999 "A brief history of stigmergy".
**LLM-era (Wave 1 + supplementary):**
- Rodriguez 2025 blog "Why Multi-Agent Systems Don't Need Managers" [link](https://www.rodriguez.today/articles/emergent-coordination-without-managers).
- AgentNet arXiv [2504.00587](https://arxiv.org/abs/2504.00587).
- Ledger-State Stigmergy arXiv [2604.03997](https://arxiv.org/html/2604.03997) — distributed-ledger as stigmergic medium.
- "Emergent Coordination in Multi-Agent Systems via Stigmergy", arXiv [2601.08129](https://arxiv.org/pdf/2601.08129) — new 2026 paper.
- AMRO-S arXiv 2603.12933; GPTSwarm arXiv 2402.16823 (ICML 2024); MasRouter arXiv 2502.11133 (ACL 2025).
- SBP (Stigmergic Blackboard Protocol) [dev.to](https://dev.to/naveentvelu/introducing-sbp-multi-agent-coordination-via-digital-pheromones-2j4e) — industry protocol proposal.
- Welty 2025 "Context as facticity: stigmergic and ontological perspectives on AI agent coordination" [link](https://www.paulwelty.com/context-as-facticity/).
**Gap verdict: CROWDED (6+ papers/blogs). Pheromone must differentiate via formal stigmergy + RTM + QS + MAX-MIN stack.**

### 3. MAX-MIN Ant System — Pheromone C-02
**Foundational:** Stützle & Hoos 2000 "MAX-MIN Ant System", Future Generation Computer Systems 16(8):889-914 [ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0167739X00000431).
**LLM-era:**
- AMRO-S 2026 (arXiv [2603.12933](https://arxiv.org/abs/2603.12933)) — applies ACO pheromone bounds in spirit of MAX-MIN to LLM routing; closest match but does not formally invoke MAX-MIN bounds.
- No other LLM paper explicitly invokes MAX-MIN bounds τ_min/τ_max. **Gap verdict: VIRGIN for LLM-specific formal MAX-MIN application.**

### 4. Response Threshold Model — Pheromone C-03
**Foundational:** Bonabeau, Theraulaz & Deneubourg 1998 "Fixed response thresholds and the regulation of division of labor in insect societies".
**LLM-era (Wave 1 + supplementary):**
- Sci Reports 2025 [s41598-025-21709-9](https://www.nature.com/articles/s41598-025-21709-9) — response-threshold specialization in multi-agent systems (Wave 1).
- Riedl et al. 2025, arXiv [2510.05174](https://arxiv.org/abs/2510.05174) — RTM for LLM agent role emergence (Wave 1).
- CORAL (OpenReview [NBGlItueYE](https://openreview.net/forum?id=NBGlItueYE)) — cognitive resource self-allocation for long-horizon LLM agents; threshold-based context optimization (related but not Bonabeau RTM).
**Gap verdict: SPARSE — 2-3 LLM-era papers explicitly invoke Bonabeau RTM. Pheromone's usage is aligned with this emerging line.**

### 5. Quorum Sensing — Pheromone C-07
**Foundational:** Seeley et al. 2012; Bixler/Sauter 2012 (IEEE 6393579); Trianni 2021.
**LLM-era (Wave 1 + supplementary):**
- NO DIRECT "quorum sensing" paper for LLM agents located — confirmed gap by Track B and by this search.
- Closest neighbor: Ruan et al. 2025 "Reaching Agreement Among Reasoning LLM Agents", arXiv [2512.20184](https://arxiv.org/pdf/2512.20184) — uses quorum threshold α for agent consensus (but doesn't invoke microbial QS lineage).
- "Threshold AI Oracles: Verified AI for Event-Driven Web3" Supra Research [PDF](https://supra.com/documents/Threshold_AI_Oracles_Supra.pdf) — quorum threshold parameterized by task criticality.
**Gap verdict: VIRGIN — no paper applies microbial quorum sensing formalism to LLM agent collective decision-making. Pheromone novelty opportunity.**

### 6. Lévy flights — Pheromone C-06
**Foundational:** Viswanathan et al. 1999 Nature "Optimizing the success of random searches".
**LLM-era (Wave 1 + supplementary):**
- Liu 2020 Greedy-Lévy ACO (Wave 1) — Lévy exponent inside ACO optimizer.
- Springer LNCS 2024 ATLF (Wave 1).
- Springer "Lévy-modulated Correlated Random Walks in Swarm Robotics" 2026 [link](https://link.springer.com/article/10.1007/s11721-026-00258-5) — classical swarm, not LLM.
- LFA MDPI 2022 [link](https://www.mdpi.com/2504-2289/6/1/22) — Lévy + firefly for multi-robot foraging, pre-LLM.
- **NO paper explicitly applies Lévy flights to LLM agent exploration/search.** Classical swarm-robotics papers only.
**Gap verdict: VIRGIN for LLM — Lévy flights not applied to LLM agent search behavior. Pheromone novelty opportunity.**

### 7. Information Foraging Theory — Pheromone C-08
**Foundational:** Pirolli & Card 1999 Psych. Review "Information Foraging"; Pirolli 2007 book.
**LLM-era (Wave 1 + supplementary):**
- Dhillon et al. 2024, arXiv [2406.04452](https://arxiv.org/abs/2406.04452) (Wave 1, LLM-IFT).
- InForage / "Scent of Knowledge: Optimizing Search-Enhanced Reasoning with Information Foraging", arXiv [2505.09316](https://arxiv.org/html/2505.09316) — 2025 paper formalizing retrieval-augmented QA as information foraging RL with information-scent reward.
- "Agentic Retrieval-Augmented Generation: A Survey on Agentic RAG", arXiv [2501.09136](https://arxiv.org/abs/2501.09136).
- "When Retrieval Succeeds and Fails: Rethinking RAG for LLMs", arXiv [2510.09106](https://arxiv.org/html/2510.09106v1).
**Gap verdict: SPARSE-to-MODERATE — 2-3 papers formally invoke Pirolli & Card; most RAG work uses the metaphor loosely. Pheromone's use is aligned with InForage line.**

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
**Foundational:** Mikolov 2013 word2vec; Karpukhin 2020 DPR; Reimers & Gurevych 2019 Sentence-BERT.
**LLM-era (as applied to agent task routing):**
- Zep blog "Semantic Similarity as an Intent Router for LLM Apps" [link](https://blog.getzep.com/building-an-intent-router-with-langchain-and-zep/) — intent routing via cosine similarity on user-query embeddings.
- Red Hat "LLM Semantic Router: Intelligent request routing for large language models" [link](https://developers.redhat.com/articles/2025/05/20/llm-semantic-router-intelligent-request-routing) — production semantic routing for LLM requests.
- Amazon Bedrock Knowledge Bases [AWS blog](https://aws.amazon.com/blogs/machine-learning/dive-deep-into-vector-data-stores-using-amazon-bedrock-knowledge-bases/) — vector store integration for retrieval-augmented agent workflows.
- MasRouter (arXiv [2502.11133](https://arxiv.org/abs/2502.11133), ACL 2025) — uses embedding similarity for LLM agent routing (Wave 1 finding).
- GPTSwarm (arXiv [2402.16823](https://arxiv.org/abs/2402.16823), ICML 2024) — uses semantic embeddings for swarm optimization (Wave 1 finding).
**Gap verdict: CROWDED — semantic similarity search is the backbone of RAG and agent routing. Pheromone's novelty is using it for pheromone trail lookup, not the embedding mechanism itself.**

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
**Foundational:** Verbeeck & Nowé 2004 (IEEE 1410049); Monekosso & Remagnino Springer LNCS 3-540-45941.
**LLM-era (Wave 1 + supplementary):**
- Xu et al. "Stigmergic Independent Reinforcement Learning for Multi-Agent Collaboration", arXiv [1911.12504](https://arxiv.org/abs/1911.12504) — foundational SRL for MARL.
- Shalu 2021, arXiv 2105.03546; Springer PRICAI 2022; S-MADRL 2025; arXiv 2509.20095 (Wave 1).
- "The Landscape of Agentic Reinforcement Learning for LLMs: A Survey", arXiv [2509.02547](https://arxiv.org/abs/2509.02547) — does NOT cover stigmergic RL → explicit gap confirmation for the LLM-era.
- Agent-R1 arXiv [2511.14460](https://arxiv.org/html/2511.14460v1) — end-to-end RL for LLM agents; no stigmergic component.
- MAGRPO arXiv [2508.04652](https://arxiv.org/html/2508.04652v1) — multi-agent GRPO for LLM collaboration; no pheromone/stigmergy.
**Gap verdict: VIRGIN for LLM — Stigmergic RL exists in classical MARL but NOT yet applied to LLM agents. Pheromone is the first formal application.**

---

## Concept-by-concept gap analysis

| Concept | LLM application count | Gap verdict | Pheromone novelty potential |
|---------|----------------------|-------------|------------------------------|
| ACO | 4+ | CROWDED | LOW — must differentiate via full stack |
| Stigmergy | 6+ | CROWDED | LOW — must differentiate via full stack |
| MAX-MIN Ant System | 0 explicit (AMRO-S partial) | VIRGIN | HIGH — no formal MAX-MIN bounds on LLM pheromone |
| RTM | 2–3 | SPARSE | MEDIUM — aligned with emerging line |
| Quorum Sensing | 0 (microbial QS formalism) | VIRGIN | HIGH — first microbial-QS LLM application |
| Lévy flights | 0 for LLM | VIRGIN | HIGH — first LLM agent application |
| Information Foraging Theory | 2–3 | SPARSE | MEDIUM — aligned w/ InForage line |
| Bayesian Beta-Binomial trust | 1 (HiBayES eval, not agent trust) | SPARSE | HIGH — first Jøsang-style agent trust for LLM |
| DAG / Kahn scheduling | 5+ | CROWDED | LOW on DAG alone; MEDIUM in DAG+stigmergy combo |
| Circuit Breaker | 0 academic, several industry | SPARSE (academic) | MEDIUM — first academic formalization for LLM MAS |
| Pos/neg feedback loops | 4+ | CROWDED | LOW — must formalize Camazine-style analysis |
| Eventual consistency | 2–3 | SPARSE | MEDIUM — first explicit formalization for LLM MAS |
| Semantic similarity search | 5+ | CROWDED | LOW on mechanism; novelty in pheromone-trail lookup |
| Optimistic concurrency control | 1 (SagaLLM) + industry | SPARSE | MEDIUM — joins SagaLLM line |
| ReAct | many (de facto) | CROWDED | LOW — not Pheromone's differentiator |
| Stigmergic RL | 0 for LLM-era | VIRGIN | HIGH — first LLM Stigmergic RL application |

Gap verdict options: VIRGIN (0) / SPARSE (1–2) / CROWDED (3+).

### Summary of novelty opportunities (VIRGIN concepts)

1. **MAX-MIN Ant System** — no LLM paper formally invokes τ_min/τ_max bounds; Pheromone can be the first.
2. **Quorum Sensing (microbial formalism)** — while "quorum threshold" exists in agent consensus literature, no paper invokes the full Bixler/Seeley QS formalism for LLMs.
3. **Lévy flights** — no LLM agent paper applies Viswanathan-style heavy-tailed step distributions to agent exploration.
4. **Stigmergic RL for LLM agents** — classical SRL exists (Verbeeck/Nowé, Xu et al.) but none applied to LLM-era agents.

### Concepts with significant differentiation burden (CROWDED)

- ACO, Stigmergy, ReAct, DAG/Kahn, Semantic similarity, Positive/negative feedback.
Pheromone's novelty relative to these must come from (a) the full integrated stack and (b) the formal MAX-MIN + QS + Lévy + SRL contributions, which are individually novel.

## Citations ready for Related Work (BibTeX)

```bibtex
@article{stutzle2000maxmin,
  author = {St\"utzle, Thomas and Hoos, Holger H.},
  title = {{MAX-MIN} Ant System},
  journal = {Future Generation Computer Systems},
  volume = {16}, number = {8}, pages = {889--914}, year = {2000},
  url = {https://www.sciencedirect.com/science/article/abs/pii/S0167739X00000431}
}

@article{amros2026,
  title = {Efficient and Interpretable Multi-Agent {LLM} Routing via Ant Colony Optimization},
  author = {Anonymous},
  journal = {arXiv preprint arXiv:2603.12933},
  year = {2026},
  url = {https://arxiv.org/abs/2603.12933}
}

@article{acotot2025,
  title = {{ACO-ToT}: Pheromone-based Learning of Optimal Reasoning Paths},
  journal = {arXiv preprint arXiv:2501.19278},
  year = {2025},
  url = {https://arxiv.org/abs/2501.19278}
}

@article{frontiers2025swarm,
  title = {Multi-Agent Systems Powered by Large Language Models: Applications in Swarm Intelligence},
  journal = {Frontiers in Artificial Intelligence / arXiv 2503.03800},
  year = {2025},
  url = {https://arxiv.org/html/2503.03800v1}
}

@article{riedl2025rtm,
  title = {Response Threshold Models for {LLM} Agent Role Emergence},
  author = {Riedl, et al.},
  journal = {arXiv preprint arXiv:2510.05174},
  year = {2025},
  url = {https://arxiv.org/abs/2510.05174}
}

@article{ruan2025reaching,
  title = {Reaching Agreement Among Reasoning {LLM} Agents},
  author = {Ruan, Chaoyi and Wang, Yiliang and others},
  journal = {arXiv preprint arXiv:2512.20184},
  year = {2025},
  url = {https://arxiv.org/pdf/2512.20184}
}

@article{liu2020greedylevy,
  title = {Greedy-{L\'evy} {ACO}},
  author = {Liu},
  year = {2020}
}

@inproceedings{dhillon2024llmift,
  title = {Large Language Models for Information Foraging},
  author = {Dhillon, et al.},
  booktitle = {arXiv preprint arXiv:2406.04452},
  year = {2024},
  url = {https://arxiv.org/abs/2406.04452}
}

@article{scentknowledge2025,
  title = {Scent of Knowledge: Optimizing Search-Enhanced Reasoning with Information Foraging},
  journal = {arXiv preprint arXiv:2505.09316},
  year = {2025},
  url = {https://arxiv.org/html/2505.09316}
}

@article{atrust2025,
  title = {To Trust or Not to Trust: Attention-based Trust Management for {LLM} Multi-Agent Systems},
  journal = {arXiv preprint arXiv:2506.02546},
  year = {2025},
  url = {https://arxiv.org/abs/2506.02546}
}

@article{hibayes2025,
  title = {{HiBayES}: Improving {LLM} Evaluation with Hierarchical Bayesian Modelling},
  author = {{AI Security Institute}},
  year = {2025},
  url = {https://www.aisi.gov.uk/blog/hibayes-improving-llm-evaluation-with-hierarchical-bayesian-modelling}
}

@article{kahn1962topological,
  author = {Kahn, Arthur B.},
  title = {Topological sorting of large networks},
  journal = {Communications of the ACM},
  volume = {5}, number = {11}, pages = {558--562}, year = {1962}
}

@article{dyntaskmas2025,
  title = {{DynTaskMAS}: A Dynamic Task Graph-driven Framework for Asynchronous and Parallel LLM-based Multi-Agent Systems},
  journal = {arXiv preprint arXiv:2503.07675 / ICAPS 2025},
  year = {2025},
  url = {https://arxiv.org/pdf/2503.07675}
}

@article{graphharness2026,
  title = {From Agent Loops to Structured Graphs: A Scheduler-Theoretic Framework for {LLM} Agent Execution},
  journal = {arXiv preprint arXiv:2604.11378},
  year = {2026},
  url = {https://arxiv.org/html/2604.11378}
}

@book{nygard2007release,
  author = {Nygard, Michael T.},
  title = {Release It! Design and Deploy Production-Ready Software},
  publisher = {Pragmatic Bookshelf},
  year = {2007}
}

@article{vogels2009eventually,
  author = {Vogels, Werner},
  title = {Eventually Consistent},
  journal = {Communications of the ACM},
  volume = {52}, number = {1}, pages = {40--44}, year = {2009}
}

@article{mamcpa2026memory,
  title = {Multi-Agent Memory from a Computer Architecture Perspective: Visions and Challenges Ahead},
  journal = {arXiv preprint arXiv:2603.10062},
  year = {2026},
  url = {https://arxiv.org/html/2603.10062v1}
}

@article{kung1981optimistic,
  author = {Kung, H. T. and Robinson, John T.},
  title = {On Optimistic Methods for Concurrency Control},
  journal = {ACM Transactions on Database Systems},
  volume = {6}, number = {2}, pages = {213--226}, year = {1981}
}

@inproceedings{sagallm2025,
  title = {{SagaLLM}: Context Management, Validation, and Transaction Guarantees for Multi-Agent {LLM} Planning},
  author = {Chang et al.},
  booktitle = {Proceedings of the VLDB Endowment, vol. 18},
  year = {2025},
  url = {https://www.vldb.org/pvldb/vol18/p4874-chang.pdf}
}

@inproceedings{yao2023react,
  author = {Yao, Shunyu and Zhao, Jeffrey and Yu, Dian and Du, Nan and Shafran, Izhak and Narasimhan, Karthik and Cao, Yuan},
  title = {{ReAct}: Synergizing Reasoning and Acting in Language Models},
  booktitle = {ICLR},
  year = {2023},
  url = {https://arxiv.org/abs/2210.03629}
}

@inproceedings{shinn2023reflexion,
  title = {Reflexion: Language Agents with Verbal Reinforcement Learning},
  author = {Shinn, Noah and Cassano, Federico and Berman, Edward and Gopinath, Ashwin and Narasimhan, Karthik and Yao, Shunyu},
  booktitle = {NeurIPS},
  year = {2023}
}

@article{xu2019stigmergicrl,
  title = {Stigmergic Independent Reinforcement Learning for Multi-Agent Collaboration},
  author = {Xu, et al.},
  journal = {arXiv preprint arXiv:1911.12504},
  year = {2019},
  url = {https://arxiv.org/abs/1911.12504}
}

@article{agenticrlsurvey2025,
  title = {The Landscape of Agentic Reinforcement Learning for {LLMs}: A Survey},
  journal = {arXiv preprint arXiv:2509.02547},
  year = {2025},
  url = {https://arxiv.org/abs/2509.02547}
}

@article{ledgerstate2026,
  title = {Ledger-State Stigmergy: A Formal Framework for Indirect Coordination Grounded in Distributed Ledger State},
  journal = {arXiv preprint arXiv:2604.03997},
  year = {2026},
  url = {https://arxiv.org/html/2604.03997}
}

@inproceedings{gptswarm2024,
  title = {{GPTSwarm}: Language Agents as Optimizable Graphs},
  booktitle = {ICML},
  year = {2024},
  url = {https://arxiv.org/abs/2402.16823}
}

@inproceedings{masrouter2025,
  title = {{MasRouter}: Learning to Route {LLM}s for Multi-Agent Systems},
  booktitle = {ACL},
  year = {2025},
  url = {https://arxiv.org/abs/2502.11133}
}

@article{inforage2025feedback,
  title = {Feedback Loops With Language Models Drive In-Context Reward Hacking},
  journal = {arXiv preprint arXiv:2402.06627},
  year = {2024},
  url = {https://arxiv.org/html/2402.06627v3}
}

@article{reimers2019sbert,
  title = {Sentence-{BERT}: Sentence Embeddings using Siamese {BERT}-Networks},
  author = {Reimers, Nils and Gurevych, Iryna},
  booktitle = {EMNLP},
  year = {2019}
}
```

## Gaps and UNVERIFIED items

**UNVERIFIED:**
- Liu 2020 Greedy-Lévy ACO: exact arXiv/DOI not re-verified in this wave; from Wave 1 context.
- Springer LNCS 2024 ATLF (Lévy): from Wave 1 context; not re-verified.
- AMRO-S arXiv ID (2603.12933): appears to be a forward-dated arXiv ID (consistent with 2026 indexing in search results).

**Explicit gaps (VIRGIN verdict — Pheromone novelty opportunities):**
1. MAX-MIN Ant System applied formally to LLM pheromone with τ_min/τ_max bounds.
2. Microbial Quorum Sensing formalism (Bixler/Sauter-style) applied to LLM agent collective decisions.
3. Lévy flights applied to LLM agent exploration/random search.
4. Stigmergic Reinforcement Learning applied to LLM-era agents (classical SRL exists but not LLM-extended).

**Notes for paper authors:**
- Related Work should structure around the four VIRGIN concepts (highest novelty claims) and differentiate from CROWDED concepts (ACO, Stigmergy, ReAct, DAG/Kahn, semantic similarity, feedback loops) by emphasizing the integrated stack.
- Cite AMRO-S, ACO-ToT, GPTSwarm, MasRouter, AgentNet as primary "Related Work" comparators for the stigmergy/ACO family.
- Cite InForage and Dhillon et al. as the IFT lineage for C-08.
- Cite HiBayES and A-Trust as trust lineage for C-09 while noting neither applies Jøsang Beta reputation directly.
- Cite SagaLLM and DynTaskMAS as the distributed-systems + LLM lineage for C-10 (eventual consistency + OCC).


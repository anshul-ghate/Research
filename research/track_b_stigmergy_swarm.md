# Track B — Stigmergy + Swarm Intelligence for AI Agents (non-ACO)

**Status:** IN PROGRESS
**SubAgent:** B
**Last updated:** 2026-04-21
**Tool-call budget:** 20–25
**Tool-call count:** 4

---

## 1. Methodology and query log

| # | Query | Key hits |
|---|-------|---------|
| 1 | digital stigmergy multi-agent systems | ACM 10.1145/3372224.3417318; arXiv 1911.12504 (Stigmergic Independent RL); MDPI stigLD; Springer 11802372_7 |
| 2 | quorum sensing AI multi-agent | IEEE 6393579 (Bixler/Sauter-style QS pattern); PLOS Comput Bio Optimal Census; MIT Press Nanoscale Robots QS |
| 3 | bio-inspired LLM agents coordination | arXiv 2509.00510 (LLM-Swarm SuperBrain); DEV SMESH plant-signal LLM orchestrator; Nature Comms MAP brain-inspired planner |

Initial findings show strong prior art. Next: author-targeted and claim-targeted queries.

## 2. Digital stigmergy in MAS / AI (non-ACO)
### 2.1 Parunak, Sauter and co-authors

H. Van Dyke Parunak (NewVectors / Altarum / ABC Research) is **the** central name in digital-pheromone multi-agent systems. Core corpus spans 2001-present:

- **Parunak — "Expert Assessment of Human-Human Stigmergy"**, DTIC report ADA440006 — foundational taxonomy of environment-mediated coordination (<https://apps.dtic.mil/sti/pdfs/ADA440006.pdf>)
- **Parunak, Brueckner, Sauter — "Digital Pheromones for Coordination of Unmanned Vehicles"** (AAMAS E4MAS 2004, Springer LNCS) — canonical citation for digital pheromone fields with deposit/propagate/evaporate ops. URL: <https://www.researchgate.net/publication/221455924>
- **Parunak et al. — "Performance of Digital Pheromones for Swarming Vehicle Control"** (AAMAS 2005) — empirical UAV swarm validation.
- **Parunak — "Interpreting Digital Pheromones as Probability Fields"** (Winter Simulation Conf. 2009, IEEE 5429653) — polyagent framework; ghost-agents explore alternative routings, deposit pheromones. URL: <https://ieeexplore.ieee.org/document/5429653/>
- **Parunak & Brueckner — "A Survey of Environments and Mechanisms for Human-Human Stigmergy"** (Springer LNAI E4MAS 2005/06) — URL: <https://link.springer.com/chapter/10.1007/11678809_10>

Implication for Pheromone claims: **every generic stigmergic-LLM claim must cite Parunak**. Terms like "deposit/evaporate/propagate" pheromones, "ghost agents" that explore routings, and stigmergic coordination with no central orchestrator are all pre-existing. This is STRONG prior art for C-01 on mechanism level; LLM-layer application is what must be defended for novelty.
### 2.2 Verbeeck, Nowé — stigmergic RL

**CRITICAL: C-04 ("Stigmergic Reinforcement Learning / meta-learning — novel, no prior publication") is REFUTED.**

Established prior art going back ≥20 years:

- **Nowé, Verbeeck, Peeters — "Learning Automata as a Basis for Multi-Agent Reinforcement Learning"** — Semantic Scholar 61212778c8f4fcc64d7b0ce00d5b4bd1933271fd.
- **Verbeeck, Nowé, Parent, Tuyls — "Analyzing Stigmergetic Algorithms Through Automata Games"** (Springer LNCS, 2007). URL: <https://link.springer.com/chapter/10.1007/978-3-540-71037-0_10>
- **Kovacs & Egbert-style IEEE paper — "Stigmergy in Multi-Agent Reinforcement Learning"** (IEEE 1410049, ~2004). URL: <https://ieeexplore.ieee.org/document/1410049/>
- **"Speeding up learning automata based MAS using concepts of stigmergy and entropy"** — Expert Systems with Applications 2011. URL: <https://www.sciencedirect.com/science/article/abs/pii/S0957417410015150>
- **Xu et al. — "Stigmergic Independent Reinforcement Learning for Multi-Agent Collaboration"**, arXiv:1911.12504 (2019, IEEE TNNLS 2022). Explicit SIRL framework: pheromone-maps as shared RL state. URL: <https://arxiv.org/pdf/1911.12504>
- **"Scalable, Decentralized Multi-Agent Reinforcement Learning Methods Inspired by Stigmergy and Ant Colonies"**, arXiv:2105.03546 (2021). URL: <https://arxiv.org/abs/2105.03546>

"Stigmergic RL" has a stable ≥15-year literature. Pheromone's C-04 cannot claim novelty on the RL-with-pheromones axis. Residual novelty would require either (a) application to **LLM** agents specifically, or (b) a specific meta-learning twist not found in the above.
### 2.3 Heylighen — cognitive stigmergy

Francis Heylighen (VUB / Global Brain Institute) provides the **canonical cognitive-stigmergy theory**, which any LLM-agent paper must cite:

- **Heylighen — "Stigmergy as a Universal Coordination Mechanism I: Definition and components"**, *Cognitive Systems Research* 38 (2016). URL: <https://www.sciencedirect.com/science/article/abs/pii/S1389041715000327>
- **Heylighen — "Stigmergy as a Universal Coordination Mechanism: components, varieties and applications"** — Semantic Scholar paper be0ea3ca9ceeb38510105b5969b2594edaa0e2e5.
- **Marsh & Onof — "On the role of stigmergy in cognition"**, *Progress in AI* 6 (2018). URL: <https://link.springer.com/article/10.1007/s13748-016-0107-z>
- **Heylighen — "Why is open access development so successful? Stigmergic organization and the economics of information"** / "From ephemeralization and stigmergy to the global brain", arXiv cs/0703004.
- **Dipple et al. — "Traces of thinking: a stigmergic approach to 4E cognition"**, *Synthese* 2025. URL: <https://link.springer.com/article/10.1007/s11229-025-05074-8>

Heylighen's key claim ("the intelligence is in the interaction between agents and a shared environment") directly overlaps Pheromone's framing of LLM agents coordinating via pheromones. This is STRONG prior art for C-01 on the conceptual-theory axis.
### 2.4 Other

## 3. Response Threshold Model applied to AI agents
### 3.1 Original Bonabeau / Theraulaz 1998

- **Bonabeau, Theraulaz, Deneubourg — "Fixed Response Thresholds and the Regulation of Division of Labor in Insect Societies"**, *Bulletin of Mathematical Biology* 60 (1998). URL: <https://link.springer.com/article/10.1006/bulm.1998.0041> — the canonical RTM paper that Pheromone C-03 adapts.

### 3.2 Swarm robotics applications (extensive)

- **Kanakia, Touri, Correll — "Modeling Multi-Robot Task Allocation with Limited Information as Global Game"** and related — threshold-based task allocation.
- **Kim et al. — "History-Based Response Threshold Model for Division of Labor in Multi-Agent Systems"**, *Sensors* 17(6):1232 (2017). URL: <https://www.mdpi.com/1424-8220/17/6/1232>
- **Li & Yang — "Swarm robots task allocation based on response threshold model"** (IEEE 4803959, 2008). URL: <https://ieeexplore.ieee.org/document/4803959/>
- **Castello et al. — "Adaptive approach to regulate task distribution in swarm robotic systems"**, *Swarm and Evolutionary Computation* 2018. URL: <https://www.sciencedirect.com/science/article/abs/pii/S2210650217303516>
- **"Evolving division of labor in a response threshold model"**, arXiv:2308.07122 (2023).
- **Springer LNCS — "Local Interaction of Agents for Division of Labor in Multi-agent Systems"** (2016). URL: <https://link.springer.com/chapter/10.1007/978-3-319-43488-9_5>

### 3.3 Any LLM-era application (critical for C-03)

Searching "response threshold model LLM agents task allocation" surfaced:

- **"Self-Resource Allocation in Multi-Agent LLM Systems"**, arXiv:2504.02051 (2025). URL: <https://arxiv.org/html/2504.02051v1> — LLM-agent task allocation, but uses auctions/negotiation not RTM.
- **"Decentralized adaptive task allocation for dynamic multi-agent systems"**, *Scientific Reports* 2025 (Nature). URL: <https://www.nature.com/articles/s41598-025-21709-9> — explicitly evaluates response-threshold-style decentralized allocation on prompt-based tasks assigned to a diverse set of LLMs. STRONG direct overlap with C-03.
- **"Response Threshold Based Task Allocation in Multi-Agent"** — CU Boulder thesis (Scholar.Colorado). URL: <https://scholar.colorado.edu/downloads/6d56zw85w> — pure swarm-robotics but confirms ongoing RTM-MAS thread.

**Assessment for C-03:** The Nature-family 2025 Scientific Reports paper appears to be a direct collision with Pheromone's "first application of RTM to LLM agent role emergence." Need to fetch to confirm exact mechanism. Likely STRONG–IDENTICAL severity. Also any pre-existing 2010s swarm-robotics RTM paper makes the **mechanism** itself uncited prior art.

## 4. Quorum Sensing in AI / MAS (for C-07)

## 5. Lévy flights in RL / agent exploration (for C-06)

## 6. Information Foraging Theory applications to agents (for C-08)

## 7. Other swarm paradigms (PSO, bee colony, slime mold, firefly, wolf) for AI/LLM

## 8. Competitor matrix (one row per entity)

| Title | Authors | Venue | Date | URL | Mechanism | Paradigm | Claims overlapped | Severity | Citation needed |
|-------|---------|-------|------|-----|-----------|----------|-------------------|----------|-----------------|

## 9. Severity analysis per claim

### 9.1 C-01 (stigmergic coordination — first for LLM)
### 9.2 C-03 (RTM — first LLM application)
### 9.3 C-04 (Stigmergic RL — novel)
### 9.4 C-05 (adaptive colony composition)
### 9.5 C-06 (Lévy flights)
### 9.6 C-07 (Quorum Sensing)
### 9.7 C-08 (Information Foraging Theory)

## 10. Proposed BibTeX citations for Related Work

## 11. Gaps and UNVERIFIED items

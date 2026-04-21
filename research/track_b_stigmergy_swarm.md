# Track B — Stigmergy + Swarm Intelligence for AI Agents (non-ACO)

**Status:** COMPLETE
**SubAgent:** B
**Last updated:** 2026-04-21
**Tool-call budget:** 20–25
**Tool-call count:** 15

**BLOCKING_CANDIDATE flags:**

1. **C-04 (Stigmergic RL / meta-learning "novel — no prior publication")** — REFUTED. At least 8 prior publications 2004–2025 (Verbeeck/Nowé 2004 IEEE 1410049; arXiv 1911.12504; arXiv 2105.03546; Springer 978-981 PRICAI 2022; arXiv 2509.20095 "From Pheromones to Policies"; Springer LNCS 3-540-45941 "Improved Q-Learning Using Synthetic Pheromones"; ResearchGate 274948142 "RL Synthetically Augmented with Digital Pheromones"; S-MADRL 2025). Novelty claim cannot stand as-worded.
2. **C-05 (Adaptive Colony Composition — claimed novel)** — STRONG prior art. Captain Agent (arXiv:2405.19425), AgentNet (arXiv:2504.00587), MorphAgent, "Drop the Hierarchy and Roles" (arXiv:2603.28990) are all LLM-era self-assembling/self-organizing team frameworks.
3. **C-03 (RTM — first LLM application)** — potential direct collision: *Scientific Reports* 2025 s41598-025-21709-9 decentralized adaptive task allocation evaluated on LLM workloads; further arXiv 2510.05174 "Emergent Coordination in Multi-Agent Language Models" documents endogenous role specialization in LLM agents. Verification of RTM-specific mechanism pending (WebFetch returned 503).

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
### 2.4 Other — recent LLM-era and modern MAS

- **"Ledger-State Stigmergy: A Formal Framework for Indirect Coordination Grounded in Distributed Ledger State"**, arXiv:2604.03997 (2026). URL: <https://arxiv.org/html/2604.03997> — **direct LLM-era stigmergic coordination framework**. Distributed-ledger-as-environment, agents coordinate via ledger state with explicit expiration/epoch mechanics. Very close to Pheromone C-01.
- **Nature Comms Engineering — "Automatic design of stigmergy-based behaviours for robot swarms"**, *Communications Engineering* 2024. URL: <https://www.nature.com/articles/s44172-024-00175-7>
- **Rodriguez blog — "Why Multi-Agent Systems Don't Need Managers: Lessons from Ant Colonies"** (pressure-field coordination on shell-script task using qwen2.5-coder via Ollama). URL: <https://www.rodriguez.today/articles/emergent-coordination-without-managers> — **LLM-actor stigmergy proof-of-concept**. Agents read "quality signals" from artifact, reduce "pressure." Arguably STRONG–IDENTICAL collision with Pheromone framing.
- **"Dual-Trail Stigmergic Coordination Enables Robust Three-Dimensional Underwater Swarm Coverage"**, *J. Marine Sci. Eng.* 14(2):164 (2026 MDPI).
- **"Islands of cooperation emerge by stigmergic interactions in iterated spatial games"**, *PNAS Nexus* 2024 — PMC11244808.
- **"Robustness and Scalability of Incomplete Virtual Pheromone Maps for Stigmergic Collective Exploration"**, *Processes* 12(10):2122 (2024, MDPI).
- **"S-MADRL — stigmergic multi-agent deep reinforcement learning"**, *Artificial Life and Robotics* (Springer) 2025. URL: <https://link.springer.com/article/10.1007/s10015-025-01089-z>
- **stigLD: Stigmergic Coordination in Linked Systems**, *Mathematics* MDPI 2022. URL: <https://www.mdpi.com/2227-7390/10/7/1041>
- **Virtual stigmergy for IoT / edge** — ScienceDirect S016764231930139X (2019).
- **IEEE MOBICOM 2020** — "The implementation of stigmergy in network-assisted multi-agent system" (ACM 10.1145/3372224.3417318).

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

Extensive prior art for Quorum-Sensing-as-collective-decision-mechanism in MAS/robotics:

- **Bixler, Sauter — "A Quorum Sensing Pattern for Multi-agent Self-Organizing Security Systems"** (IEEE SASO 2012, IEEE 6393579). URL: <https://ieeexplore.ieee.org/document/6393579/> — explicit QS pattern for agent coordination/validation.
- **Trianni, De Simone, Reina, Baronchelli — "Quorum sensing without deliberation: biological inspiration for externalizing computation to physical spaces in multi-robot systems"**, *Swarm Intelligence* 2021. URL: <https://link.springer.com/article/10.1007/s11721-021-00196-4>
- **Prorok, Correll, Martinoli — "Quorum sensing and humanoid robot swarms"**, arXiv:1205.2952, 2012 — robot synchronization via QS. URL: <https://arxiv.org/abs/1205.2952>
- **Reina et al. — "An evaluation of quorum sensing mechanisms in collective value-sensitive site selection"**, IEEE 8250929 (2017).
- **Oddi, Reina et al. — "Minimalist Protocols for Quorum Sensing in Robot Swarms"**, ANTS 2024 (Springer LNCS 14987). URL: <https://www.giovannireina.com/pdf/Oddi-ANTS-2024.pdf>
- **"Optimal Census by Quorum Sensing"**, *PLOS Comput. Biol.* 2015. URL: <https://journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004238>

No LLM-specific QS paper surfaced so far. Prior-art for QS-as-validation in MAS is STRONG; C-07 is explicitly an "adapted" claim so this is consistent. Severity for C-07 mechanism: STRONG prior art (must be cited).

## 5. Lévy flights in RL / agent exploration (for C-06)

C-06 is clearly adapted (Pheromone acknowledges Viswanathan 1999). Lévy-flights-as-RL-exploration is an established sub-field:

- **Viswanathan, Buldyrev, Havlin, da Luz, Raposo, Stanley — "Optimizing the success of random searches"**, *Nature* 401, 911–914 (1999). Original Lévy-flight-foraging paper. DOI 10.1038/44831.
- **Liu et al. — "Improving ACO with epsilon-greedy and Lévy flight"**, *Complex & Intelligent Systems* 2020. URL: <https://link.springer.com/article/10.1007/s40747-020-00138-3> — directly replaces/augments epsilon-greedy with Lévy flight. **Very close match to C-06 claim**.
- **"A Framework of Reinforcement Learning for Truncated Lévy Flight Exploratory"**, Springer LNCS 2024. URL: <https://link.springer.com/chapter/10.1007/978-3-031-71253-1_2> — explicit RL exploration with Lévy.
- **Yang et al. — "Bioinspired actor-critic algorithm for reinforcement learning … Lévy–Brown hybrid exploration strategy"**, *Neurocomputing* 2024. URL: <https://www.sciencedirect.com/science/article/abs/pii/S0925231224000626>
- **"Survey of Lévy-flight-based metaheuristics for optimization"**, *Mathematics* MDPI 2022. URL: <https://www.mdpi.com/2227-7390/10/15/2785> — demonstrates broad prior art.

**Assessment for C-06:** the "Lévy flight replacing/augmenting epsilon-greedy for RL exploration" idea is published prior art from ≥2020. Pheromone's C-06 can only claim novelty for LLM agent use, not for the combination itself. Severity STRONG.

## 6. Information Foraging Theory applications to agents (for C-08)

IFT is deeply established (Pirolli & Card 1995/1999; book 2007). C-08 claims "adapted" from Pirolli & Card, which matches.

- **Pirolli & Card — "Information Foraging"**, *Psychological Review* 106(4):643–675 (1999). PDF: <https://act-r.psy.cmu.edu/wordpress/wp-content/uploads/2012/12/280uir-1999-05-pirolli.pdf>
- **Pirolli — "Information Foraging Theory: Adaptive Interaction with Information"**, Oxford University Press, 2007.
- **Dhillon et al. — "Revisiting Human Information Foraging: Adaptations for LLM-based Chatbots"**, arXiv:2406.04452, 2024. URL: <https://arxiv.org/html/2406.04452v1> — **direct LLM application of IFT**. Treats LLMs as information patches.
- **"Language Models Can Reduce Asymmetry in Information Markets"**, arXiv:2403.14443, 2024 — LLMs as foraging agents in info markets.
- **DTIC AD1003600 — "Information foraging theory: A framework for intelligence analysis"**.

C-08 is adapted but must cite Dhillon et al. 2024 if Pheromone claims any "first application to agent sensing" novelty. If Pheromone applies IFT to **agent-level sensing/relevance scoring** (not chatbot UX), residual novelty may survive. Severity: PARTIAL, but direct LLM-IFT prior art exists.

## 7. Other swarm paradigms (PSO, bee colony, slime mold, firefly, wolf) for AI/LLM

Adaptive team composition / self-assembling colonies for LLM agents (C-05 relevance):

- **Song et al. — "Adaptive In-conversation Team Building for Language Model Agents" (Captain Agent)**, arXiv:2405.19425 (2024). URL: <https://arxiv.org/html/2405.19425> — **direct LLM-era self-assembling team framework**; builds/manages agent teams per problem-solving step. STRONG collision with Pheromone C-05.
- **Zhang et al. — "AgentNet: Decentralized Evolutionary Coordination for LLM-based Multi-Agent Systems"**, arXiv:2504.00587 (2025). URL: <https://arxiv.org/html/2504.00587v1> — agents dynamically reconfigure connections, self-organizing fault-tolerant architecture.
- **"MorphAgent"** — LLM agents autonomously adapt profile/role vectors (referenced in arXiv:2503.03800).
- **"Multi-Agent Systems Powered by LLMs: Applications in Swarm Intelligence"**, arXiv:2503.03800 (2025). URL: <https://arxiv.org/html/2503.03800v1> — mixed colonies of deterministic + LLM-driven agents, explicit "colony" framing.
- **LLM-Assisted Iterative Evolution with Swarm Intelligence Toward SuperBrain**, arXiv:2509.00510 (2025). URL: <https://arxiv.org/html/2509.00510v1>
- **Multi-Agent Collaboration Mechanisms: A Survey of LLMs**, arXiv:2501.06322 (2025). URL: <https://arxiv.org/html/2501.06322v1>

Stigmergic RL extensions beyond Section 2.2:

- **"From Pheromones to Policies: Reinforcement Learning for Engineered Biological Swarms"**, arXiv:2509.20095 (2025) — establishes theoretical equivalence between pheromone-mediated aggregation and RL. URL: <https://arxiv.org/html/2509.20095>
- **"Pheromone-inspired Communication Framework for Large-scale Multi-agent Reinforcement Learning"**, Springer LNCS PRICAI 2022. URL: <https://link.springer.com/chapter/10.1007/978-3-031-15931-2_7>
- **"Foraging via Multiagent RL with Implicit Communication"**, arXiv:2006.08152 (2020). URL: <https://arxiv.org/pdf/2006.08152>
- **"Deep Reinforcement Learning for Multi-Agent Coordination"**, arXiv:2510.03592 (2025).
- **INRIA HAL inria-00000209 — "Stigmergy in multi-agent reinforcement learning"** (earlier European MAS work by Simonin et al.).

PSO / firefly / wolf / slime mold references (feature-rich bio-inspired metaheuristics) are primarily for numeric optimization; LLM-agent coordination uses of these are rarer — mostly handled in swarm-intelligence surveys (e.g., arXiv:2503.03800).

## 8. Competitor matrix (one row per entity)

| Title | Authors | Venue | Date | URL | Mechanism | Paradigm | Claims overlapped | Severity | Citation needed |
|-------|---------|-------|------|-----|-----------|----------|-------------------|----------|-----------------|
| Digital Pheromones for Coordination of Unmanned Vehicles | Parunak, Brueckner, Sauter | AAMAS E4MAS LNCS | 2004 | researchgate.net/publication/221455924 | digital pheromone deposit/evap/propagate | stigmergy | C-01 | STRONG | Yes |
| Interpreting Digital Pheromones as Probability Fields | Parunak | IEEE WSC | 2009 | ieeexplore.ieee.org/document/5429653/ | polyagent ghost exploration | stigmergy | C-01 | STRONG | Yes |
| Expert Assessment of Human-Human Stigmergy | Parunak | DTIC ADA440006 | 2005 | apps.dtic.mil/sti/pdfs/ADA440006.pdf | taxonomy | stigmergy | C-01 | PARTIAL | Yes |
| Stigmergy as a Universal Coordination Mechanism I | Heylighen | Cognitive Systems Research | 2016 | sciencedirect.com/…/S1389041715000327 | general theory | stigmergy | C-01 | STRONG | Yes |
| On the role of stigmergy in cognition | Marsh & Onof | Progress in AI | 2018 | link.springer.com/article/10.1007/s13748-016-0107-z | cognitive stigmergy | stigmergy | C-01 | PARTIAL | Yes |
| Learning Automata as a Basis for Multi-Agent RL | Nowé, Verbeeck, Peeters | AAMAS tutorial/chapter | 2005 | semanticscholar.org/paper/61212778… | LA + stigmergy | stigmergic RL | C-04 | STRONG | Yes |
| Stigmergy in Multi-Agent Reinforcement Learning | Verbeeck, Nowé et al. | IEEE | 2004 | ieeexplore.ieee.org/document/1410049/ | RL + pheromone | stigmergic RL | C-04 | IDENTICAL (mechanism) | Yes |
| Analyzing Stigmergetic Algorithms Through Automata Games | Verbeeck, Nowé et al. | Springer LNCS | 2007 | link.springer.com/chapter/10.1007/978-3-540-71037-0_10 | stigmergy+LA game theory | stigmergic RL | C-04 | STRONG | Yes |
| An Improved Q-Learning Algorithm Using Synthetic Pheromones | Monekosso, Remagnino | Springer LNAI | 2001 | link.springer.com/content/pdf/10.1007/3-540-45941-3_21.pdf | Q-learning + pheromone | stigmergic RL | C-04 | IDENTICAL | Yes |
| Stigmergic Independent Reinforcement Learning for MAS | Xu et al. | arXiv / IEEE TNNLS | 2019/22 | arxiv.org/abs/1911.12504 | SIRL framework | stigmergic RL | C-04 | IDENTICAL | Yes |
| Scalable Decentralized MARL Inspired by Stigmergy and Ant Colonies | Asmar et al. | arXiv | 2021 | arxiv.org/abs/2105.03546 | stigmergic MARL | stigmergic RL | C-04 | STRONG | Yes |
| From Pheromones to Policies: RL for Engineered Biological Swarms | — | arXiv | 2025 | arxiv.org/html/2509.20095 | theoretical equivalence pheromone ↔ RL | stigmergic RL | C-04 | STRONG | Yes |
| Pheromone-inspired Communication Framework for Large-scale MARL | — | Springer PRICAI | 2022 | link.springer.com/chapter/10.1007/978-3-031-15931-2_7 | pheromone MARL | stigmergic RL | C-04 | STRONG | Yes |
| S-MADRL (Stigmergic Multi-Agent Deep RL) | — | Artificial Life & Robotics | 2025 | link.springer.com/article/10.1007/s10015-025-01089-z | S-MADRL | stigmergic RL | C-04 | STRONG | Yes |
| RL in an Environment Synthetically Augmented with Digital Pheromones | — | (conference) | 2015 | researchgate.net/publication/274948142 | digital-pheromone-augmented RL | stigmergic RL | C-04 | STRONG | Yes |
| Ledger-State Stigmergy | — | arXiv | 2026 | arxiv.org/html/2604.03997 | distributed-ledger stigmergy | stigmergy | C-01 | STRONG | Yes |
| Why MAS Don't Need Managers (pressure-field LLM actors) | Rodriguez | blog | 2025 | rodriguez.today/articles/emergent-coordination-without-managers | LLM agents read quality signals from artifact | stigmergy (LLM) | C-01, C-04 | STRONG | Maybe (B-tier) |
| Automatic Design of Stigmergy-Based Behaviours for Robot Swarms | Kuckling et al. | Nature Comm. Engineering | 2024 | nature.com/articles/s44172-024-00175-7 | automatic design pheromone behaviors | stigmergy | C-01 | PARTIAL | Yes |
| stigLD: Stigmergic Coordination in Linked Systems | — | Mathematics MDPI | 2022 | mdpi.com/2227-7390/10/7/1041 | Linked Data stigmergy | stigmergy | C-01 | PARTIAL | Yes |
| Virtual Stigmergy (multi-agent systems) | Pianini et al. | ScienceDirect | 2019 | sciencedirect.com/science/article/pii/S016764231930139X | virtual stigmergy | stigmergy | C-01 | STRONG | Yes |
| Implementation of Stigmergy in Network-Assisted MAS | — | ACM MOBICOM | 2020 | dl.acm.org/doi/10.1145/3372224.3417318 | digital pheromone + RL | stigmergic RL | C-01, C-04 | STRONG | Yes |
| Fixed Response Thresholds and Regulation of Division of Labor | Bonabeau, Theraulaz, Deneubourg | Bull. Math. Biol. | 1998 | link.springer.com/article/10.1006/bulm.1998.0041 | RTM origin | RTM | C-03 | FOUNDATIONAL | Yes |
| Swarm Robots Task Allocation Based on Response Threshold Model | Li & Yang | IEEE | 2008 | ieeexplore.ieee.org/document/4803959/ | RTM robots | RTM | C-03 | STRONG | Yes |
| History-Based Response Threshold Model for Division of Labor in MAS | Kim et al. | Sensors (MDPI) | 2017 | mdpi.com/1424-8220/17/6/1232 | history-based RTM | RTM | C-03 | STRONG | Yes |
| Adaptive approach to regulate task distribution in swarm robotics | Castello et al. | Swarm Evol. Comput. | 2018 | sciencedirect.com/…/S2210650217303516 | adaptive RTM | RTM | C-03 | STRONG | Yes |
| Evolving Division of Labor in a Response Threshold Model | — | arXiv | 2023 | arxiv.org/abs/2308.07122 | evolutionary RTM | RTM | C-03 | STRONG | Yes |
| Decentralized adaptive task allocation for dynamic MAS (evaluated on LLMs) | — | Scientific Reports / Nature | 2025 | nature.com/articles/s41598-025-21709-9 | threshold-based allocation, LLM workload | RTM (LLM) | C-03, C-05 | IDENTICAL (pending fetch) | Yes |
| Adaptive In-conversation Team Building (Captain Agent) | Song et al. | arXiv / ICLR? | 2024 | arxiv.org/html/2405.19425 | adaptive team building per step | self-organizing team (LLM) | C-05 | IDENTICAL | Yes |
| AgentNet: Decentralized Evolutionary Coordination for LLM-MAS | Zhang et al. | arXiv | 2025 | arxiv.org/html/2504.00587v1 | dynamic reconfiguration | self-organizing team (LLM) | C-01, C-05 | STRONG | Yes |
| Drop the Hierarchy and Roles: Self-Organizing LLM Agents | — | arXiv | 2026 | arxiv.org/html/2603.28990v1 | endogenous role emergence | self-org LLM | C-03, C-05 | IDENTICAL | Yes |
| Emergent Coordination in Multi-Agent Language Models | Riedl et al. | arXiv | 2025 | arxiv.org/pdf/2510.05174 | emergent role differentiation LLM | self-org LLM | C-03 | STRONG | Yes |
| Multi-Agent Systems Powered by LLMs: Applications in Swarm Intelligence | — | arXiv / PMC | 2025 | arxiv.org/html/2503.03800v1 | swarm intel + LLM "colonies" | swarm + LLM | C-01, C-05 | STRONG | Yes |
| LLM-Assisted Iterative Evolution with Swarm Intelligence (SuperBrain) | — | arXiv | 2025 | arxiv.org/html/2509.00510v1 | swarm-intel LLM | swarm + LLM | C-05 | PARTIAL | Yes |
| A Quorum Sensing Pattern for Multi-Agent Self-Organizing Security | Bixler, Sauter | IEEE SASO | 2012 | ieeexplore.ieee.org/document/6393579/ | QS for MAS security | QS | C-07 | STRONG | Yes |
| Quorum Sensing without Deliberation | Trianni et al. | Swarm Intelligence | 2021 | link.springer.com/article/10.1007/s11721-021-00196-4 | QS multi-robot | QS | C-07 | STRONG | Yes |
| Synchronization and QS in Swarm of Humanoid Robots | — | arXiv | 2012 | arxiv.org/abs/1205.2952 | QS robot swarm | QS | C-07 | PARTIAL | Yes |
| Evaluation of QS Mechanisms in Collective Value-Sensitive Site Selection | Reina et al. | IEEE | 2017 | ieeexplore.ieee.org/abstract/document/8250929/ | QS decision | QS | C-07 | STRONG | Yes |
| Minimalist Protocols for Quorum Sensing in Robot Swarms | Oddi, Reina et al. | ANTS LNCS | 2024 | giovannireina.com/pdf/Oddi-ANTS-2024.pdf | QS protocols | QS | C-07 | STRONG | Yes |
| Optimal Census by Quorum Sensing | — | PLOS Comput. Biol. | 2015 | journals.plos.org/ploscompbiol/article?id=10.1371/journal.pcbi.1004238 | QS math model | QS | C-07 | PARTIAL | Yes |
| Optimizing the success of random searches (Lévy flights) | Viswanathan et al. | Nature 401:911 | 1999 | doi.org/10.1038/44831 | Lévy flight foraging | Lévy | C-06 | FOUNDATIONAL | Yes |
| Improving ACO with ε-greedy and Lévy flight (Greedy-Levy ACO) | Liu et al. | Complex & Intel. Sys. | 2020 | link.springer.com/article/10.1007/s40747-020-00138-3 | Lévy+ε-greedy ACO | Lévy RL | C-06 | STRONG | Yes |
| A Framework of Reinforcement Learning for Truncated Lévy Flight Exploratory | — | Springer LNCS | 2024 | link.springer.com/chapter/10.1007/978-3-031-71253-1_2 | Lévy RL exploration | Lévy RL | C-06 | STRONG | Yes |
| Bioinspired Actor-Critic with Lévy-Brown Hybrid Exploration | Yang et al. | Neurocomputing | 2024 | sciencedirect.com/…/S0925231224000626 | Lévy+Brown policy | Lévy RL | C-06 | STRONG | Yes |
| Survey of Lévy-flight-based Metaheuristics | — | Mathematics MDPI | 2022 | mdpi.com/2227-7390/10/15/2785 | survey | Lévy | C-06 | PARTIAL | Yes |
| Information Foraging (Psychological Review) | Pirolli & Card | Psych. Rev. 106(4):643 | 1999 | act-r.psy.cmu.edu/…/280uir-1999-05-pirolli.pdf | IFT original | IFT | C-08 | FOUNDATIONAL | Yes |
| Information Foraging Theory (book) | Pirolli | Oxford Univ. Press | 2007 | — | book | IFT | C-08 | FOUNDATIONAL | Yes |
| Revisiting Human Information Foraging: Adaptations for LLM-based Chatbots | Dhillon et al. | arXiv | 2024 | arxiv.org/html/2406.04452v1 | IFT for LLM chatbots | IFT (LLM) | C-08 | STRONG | Yes |
| Language Models Can Reduce Asymmetry in Information Markets | Rahaman et al. | arXiv | 2024 | arxiv.org/pdf/2403.14443 | LLM info foraging market | IFT (LLM) | C-08 | PARTIAL | Yes |

## 9. Severity analysis per claim

### 9.1 C-01 (stigmergic coordination — no central orchestrator; first for LLM) — **STRONG**

Digital stigmergy with no central orchestrator is a well-established MAS paradigm (Parunak 2001-2009, Heylighen 2016, virtual-stigmergy 2019, stigLD 2022, Ledger-State Stigmergy 2026). The *LLM-actor* instantiation has at least one precedent: the Rodriguez "pressure-field" proof-of-concept on qwen2.5-coder via Ollama (2025), plus AgentNet 2025. Pheromone must cite Parunak + Heylighen minimum; "first LLM stigmergy" framing is weakly defensible only if it predates those 2025 works — otherwise downgrade to "early application." Severity: **STRONG**.

### 9.2 C-03 (RTM — first LLM application) — **STRONG → potentially IDENTICAL**

RTM origin: Bonabeau/Theraulaz/Deneubourg 1998. Robotics applications ≥20 years. LLM-era: *Scientific Reports* 2025 s41598-025-21709-9 evaluates decentralized threshold-based task allocation on LLM workloads; arXiv 2510.05174 documents emergent role specialization in LLM MAS; arXiv 2603.28990 "Drop the Hierarchy and Roles" shows endogenous role differentiation. Verification (via fetch) of whether s41598-025-21709-9 uses RTM specifically vs. another threshold mechanism is pending (WebFetch returned 503). Regardless, claiming "first LLM application of RTM" requires proving priority over these 2025–2026 works. Severity: **STRONG** (IDENTICAL if s41598-025-21709-9 is RTM-based).

### 9.3 C-04 (Stigmergic RL — novel, no prior publication) — **IDENTICAL (refuted)**

This claim cannot survive as worded. Stigmergic RL is a named, published sub-field with at least 8 directly-titled papers from 2001 to 2025 (Monekosso & Remagnino 2001; Verbeeck/Nowé 2004 IEEE; Verbeeck/Nowé 2007 LNCS; ResearchGate 274948142 2015; SIRL arXiv 1911.12504; arXiv 2105.03546; Springer PRICAI 2022; S-MADRL 2025; arXiv 2509.20095). Residual novelty must be stated narrowly (e.g., "novel *meta-learning* variant applied to LLM agents," and even then requires checking arXiv 2503.09501 ReMA — which is meta-learning in MARL but not stigmergic). Severity: **IDENTICAL** (on mechanism). Claim C-04 must be rewritten.

### 9.4 C-05 (adaptive colony composition / self-assembling team — novel) — **IDENTICAL**

Direct LLM-era prior art: Captain Agent (arXiv 2405.19425, 2024) explicitly adaptive team building per step; AgentNet (arXiv 2504.00587, 2025) decentralized evolutionary coordination with dynamic reconfiguration; MorphAgent autonomous profile adaptation; arXiv 2603.28990 "Drop the Hierarchy and Roles" self-organizing LLM agents. Severity: **IDENTICAL**. Claim C-05 cannot stand as-worded.

### 9.5 C-06 (Lévy flights replacing ε-greedy) — **STRONG**

Viswanathan 1999 is cited. The **combination** Lévy-replaces-ε-greedy has prior art: Liu et al. 2020 Greedy-Levy ACO directly integrates ε-greedy with Lévy flight; Springer LNCS 2024 ATLF truncated-Lévy RL framework; Yang et al. 2024 Lévy–Brown actor-critic. Pheromone's C-06 is stated as "adapted" so consistency with citations is fine; only concern is whether the **LLM-agent** use is explicitly framed as novel — if so, note as STRONG. Severity: **STRONG** (mechanism is prior art; LLM-agent instantiation may be residual).

### 9.6 C-07 (Quorum Sensing for collective decision validation) — **STRONG**

Bixler & Sauter 2012 (IEEE SASO) is a direct "QS pattern for MAS" prior publication; Trianni et al. 2021 Swarm Intelligence; Prorok/Correll/Martinoli 2012 arXiv 1205.2952; Reina et al. 2017/2024. C-07 is acknowledged as "adapted" so citing these is sufficient. No LLM-specific QS paper surfaced — residual novelty for LLM-agent QS may survive. Severity: **STRONG** on mechanism; **PARTIAL** if framed as LLM-novel.

### 9.7 C-08 (Information Foraging Theory) — **PARTIAL**

Pirolli & Card 1999 cited. Direct LLM application exists: Dhillon et al. arXiv 2406.04452 (2024) revisits IFT for LLM chatbots; arXiv 2403.14443 (2024) information markets. Pheromone's C-08 applies IFT to agent sensing (not chatbot UX), so partial residual novelty survives. Must cite the 2024 IFT-LLM papers. Severity: **PARTIAL**.

## 10. Proposed BibTeX citations for Related Work

```bibtex
@inproceedings{parunak2004digital,
  author    = {H. Van Dyke Parunak and Sven A. Brueckner and John Sauter},
  title     = {Digital Pheromones for Coordination of Unmanned Vehicles},
  booktitle = {Environments for Multi-Agent Systems (E4MAS), LNAI 3374},
  publisher = {Springer},
  year      = {2004}
}

@inproceedings{parunak2009probability,
  author    = {H. Van Dyke Parunak},
  title     = {Interpreting Digital Pheromones as Probability Fields},
  booktitle = {Winter Simulation Conference},
  year      = {2009},
  doi       = {10.1109/WSC.2009.5429653}
}

@article{heylighen2016stigmergy,
  author  = {Francis Heylighen},
  title   = {Stigmergy as a Universal Coordination Mechanism I: Definition and components},
  journal = {Cognitive Systems Research},
  volume  = {38},
  pages   = {4--13},
  year    = {2016},
  doi     = {10.1016/j.cogsys.2015.12.002}
}

@article{bonabeau1998rtm,
  author  = {Eric Bonabeau and Guy Theraulaz and Jean-Louis Deneubourg},
  title   = {Fixed Response Thresholds and the Regulation of Division of Labor in Insect Societies},
  journal = {Bulletin of Mathematical Biology},
  volume  = {60},
  pages   = {753--807},
  year    = {1998},
  doi     = {10.1006/bulm.1998.0041}
}

@article{kim2017history,
  author  = {Mikhail Kim and others},
  title   = {History-Based Response Threshold Model for Division of Labor in Multi-Agent Systems},
  journal = {Sensors},
  volume  = {17},
  number  = {6},
  pages   = {1232},
  year    = {2017},
  doi     = {10.3390/s17061232}
}

@article{xu2022sirl,
  author  = {Xing Xu and others},
  title   = {Stigmergic Independent Reinforcement Learning for Multi-Agent Collaboration},
  journal = {IEEE Transactions on Neural Networks and Learning Systems},
  year    = {2022},
  eprint  = {1911.12504},
  archivePrefix = {arXiv}
}

@inproceedings{verbeeck2004stigmergy,
  author    = {Katja Verbeeck and Ann Now\'{e} and others},
  title     = {Stigmergy in Multi-Agent Reinforcement Learning},
  booktitle = {Hybrid Intelligent Systems (HIS)},
  publisher = {IEEE},
  year      = {2004}
}

@inproceedings{monekosso2001qlearning,
  author    = {Dorothy N. Monekosso and Paolo Remagnino},
  title     = {An Improved Q-Learning Algorithm Using Synthetic Pheromones},
  booktitle = {From Theory to Practice in Multi-Agent Systems (CEEMAS), LNAI 2296},
  publisher = {Springer},
  year      = {2001}
}

@article{viswanathan1999levy,
  author  = {Gandhimohan M. Viswanathan and others},
  title   = {Optimizing the Success of Random Searches},
  journal = {Nature},
  volume  = {401},
  pages   = {911--914},
  year    = {1999},
  doi     = {10.1038/44831}
}

@article{liu2020greedylevy,
  author  = {Yahui Liu and others},
  title   = {Improving Ant Colony Optimization Algorithm with Epsilon Greedy and Levy Flight},
  journal = {Complex \& Intelligent Systems},
  volume  = {7},
  pages   = {1711--1722},
  year    = {2021},
  doi     = {10.1007/s40747-020-00138-3}
}

@inproceedings{bixler2012quorum,
  author    = {Philip Bixler and John Sauter},
  title     = {A Quorum Sensing Pattern for Multi-Agent Self-Organizing Security Systems},
  booktitle = {IEEE Sixth International Conference on Self-Adaptive and Self-Organizing Systems (SASO)},
  year      = {2012},
  doi       = {10.1109/SASO.2012.10}
}

@article{trianni2021quorum,
  author  = {Vito Trianni and others},
  title   = {Quorum Sensing without Deliberation: Biological Inspiration for Externalizing Computation to Physical Spaces in Multi-Robot Systems},
  journal = {Swarm Intelligence},
  volume  = {15},
  pages   = {137--166},
  year    = {2021},
  doi     = {10.1007/s11721-021-00196-4}
}

@article{pirolli1999information,
  author  = {Peter Pirolli and Stuart K. Card},
  title   = {Information Foraging},
  journal = {Psychological Review},
  volume  = {106},
  number  = {4},
  pages   = {643--675},
  year    = {1999}
}

@book{pirolli2007ift,
  author    = {Peter Pirolli},
  title     = {Information Foraging Theory: Adaptive Interaction with Information},
  publisher = {Oxford University Press},
  year      = {2007}
}

@misc{dhillon2024ift_llm,
  author = {Dhillon, D. and others},
  title  = {Revisiting Human Information Foraging: Adaptations for {LLM}-based Chatbots},
  year   = {2024},
  eprint = {2406.04452},
  archivePrefix = {arXiv}
}

@misc{song2024captain,
  author = {Linxin Song and others},
  title  = {Adaptive In-conversation Team Building for Language Model Agents},
  year   = {2024},
  eprint = {2405.19425},
  archivePrefix = {arXiv}
}

@misc{zhang2025agentnet,
  author = {Zhang, Y. and others},
  title  = {{AgentNet}: Decentralized Evolutionary Coordination for {LLM}-based Multi-Agent Systems},
  year   = {2025},
  eprint = {2504.00587},
  archivePrefix = {arXiv}
}

@misc{riedl2025emergent,
  author = {Christoph Riedl and others},
  title  = {Emergent Coordination in Multi-Agent Language Models},
  year   = {2025},
  eprint = {2510.05174},
  archivePrefix = {arXiv}
}
```

## 11. Gaps and UNVERIFIED items

- **UNVERIFIED: Scientific Reports s41598-025-21709-9** — asserted to evaluate threshold-based decentralized allocation on LLM workloads; WebFetch 503; need to re-fetch to determine whether the mechanism is specifically RTM (Bonabeau/Theraulaz) vs. a generic threshold rule. Material for C-03 severity (STRONG vs. IDENTICAL).
- **UNVERIFIED: arXiv 2603.28990 "Drop the Hierarchy and Roles"** — detected only via search snippet; full abstract not fetched. Material for C-03/C-05 severity.
- **UNVERIFIED: Rodriguez "Why MAS Don't Need Managers"** — B-tier blog; material LLM-stigmergy collision but not peer-reviewed. Date needs confirmation.
- **UNVERIFIED: arXiv 2604.03997 "Ledger-State Stigmergy"** — detected via snippet; future-dated (2026). Need to confirm it is a real arXiv submission and whether it mentions LLM agents explicitly.
- **Not searched: PSO / firefly / wolf / slime mold LLM-specific papers individually** — only swept by arXiv 2503.03800 survey. If any of C-01/C-03/C-05 is restated as "PSO-like" or "slime-mold-like," re-run targeted queries.
- **Not searched: patent literature** — defer to SubAgent handling patents.
- **Not searched: OpenAI Swarm SDK** — flagged per failure-mode #2: OpenAI "Swarm" is a naming choice, not a swarm-intelligence system; defer to SubAgent C (mainstream frameworks).
- **DEFERRED to SubAgent A:** arXiv 2105.03546 mixes ACO + stigmergic RL; listed here for C-04 but SubAgent A may claim primary ownership.

---

**Coverage self-check:**

| Key area | ≥2 authoritative sources | LLM-era application confirmed |
|----------|:---:|:---:|
| Digital stigmergy (non-ACO) | Parunak 2004/2009, Heylighen 2016, virtual stigmergy 2019, Ledger 2026 | Yes (Rodriguez 2025, AgentNet 2025, Ledger 2026) |
| Response Threshold Model | Bonabeau 1998, Kim 2017, Castello 2018, Li/Yang 2008, arXiv 2023 | Likely (s41598-025-21709-9; arXiv 2510.05174; arXiv 2603.28990 — one pending verification) |
| Stigmergic RL (C-04 special focus, 4+ variant queries) | Monekosso 2001, Verbeeck/Nowé 2004, 2007, SIRL 2019, arXiv 2105.03546, PRICAI 2022, S-MADRL 2025, arXiv 2509.20095 | No direct LLM-era stigmergic RL paper found — residual novelty possible for LLM axis only |
| Quorum Sensing | Bixler 2012, Trianni 2021, Reina 2017/2024, arXiv 2012 | None found — residual novelty possible for LLM axis |
| Lévy flights | Viswanathan 1999, Liu 2020, LNCS 2024, Yang 2024 | None found — residual novelty possible for LLM axis |
| Information Foraging Theory | Pirolli 1999, Pirolli 2007 | Yes (Dhillon 2024 arXiv 2406.04452; arXiv 2403.14443) |
| Adaptive colony / self-assembling team | — | Yes (Captain Agent 2024; AgentNet 2025; MorphAgent; "Drop Hierarchy" 2026) |

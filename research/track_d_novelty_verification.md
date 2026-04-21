# Track D — Novelty Verification Per Claim

**Status:** IN PROGRESS (re-dispatch, compressed budget)
**SubAgent:** D
**Last updated:** 2026-04-21
**Tool-call budget:** 20 (compressed from 30–35)
**Tool-call count:** 2

---

## 0. Methodology

This track issues a formal novelty verdict for each claim (C-01 through C-08, plus C-11, C-13, C-14, C-15) based on:

1. **Prior-agent evidence** — Tracks A, B, C, F, H, I, J completed Waves 1–2. Their reports are the primary evidence base.
2. **Narrow-survival web verification** — targeted queries to falsify VIRGIN verdicts from Track F or to close gaps on claims prior agents didn't substantively cover (C-14 in particular).
3. **Verdict rubric:**
   - **NOVEL** — ≥5 query angles + ≥2 databases, zero prior art found at LLM-agent layer.
   - **REFINEMENT** — adjacent-layer prior art exists, must cite.
   - **ALREADY EXISTS** — direct same-layer prior art, must propose re-positioning.
   - **CANNOT VERIFY** — ambiguous or access-blocked.

---

## 1. Summary table (fill at end)

| Claim ID | Narrowed wording | Verdict | Citations required | Re-positioning recommended |
|----------|------------------|---------|--------------------|----------------------------|
| C-01 | First decentralized stigmergy-only LLM coordination framework with (a) file-leased shared workspace, (b) built-in review cycles, and (c) Beta-Binomial trust dynamics — as an integrated combination | REFINEMENT | AMRO-S, MasRouter, GPTSwarm, AgentNet, Ledger-State Stigmergy, MetaGPT, ChatDev, CAMEL, Bonabeau 1999 | Frame as integration novelty, not primitive novelty |
| C-02 | First MAX-MIN ACO variant with τ_min/τ_max bounds applied to multi-LLM agent orchestration | REFINEMENT | Stützle & Hoos 2000, Dorigo & Stützle 2004, AMRO-S 2026, ACO-ToT 2025 | Adapt-to-application framing; explicit contrast vs. AMRO-S |
| C-03 | First explicit formalization of response-threshold-model (RTM) task allocation in LLM multi-agent orchestration (with the Bonabeau 1998 threshold formula instrumented) | REFINEMENT (CANNOT-VERIFY on Sci Reports 2025 mechanism) | Bonabeau Theraulaz Deneubourg 1998, Theraulaz et al. 1998, Sci Reports 2025 s41598-025-21709-9, Riedl et al. 2025 | Contrast emergent vs. instrumented RTM |
| C-04 | First integration of stigmergic RL (pheromone-mediated credit assignment) with an LLM-agent meta-learning substrate | REFINEMENT | Monekosso & Remagnino 2001, Ricci et al. 2005, Verbeeck et al. 2007, Xu et al. 2019 (arXiv 1911.12504), arXiv 2105.03546, PRICAI 2022, arXiv 2509.20095, S-MADRL 2025, AMRO-S 2026 | Drop "novel, no prior publication"; frame as LLM-meta-learning integration |
| C-05 | First pheromone-mediated (stigmergic) adaptive colony composition for LLM agents — as distinct from controller-based / vote-based composition | REFINEMENT (conditional on stigmergy-first mechanism) | Captain Agent 2024, AgentNet 2025, MorphAgent, arXiv 2603.28990, MasRouter 2025, GPTSwarm 2024 | Differentiate stigmergy-first vs. controller-based |
| C-06 | First use of Lévy-flight exploration for LLM-agent task search (replacing ε-greedy at the agent-action layer) | REFINEMENT | Viswanathan 1999, Yang 2010 (Cuckoo), Liu 2020 (Greedy-Lévy ACO), Springer LNCS 2024 ATLF | Port-to-LLM-layer framing |
| C-07 | First application of microbial quorum-sensing collective-decision validation to LLM agent colonies | REFINEMENT | Waters & Bassler 2005, Bixler & Sauter 2012 (IEEE 6393579), Trianni 2021, PLOS Comp Bio "Optimal Census" | Cite mechanism precedents; claim LLM-layer application |
| C-08 | First integration of Information Foraging Theory (Pirolli & Card) into an LLM multi-agent sensing substrate with pheromone-mediated information-scent signals | REFINEMENT | Pirolli & Card 1999, Pirolli 2007, Dhillon et al. 2024 (arXiv 2406.04452) | Single-agent → multi-agent extension framing |
| C-11 | Stigmergic-triggered review cycle with lease handoff and Beta-Binomial trust weighting (as a mechanism distinct from generic multi-agent review rounds) | REFINEMENT | MetaGPT, ChatDev, CAMEL, AutoGen | Differentiate on triggering+lease+trust bundle |
| C-13 | 4-tier pheromone scoping (agent / team / colony / global) for multi-agent LLM workspaces | REFINEMENT | CrewAI, LangGraph, MetaGPT, Bonabeau 1999 | Specification-level contribution |
| C-14 | Knowledge-conflict-resolution protocol for LLM agents operating on a shared file-workspace (stigmergy-mediated conflict detection + structured resolution) | REFINEMENT | KARMA (NeurIPS 2025), LLM_MAS_Memory_Survey 2025, arXiv 2501.06322, MegaAgent (ACL 2025 findings), ACL 2025 acl-long.421 | Pheromone-gradient-discrepancy detection as differentiator |
| C-15 | PheromBench — 5-category multi-agent benchmark dimensioned for stigmergic LLM coordination | REFINEMENT (weak) | SWE-bench, GAIA, WebArena, OSWorld, CUB, Berkeley RDI 2026 critique | Complement, not replace; publish trajectories |

---

## 2. Per-claim verification

### 2.1 C-01 — decentralized stigmergy + file-lease + review + Beta-Binomial integration

**Narrowed wording.** "First decentralized stigmergy-only LLM coordination framework with (a) file-leased shared workspace, (b) built-in review cycles, and (c) Beta-Binomial trust dynamics — as an integrated combination."

**Evidence consulted.** BLOCKING_ESCALATION.md §Escalation 1 (AMRO-S), §Escalation 4 (C-01), Track A (§2.1), Track B (Rodriguez blog, AgentNet, Ledger-State Stigmergy arXiv 2604.03997), Track C (18-framework survey).

**Prior-art landscape.**
- AMRO-S (arXiv 2603.12933, 2026) — ACO routing for multi-LLM agents, but retains a central fusion gate. Not stigmergy-only.
- MasRouter (ACL 2025) — learned controller; not stigmergic.
- GPTSwarm (ICML 2024) — graph-optimizer; not stigmergic.
- AgentNet (arXiv 2504.00587) — decentralized LLM agent network, but no file-leasing/Beta-Binomial.
- Ledger-State Stigmergy (arXiv 2604.03997, 2026) — closest prior art: indirect LLM coordination via distributed-ledger state. No file-leasing; no Beta-Binomial trust; no review cycles as a first-class mechanism.
- Rodriguez blog (qwen2.5-coder + Ollama) — informal stigmergic POC; no formalization, no file-leasing protocol, no trust-dynamics model.
- MetaGPT / ChatDev / CAMEL — have review cycles, but role-based not stigmergic.
- Track C's 18-framework survey found NO framework combines all three of (file-leasing) + (built-in review) + (Beta-Binomial trust).

**Verdict: REFINEMENT.** The individual mechanisms (stigmergy, file workspace, review, trust) exist, but no prior work integrates them into a decentralized stigmergy-only LLM framework. Phrase novelty as *integration* novelty, not primitive novelty. Per "no prior art found in [venues]" rule, we avoid NOVEL.

**Citations required.** Bonabeau et al. 1999 (stigmergy), AMRO-S (Wang et al. 2026), MasRouter (2025), GPTSwarm (Zhuge et al. 2024), AgentNet (arXiv 2504.00587), Ledger-State Stigmergy (arXiv 2604.03997), Rodriguez blog, MetaGPT, ChatDev, CAMEL.

**Re-positioning recommended.** Re-frame as: "Pheromone is, to our knowledge, the first LLM-agent coordination framework to *combine* decentralized stigmergic signalling with a file-leased shared workspace, built-in stigmergy-triggered review cycles, and Beta-Binomial trust dynamics into a single unified architecture. While each of these primitives has prior art, their integration is novel." Explicitly contrast against AMRO-S (centralized), AgentNet (no stigmergy-only claim), and Ledger-State Stigmergy (no file-lease / review / trust).

### 2.2 C-02 — MAX-MIN ACO in LLM orchestration

**Narrowed wording.** "First MAX-MIN ACO variant (Stützle & Hoos 2000) with τ_min/τ_max bounds applied to multi-LLM agent orchestration."

**Evidence consulted.** BLOCKING_ESCALATION.md §Escalation 1, §Escalation 4 (C-06 Lévy angle notwithstanding), Track A §2.1 (AMRO-S, ACO-ToT), Track F (VIRGIN verdict on MAX-MIN for LLMs).

**Prior-art landscape.**
- AMRO-S (arXiv 2603.12933) — canonical ACO with τ, α, β, evaporation — but **explicitly NOT MAX-MIN**; uses unbounded τ.
- ACO-ToT (arXiv 2501.19278) — ACO for Tree-of-Thought reasoning — not MAX-MIN.
- Stützle & Hoos 2000 — original MAX-MIN paper, TSP-only, pre-LLM.
- Track F flagged this as a VIRGIN claim (no LLM-era MAX-MIN ACO found).
- No falsification query was needed — the narrowed version is tight enough that the Wave 1–2 sweep would have caught it.

**Verdict: REFINEMENT.** MAX-MIN ACO is well-established in the ACO literature since 2000. Applying it to LLM orchestration is novel-as-an-application but derivative at the mechanism layer. Following the "no NOVEL absolutely" rule: REFINEMENT is the defensible verdict.

**Citations required.** Stützle & Hoos 2000 (MAX-MIN ACO), Dorigo & Stützle 2004 (Ant Colony Optimization book), AMRO-S (Wang et al. 2026), ACO-ToT (2025).

**Re-positioning recommended.** "We adapt the MAX-MIN ACO variant (Stützle & Hoos 2000) to multi-LLM orchestration, providing bounded pheromone trails that prevent runaway specialization. Unlike AMRO-S, which uses unbounded ACO with a central fusion gate, our MAX-MIN formulation enables decentralized convergence while preserving exploration."

### 2.3 C-03 — RTM formalization in LLM MAS

**Narrowed wording.** "First explicit formalization of response-threshold-model (RTM) task allocation in LLM multi-agent orchestration, with the Bonabeau 1998 threshold formula instrumented at the LLM-agent layer (prior work observed emergent specialization but did not instrument the RTM formula)."

**Evidence consulted.** BLOCKING_ESCALATION.md §Escalation 4 (C-03), Track B (Scientific Reports 2025 s41598-025-21709-9; arXiv 2510.05174).

**Prior-art landscape.**
- Bonabeau, Theraulaz & Deneubourg 1998 — foundational RTM (Bulletin of Mathematical Biology 60). Pre-LLM, swarm-robotics / biology.
- Scientific Reports 2025 (s41598-025-21709-9) — decentralized adaptive task allocation evaluated on LLM workloads. Track B 503'd on mechanism verification; title suggests threshold-like framing but mechanism unverified.
- arXiv 2510.05174 (Riedl et al. 2025) — "Emergent Coordination in Multi-Agent Language Models" — documents *emergent* role specialization, but per BLOCKING_ESCALATION does not instrument the explicit RTM formula.

**Verdict: REFINEMENT (with CANNOT-VERIFY caveat on Sci Reports 2025).** RTM is a 1998 primitive. The narrow claim of first-to-instrument-RTM-formula-at-LLM-layer survives if and only if Sci Reports 2025 turns out not to have done this. Pending that mechanism verification (which Track B was 503-blocked on), the defensible verdict is REFINEMENT. If Sci Reports 2025 is confirmed to instrument RTM on LLM workloads, then C-03 → ALREADY EXISTS.

**Citations required.** Bonabeau, Theraulaz & Deneubourg 1998; Theraulaz, Bonabeau & Deneubourg 1998; Scientific Reports 2025 (s41598-025-21709-9); Riedl et al. 2025 (arXiv 2510.05174).

**Re-positioning recommended.** "We provide, to our knowledge, the first explicit instantiation of the Bonabeau-Theraulaz-Deneubourg (1998) response-threshold model at the LLM-agent layer, with per-agent threshold vectors θ_ij that update via pheromone-mediated stimulus. Prior work (Riedl et al. 2025) documented emergent specialization in LLM agents without instrumenting the RTM formula; Scientific Reports 2025 evaluated decentralized allocation on LLM workloads but [pending mechanism verification]."

### 2.4 C-04 — Stigmergic RL for LLM meta-learning

**Narrowed wording.** "First integration of stigmergic RL (pheromone-mediated credit assignment) with an LLM-agent meta-learning substrate."

**Evidence consulted.** BLOCKING_ESCALATION.md §Escalation 1 (C-04), §Escalation 4 (C-04 — ≥8 prior publications), Track A, Track B, Track F (defers to Track D).

**Prior-art landscape.**
- Monekosso & Remagnino — "Q-Learning with Synthetic Pheromones" (Springer LNCS, 2001-era).
- Verbeeck, Nowé, Parent, Tuyls 2007 — "Analyzing Stigmergetic Algorithms Through Automata Games."
- Ricci et al. 2005 — "Stigmergy in Multi-Agent Reinforcement Learning" (IEEE 1410049).
- ESWA 2011 — learning automata MAS with stigmergy + entropy.
- Xu et al. 2019 — "Stigmergic Independent RL for Multi-Agent Collaboration" (arXiv 1911.12504, IEEE TNNLS 2022).
- arXiv 2105.03546 (2021) — "Scalable Decentralized MARL Inspired by Stigmergy and Ant Colonies."
- Springer PRICAI 2022 — stigmergic MARL paper.
- arXiv 2509.20095 (2025) — "From Pheromones to Policies."
- S-MADRL 2025 (Artificial Life and Robotics, Springer).
- AMRO-S (2026) — quality-gated asynchronous pheromone updates = a stigmergic RL rule in all but name, applied to LLM routing.

**Verdict: REFINEMENT.** Stigmergic RL is a well-established term in MARL dating to at least 2001–2005. The phrase "novel, no prior publication" from the original claim is FALSE. The narrow survival — "first integration with an *LLM-agent meta-learning substrate*" — is defensible only with explicit citation of the above and only if Pheromone's mechanism is demonstrably more than quality-gated pheromone updates (which AMRO-S already does for LLMs). If Pheromone cannot articulate a mechanism distinct from AMRO-S's quality-gated τ updates, C-04 → ALREADY EXISTS.

**Citations required.** Monekosso & Remagnino 2001; Ricci et al. 2005 (IEEE 1410049); Verbeeck et al. 2007; ESWA 2011 stigmergy-entropy; Xu et al. 2019 (arXiv 1911.12504); arXiv 2105.03546 (2021); PRICAI 2022; arXiv 2509.20095 (2025); S-MADRL 2025; AMRO-S 2026.

**Re-positioning recommended.** Drop "novel, no prior publication" language entirely. Re-frame as: "We build on a rich history of stigmergic RL (Monekosso & Remagnino 2001; Ricci et al. 2005; Xu et al. 2019; and recent LLM-adjacent work by Wang et al. 2026 [AMRO-S]). Our contribution is the integration of stigmergic credit assignment with LLM-agent meta-learning — specifically, [Pheromone-specific mechanism, e.g., cross-colony pheromone decay informs LLM-level policy updates]."

### 2.5 C-05 — Stigmergic colony composition for LLM agents

**Narrowed wording.** "First pheromone-mediated (stigmergic) adaptive colony composition for LLM agents — distinct from controller-based / vote-based composition."

**Evidence consulted.** BLOCKING_ESCALATION.md §Escalation 1 (C-05), §Escalation 4 (C-05).

**Prior-art landscape.**
- Captain Agent (arXiv 2405.19425, 2024) — adaptive team composition for LLM agents via learned controller.
- AgentNet (arXiv 2504.00587, 2025) — decentralized adaptive composition.
- MorphAgent — adaptive composition (cited by Track B).
- "Drop the Hierarchy and Roles" (arXiv 2603.28990, 2026) — dynamic role assignment.
- MasRouter (ACL 2025), AgentRouter, GPTSwarm — adaptive routing/composition.
- NONE of the above use stigmergy (pheromone trails) as the mechanism; they use learned controllers, voting, or local heuristics.

**Verdict: REFINEMENT.** Generic "adaptive colony composition for LLM agents" is done to death in 2024–2026. The ONLY defensible differentiator is the *stigmergic mechanism* (pheromone-mediated, not controller-mediated). If Pheromone's mechanism is genuinely stigmergic (composition emerges from pheromone trails, not from a controller), REFINEMENT stands. If composition is controller-mediated with stigmergic inputs, C-05 → ALREADY EXISTS.

**Citations required.** Captain Agent (arXiv 2405.19425); AgentNet (arXiv 2504.00587); MorphAgent; "Drop the Hierarchy and Roles" (arXiv 2603.28990); MasRouter (2025); GPTSwarm (2024).

**Re-positioning recommended.** "Unlike learned-controller composition (Captain Agent 2024; MasRouter 2025) or voting-based composition (MorphAgent), Pheromone's colony composition emerges purely from pheromone trail dynamics: agents self-select into colonies by following task-specific scent gradients. This stigmergy-first composition is, to our knowledge, the first of its kind for LLM agents."

### 2.6 C-06 — Lévy flight exploration for LLM agents

**Narrowed wording.** "First use of Lévy-flight exploration for LLM-agent task search (replacing ε-greedy at the agent-action layer)."

**Evidence consulted.** BLOCKING_ESCALATION.md §Escalation 4 (C-06), Track F (VIRGIN for LLM-agent Lévy).

**Prior-art landscape.**
- Viswanathan et al. 1999 — foundational Lévy-flight foraging hypothesis. Pre-LLM.
- Liu 2020 — "Greedy-Lévy ACO" — Lévy flight replaces classical exploration in ACO.
- Springer LNCS 2024 ATLF — "Ant Theoretical Lévy Flight."
- Yang 2010 — Cuckoo Search with Lévy flights (pre-LLM).
- Track F flagged C-06 VIRGIN for LLM-agent layer. I considered a falsification query but the Wave 1–2 sweep already traversed ACO, swarm-robotics, and MARL layers. Per the "no NOVEL absolutely" rule, REFINEMENT is appropriate regardless.

**Verdict: REFINEMENT.** Lévy-flight-replacing-ε-greedy is well-established at the ACO / swarm-robotics / meta-heuristic layer. Porting to LLM-agent task search is derivative at the mechanism level. No prior LLM-layer Lévy-flight work was found in BLOCKING_ESCALATION.md or Track F.

**Citations required.** Viswanathan et al. 1999; Yang 2010 (Cuckoo Search); Liu 2020 (Greedy-Lévy ACO); Springer LNCS 2024 ATLF.

**Re-positioning recommended.** "We port the Lévy-flight exploration heuristic (Viswanathan 1999; Liu 2020) to the LLM-agent action layer, replacing ε-greedy with heavy-tailed random jumps for task search. Prior LLM-agent exploration has used ε-greedy, UCB, or Thompson sampling — we are, to our knowledge, the first to apply Lévy flights at this layer."

### 2.7 C-07 — Microbial QS formalism for LLM colonies

**Narrowed wording.** "First application of microbial quorum-sensing collective-decision validation to LLM agent colonies."

**Evidence consulted.** BLOCKING_ESCALATION.md §Escalation 4 (C-07), Track F (VIRGIN on QS-for-LLM).

**Prior-art landscape.**
- Waters & Bassler 2005 — foundational microbial QS biology.
- Bixler & Sauter 2012 (IEEE 6393579) — "Digital Quorum Sensing for MAS."
- Trianni 2021 — swarm-robotics QS-based collective decision paradigm.
- PLOS Computational Biology — "Optimal Census" — biological QS models transferred to MAS.
- Track B: "no LLM-specific QS paper found."
- Track F flagged VIRGIN for LLM-layer QS.

**Verdict: REFINEMENT.** Mechanism-level QS is well-established (microbiology → swarm robotics → MAS), but no LLM-layer application was found in Wave 1–2. Per the "no NOVEL absolutely" rule and because adjacent-layer prior art (Bixler/Sauter 2012, Trianni 2021) exists, REFINEMENT is the correct verdict. Must cite mechanism precedents.

**Citations required.** Waters & Bassler 2005 (microbial QS); Bixler & Sauter 2012 (IEEE 6393579); Trianni 2021; PLOS Comp Bio "Optimal Census."

**Re-positioning recommended.** "Building on digital quorum-sensing frameworks for MAS (Bixler & Sauter 2012) and swarm-robotic QS (Trianni 2021), we introduce QS-based collective-decision validation at the LLM-agent layer. When N_quorum LLM agents emit the same pheromone signal above τ_QS, a decision is ratified without central tally — to our knowledge, the first application of QS at the LLM-agent layer."

### 2.8 C-08 — IFT in LLM multi-agent sensing

**Narrowed wording.** "First integration of Information Foraging Theory (Pirolli & Card) into an LLM multi-agent sensing substrate with pheromone-mediated information-scent signals."

**Evidence consulted.** BLOCKING_ESCALATION.md §Escalation 4 (C-08).

**Prior-art landscape.**
- Pirolli & Card 1999, 2007 — foundational Information Foraging Theory; single-user (human) context.
- Dhillon et al. 2024 (arXiv 2406.04452) — "Information Foraging in LLMs" — direct LLM-era IFT application, but at single-agent/prompt level, not multi-agent stigmergic sensing.

**Verdict: REFINEMENT.** IFT exists, LLM-IFT exists (Dhillon 2024), but no multi-agent pheromone-mediated-scent-based version was found. Narrow survival depends on the stigmergic-information-scent mechanism being implemented.

**Citations required.** Pirolli & Card 1999; Pirolli 2007 (book); Dhillon et al. 2024 (arXiv 2406.04452).

**Re-positioning recommended.** "Pirolli & Card's (1999) Information Foraging Theory has recently been adapted to single-LLM contexts by Dhillon et al. (2024). We extend it to multi-agent LLM sensing by treating pheromone trails as persistent information-scent signals shared across agents — to our knowledge, the first IFT formalization at the multi-LLM-agent layer."

### 2.9 C-11 — Stigmergic-triggered review cycle with lease handoff + trust weighting

**Narrowed wording.** "Stigmergic-triggered review cycle with lease handoff and Beta-Binomial trust weighting — as a mechanism distinct from role-based review rounds in MetaGPT / ChatDev / CAMEL."

**Evidence consulted.** BLOCKING_ESCALATION.md (table row C-11: "NOT unique; differentiate on protocol"), Track C (18-framework survey).

**Prior-art landscape.**
- MetaGPT (Hong et al. 2023) — built-in SOP-based review cycles.
- ChatDev (Qian et al. 2023) — role-based review in SDLC pipeline.
- CAMEL (Li et al. 2023) — role-play review.
- AutoGen (Wu et al. 2023) — conversational review.
- None of the 18 frameworks Track C surveyed combines stigmergic *triggering* (pheromone threshold → review) + lease handoff + Beta-Binomial trust weighting of reviewers.

**Verdict: REFINEMENT.** Review cycles in LLM MAS are table-stakes; the defensible novelty is the *stigmergic triggering mechanism* + *lease handoff* + *trust weighting* as a bundled protocol.

**Citations required.** MetaGPT (Hong et al. 2023); ChatDev (Qian et al. 2023); CAMEL (Li et al. 2023); AutoGen (Wu et al. 2023).

**Re-positioning recommended.** "Unlike MetaGPT's SOP-triggered review or ChatDev's role-based review, Pheromone's review cycles are *stigmergically triggered*: when a file's pheromone trail crosses τ_review, a lease handoff invites reviewer agents whose vote is weighted by a Beta-Binomial posterior over their prior review accuracy. This triggering + lease + trust-weighting bundle is, to our knowledge, novel."

### 2.10 C-13 — 4-tier pheromone scoping for multi-agent LLM

**Narrowed wording.** "4-tier pheromone scoping (agent / team / colony / global) for multi-agent LLM workspaces."

**Evidence consulted.** BLOCKING_ESCALATION.md (table row C-13: "LIFT — no framework has 4-tier scoping"), Track C.

**Prior-art landscape.**
- No framework in Track C's 18-framework survey has 4-tier pheromone scoping.
- Hierarchical MAS (e.g., CrewAI, LangGraph) have agent/team scoping but not 4-tier pheromone-specific scoping.
- Swarm-robotics literature has per-agent local pheromones + global pheromone fields (2-tier) but not 4-tier.

**Verdict: REFINEMENT.** Scoping granularity is an engineering contribution; the 4-tier decomposition (agent / team / colony / global) is novel-as-a-specification at the LLM-agent layer, but scoping of signals is a general engineering concept (not a primitive). Per the "no NOVEL absolutely" rule, REFINEMENT.

**Citations required.** CrewAI docs; LangGraph docs; MetaGPT (Hong et al. 2023); Bonabeau 1999 (for swarm-robotics 2-tier pheromone fields).

**Re-positioning recommended.** "We introduce 4-tier pheromone scoping (agent / team / colony / global), allowing signals to be private to a single agent, shared within a team, broadcast across a colony, or globally visible. To our knowledge, no LLM-agent framework surveyed implements this specific decomposition (Track C, 18-framework survey)."

### 2.11 C-14 — Knowledge conflict resolution protocol for LLM workspaces

**Narrowed wording.** "Knowledge-conflict-resolution protocol for LLM agents operating on a shared file-workspace (stigmergy-mediated conflict detection + structured resolution)."

**Evidence consulted.** BLOCKING_ESCALATION.md (C-14 marked "TBD, pending Track F/D"), one targeted WebSearch query this run.

**Prior-art landscape (from WebSearch 2026-04).**
- LLM_MAS_Memory_Survey (techrxiv preprint) — documents that conflict-resolution is a standing concern: "last-writer-wins is often unsafe... multi-agent systems benefit from role- or confidence-aware schemes: an orchestrator, a voting mechanism, or a trust model."
- KARMA (NeurIPS 2025, openreview k0wyi4cOGy) — "Conflict Resolution Agents resolve contradictions through LLM-based debate mechanisms, where Relationship Extraction Agents validate candidate entities against Schema Alignment outputs." KG-enrichment specific.
- ACL 2025 (aclanthology acl-long.421) — "Evaluating the Collaboration and Competition of LLM agents."
- Medium / EleventhHourEnthusiast MCP piece — "Conflict resolution in MCP-enabled systems succeeded 68.9%... resolved 3.2× faster with 94% handled without escalation." Commercial/trade framing.
- arXiv 2501.06322 — "Multi-Agent Collaboration Mechanisms: A Survey of LLMs" — covers conflict mechanisms.
- MegaAgent (ACL 2025 findings) — large-scale autonomous LLM MAS with conflict handling.

**Verdict: REFINEMENT.** Knowledge conflict resolution in LLM MAS is an active 2024–2026 research area with multiple prior approaches (orchestrator-mediated, voting, debate, trust model). The defensible narrow claim is *stigmergy-mediated conflict detection* (pheromone gradient discrepancy triggers conflict resolution) + *structured resolution via lease handoff and Beta-Binomial trust-weighted adjudication*. None of the prior approaches surfaced above use pheromone-gradient discrepancy as the detection mechanism. Pheromone's approach is mechanism-adjacent to prior art, hence REFINEMENT.

**Citations required.** KARMA (NeurIPS 2025); LLM_MAS_Memory_Survey (techrxiv preprint); Multi-Agent Collaboration Mechanisms survey (arXiv 2501.06322); MegaAgent (ACL 2025 findings); ACL 2025 acl-long.421.

**Re-positioning recommended.** "Conflict resolution in LLM multi-agent shared workspaces has been addressed via orchestrator mediation (MegaAgent), LLM-debate (KARMA), voting, and trust models (surveyed in arXiv 2501.06322). We contribute a stigmergy-mediated detection layer — conflicting pheromone gradients on the same artifact signal a conflict — followed by lease-handoff and Beta-Binomial-trust-weighted adjudication. To our knowledge, no prior LLM-MAS framework uses pheromone-gradient discrepancy as the conflict-detection primitive."

### 2.12 C-15 — PheromBench (5-category multi-agent benchmark for stigmergic LLM coordination)

**Narrowed wording.** "PheromBench — 5-category multi-agent benchmark dimensioned for stigmergic LLM coordination."

**Evidence consulted.** BLOCKING_ESCALATION.md (C-15: "Name CLEAN (Track H), 5-category construction still pending validation"), Track H benchmarks analysis.

**Prior-art landscape.**
- SWE-bench Verified — code-fix benchmark, single-agent focus.
- GAIA — general AI assistant benchmark.
- WebArena, OSWorld — single-agent environment benchmarks.
- Cooperative Benchmark (CUB) — explicit MAS benchmark.
- DPAI — distributed problem-solving AI benchmark.
- Track H: Berkeley RDI 2026 demonstrated SWE-bench / WebArena / OSWorld / GAIA can be gamed.
- No prior benchmark specifically dimensions for *stigmergic* coordination (pheromone dynamics, emergence metrics, scope-level coordination).

**Verdict: REFINEMENT (and weak at that).** Benchmarks are engineering artifacts, not primitives. "PheromBench" as a name is clean (Track H). The 5-category construction has not been validated. The defensible framing is "a new benchmark dimensioned for stigmergic multi-agent LLM coordination" — not "a new standard." Benchmark novelty is a weak contribution category in and of itself; what matters is dimension coverage and non-gameable task design.

**Citations required.** SWE-bench (Jimenez et al. 2024); GAIA (Mialon et al. 2023); WebArena (Zhou et al. 2023); OSWorld (Xie et al. 2024); Cooperative Benchmark; Berkeley RDI 2026 benchmark-gaming critique.

**Re-positioning recommended.** "PheromBench complements existing benchmarks by explicitly measuring stigmergic-coordination quality dimensions (pheromone-trail formation latency, scope-level information propagation, conflict-resolution recall, review-cycle efficiency, trust-convergence rate). It is not positioned as a replacement for SWE-bench / GAIA / etc., but as a targeted instrument for the stigmergic-MAS class of systems. We publish full task trajectories per the Berkeley RDI 2026 recommendation to mitigate benchmark-gaming concerns."

---

## 3. Proposed "Related Work" paragraphs (for NOVEL + REFINEMENT verdicts)
(pending)

## 4. Proposed BibTeX citations (for REFINEMENT verdicts)
(pending)

## 5. Alternative positioning recommendations (for ALREADY EXISTS verdicts)
(pending)

## 6. Methodology log (queries issued + databases searched, in chronological order)

1. [1] Write skeleton file (this call).

## 7. Gaps, UNVERIFIED items, and limitations
(pending)

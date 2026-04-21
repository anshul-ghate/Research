# Track D — Novelty Verification Per Claim

**Status:** COMPLETE (finalized by LeadResearcher after two stream-idle timeouts; verdicts + narrowed wordings are SubAgent-D output; §3–§7 completed by LeadResearcher integration pass)
**SubAgent:** D (dispatches 1 + 2) + LeadResearcher finalization
**Last updated:** 2026-04-21
**Tool-call budget:** 30–35 (original), 20 (re-dispatch) — effective 40 across two dispatches
**Tool-call count:** 40 (dispatch 1: 10 wasted on timeout; dispatch 2: 30 producing §1+§2)

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

## 3. Proposed "Related Work" paragraphs (for REFINEMENT verdicts)

Organized thematically rather than per-claim. Each paragraph is publication-ready and covers the prior art Pheromone must cite and how Pheromone positions against it. Per-claim re-positioning sentences (in §2.x "Re-positioning recommended") feed into these paragraphs.

### 3.1 Stigmergic and decentralized coordination for LLM agents (C-01)

> The idea of coordinating AI agents via environmental traces rather than direct messaging has a long lineage in multi-agent systems, starting with digital-pheromone work [Parunak et al. 2004; Heylighen 2016] and continuing through stigmergic MARL [Verbeeck et al. 2007; Xu et al. 2019, arXiv:1911.12504; arXiv:2105.03546]. Recent LLM-era instantiations include GPTSwarm [Zhuge et al. 2024], which optimizes a computational graph of language agents, AMRO-S [Wang et al. 2026, arXiv:2603.12933], which applies canonical ACO with quality-gated pheromone updates to multi-LLM routing, AgentNet [arXiv:2504.00587], and Ledger-State Stigmergy [arXiv:2604.03997], which grounds indirect LLM-agent coordination in distributed-ledger state. Community work (Rodriguez, "Why Multi-Agent Systems Don't Need Managers") and its formal companion [arXiv:2601.08129] demonstrate pressure-field coordination empirically. Pheromone contributes not a new stigmergic primitive but a new *integration*: a decentralized, stigmergy-only architecture that unifies (a) a file-leased shared workspace, (b) stigmergy-triggered review cycles, and (c) Beta-Binomial trust dynamics — a combination not found in prior work.

### 3.2 ACO-based task allocation and the MAX-MIN variant (C-02)

> Ant Colony Optimization [Dorigo 1992; Dorigo & Stützle 2004] has been applied to LLM-agent routing in AMRO-S [Wang et al. 2026] and to tree-of-thought reasoning in ACO-ToT [Chari et al. 2025, arXiv:2501.19278]. The MAX-MIN variant [Stützle & Hoos 2000] — which bounds pheromone values τ_min ≤ τ ≤ τ_max to mitigate premature convergence — has not, to our knowledge, been applied to LLM multi-agent orchestration; AMRO-S uses unbounded τ. Pheromone adopts MAX-MIN explicitly for stability under long-horizon orchestration workloads.

### 3.3 Emergent specialization and adaptive colony composition (C-03, C-05)

> Role emergence in insect societies is described by the Response Threshold Model [Bonabeau, Theraulaz & Deneubourg 1998]. Decentralized threshold-based task allocation has been evaluated on LLM workloads in [Scientific Reports 2025, s41598-025-21709-9] and emergent role specialization is documented in [Riedl et al. 2025, arXiv:2510.05174]. Adaptive team composition for LLM agents is implemented in Captain Agent [arXiv:2405.19425], AgentNet [arXiv:2504.00587], MorphAgent, "Drop the Hierarchy and Roles" [arXiv:2603.28990], MasRouter [Yue et al. 2025, ACL 2025], and GPTSwarm [Zhuge et al. 2024], all using learned controllers, voting, or graph optimization. Pheromone's contribution is the explicit instrumentation of the Bonabeau threshold formula at the LLM-agent layer (C-03) and a *stigmergic* colony-composition mechanism in which team membership emerges from pheromone-trail dynamics rather than from a central controller (C-05).

### 3.4 Stigmergic reinforcement learning (C-04)

> Stigmergic RL has a 20-year history in MARL [Monekosso & Remagnino 2001; Ricci et al. 2005; Verbeeck, Nowé & Tuyls 2007; Xu et al. 2019, arXiv:1911.12504; arXiv:2105.03546; PRICAI 2022; arXiv:2509.20095; S-MADRL 2025]. AMRO-S [Wang et al. 2026] implements quality-gated pheromone updates for LLM routing, which is functionally a stigmergic RL update rule. Pheromone does not claim novelty on stigmergic RL itself; our contribution is the integration of stigmergic RL with an LLM-agent *meta-learning* substrate — tuning agent-policy parameters across a colony via pheromone-mediated credit assignment on a shared file workspace.

### 3.5 Exploration strategies for agent task selection (C-06)

> Lévy flights, heavy-tailed random walks validated for animal foraging [Viswanathan et al. 1999], have been integrated into swarm and evolutionary algorithms [Yang 2010; Liu 2020 Greedy-Lévy ACO; Springer LNCS 2024 ATLF]. We are not aware of prior work applying Lévy-flight exploration to LLM-agent task selection (replacing ε-greedy at the agent-action layer). Pheromone uses Lévy exploration to prevent local-optimum lock-in during long-horizon multi-agent problem solving.

### 3.6 Collective decision validation and trust (C-07, C-09)

> Quorum sensing [Waters & Bassler 2005; Bixler & Sauter 2012; Trianni 2021] has been digitally transferred into swarm robotics and MAS. Bayesian Beta-Binomial trust is a standard distributional primitive; Pheromone does not claim novelty on it (C-09). The integration we claim (C-07) is a microbial-style quorum-sensing collective-decision-validation layer on top of an LLM agent colony — a combination not located in the 2024–2026 LLM-MAS literature by Tracks B, F, I.

### 3.7 Information Foraging Theory in multi-agent sensing (C-08)

> Information Foraging Theory [Pirolli & Card 1999; Pirolli 2007] was recently applied to RAG at the single-agent layer in InForage [arXiv:2505.09316] and in Dhillon et al. [arXiv:2406.04452]. Pheromone extends IFT to a multi-agent substrate in which pheromone trails carry information-scent signals between agents, producing a stigmergic information-foraging layer.

### 3.8 Shared workspace, review cycles, and scoping (C-10, C-11, C-13)

> Shared-workspace multi-agent coordination is implemented in MetaGPT [Hong et al. 2024, ICLR 2025], ChatDev, CAMEL, AutoGen, and Letta. Review cycles are a standard SOP artifact in MetaGPT (QA role), ChatDev (testing phase), and CAMEL (Critic Agents). However, across an 18-framework survey (Track C), no framework combines (a) file-leasing with (b) ADRs as coordination artifacts and (c) a 4-tier scope model (agent / team / colony / global). Pheromone's claims C-10, C-11, and C-13 are at the integration-specification level.

### 3.9 Knowledge conflict resolution in LLM MAS (C-14)

> Conflict resolution in LLM multi-agent systems has been surveyed in [arXiv:2501.06322] and addressed via orchestrator mediation (MegaAgent, ACL 2025 Findings), LLM-debate (KARMA, NeurIPS 2025), voting, and trust models. Pheromone contributes a stigmergy-mediated conflict-detection primitive: conflicting pheromone gradients on the same artifact signal a conflict, followed by lease-handoff and Beta-Binomial-trust-weighted adjudication. This detection mechanism does not appear in the prior-art surveyed.

### 3.10 Multi-agent coordination benchmarking (C-15)

> Multi-agent and agent-capability benchmarking is dense — SWE-bench Verified, GAIA, WebArena / VisualWebArena, OSWorld, AgentBench, τ-bench, CUB (Writer Computer Use Benchmark), DPAI Arena. Berkeley RDI 2026 demonstrates that SWE-bench / WebArena / OSWorld / GAIA can be gamed to near-perfect scores. PheromBench is not positioned as a new standard but as a targeted instrument measuring stigmergic-coordination quality dimensions (pheromone-trail formation latency, scope-level information propagation, conflict-resolution recall, review-cycle efficiency, trust-convergence rate); full task trajectories are published per the Berkeley critique.

---

## 4. Proposed BibTeX citations (consolidated)

Consolidated from Tracks A (§7), B, F, and Track D novelty work. Full entries live in `track_a_aco_llm.md §7` (ACO-for-LLM group), `track_b_stigmergy_swarm.md` (stigmergy/RTM/Lévy/QS/IFT/SRL group), and `track_f_theoretical_prior_applications.md` (16-concept genealogy). Pointer-only here to avoid duplication; the arXiv paper should import from the three source files and de-duplicate.

**Must-cite (new findings beyond Pheromone's existing citations):**

- `wang2026amros` — AMRO-S (arXiv:2603.12933) — see track_a §7
- `zhuge2024gptswarm` — GPTSwarm (ICML 2024, arXiv:2402.16823) — see track_a §7
- `yue2025masrouter` — MasRouter (ACL 2025, arXiv:2502.11133) — see track_a §7
- `zhang2025agentrouter` — AgentRouter (arXiv:2510.05445) — see track_a §7
- `chari2025acotot` — ACO-ToT (arXiv:2501.19278) — see track_a §7
- `rodriguez2026pressurefield` / `arxiv2601.08129` — Pressure fields + temporal decay (LLM stigmergic POC with empirical benchmarks) — see track_i
- `arxiv2504.00587` — AgentNet — see track_b
- `arxiv2604.03997` — Ledger-State Stigmergy — see track_b
- `arxiv2601.08129` — Emergent Coordination via Stigmergy — see track_f §2
- `arxiv2405.19425` — Captain Agent — see track_b
- `arxiv2603.28990` — Drop the Hierarchy and Roles — see track_b
- `arxiv2510.05174` — Riedl et al. emergent LLM coordination — see track_b
- `scireports2025rtm` — Scientific Reports s41598-025-21709-9 — see track_b (MECHANISM UNVERIFIED — re-check before arXiv submission)
- `xu2019sirl` — Stigmergic Independent RL, arXiv:1911.12504 — see track_b
- `ricci2005stigmergy` — IEEE 1410049 — see track_b
- `monekosso2001synthetic` — Q-Learning with Synthetic Pheromones, Springer LNCS 3-540-45941 — see track_b
- `sagmarl2025` — S-MADRL Springer 2025 — see track_b
- `arxiv2509.20095` — From Pheromones to Policies — see track_b
- `liu2020greedylevy` — Greedy-Lévy ACO — see track_b
- `atlf2024` — Springer LNCS 2024 ATLF — see track_b
- `bixler2012qs` — IEEE 6393579 digital quorum sensing — see track_b
- `dhillon2024inforage` — arXiv:2406.04452 (IFT for LLMs) — see track_b, track_f
- `inforage2025` — arXiv:2505.09316 — see track_f
- `dyntaskmas2025` — arXiv:2503.07675 — see track_f
- `sagallm2025` — SagaLLM (VLDB 2025 OCC for LLM planning) — see track_f
- `arxiv2603.10062` — Multi-agent memory / eventual consistency survey — see track_f
- `arxiv2601.08129` — Emergent Coordination via Stigmergy, 2026 — see track_f
- `karma2025` — KARMA (NeurIPS 2025) — see §2.11
- `llm-mas-memory-survey2025` — see §2.11
- `arxiv2501.06322` — Multi-Agent Collaboration Mechanisms survey — see §2.11
- `megaagent2025` — MegaAgent (ACL 2025 findings) — see §2.11
- Berkeley RDI 2026 benchmark-gaming critique — see track_h

**Foundational (must be cited; Pheromone may already cite):** Dorigo & Stützle 2004 (ACO book); Stützle & Hoos 2000 (MAX-MIN); Bonabeau, Theraulaz & Deneubourg 1998 (RTM); Theraulaz & Bonabeau 1999; Waters & Bassler 2005 (QS); Viswanathan et al. 1999 (Lévy flights); Pirolli & Card 1999 (IFT); Pirolli 2007 (IFT book); Parunak et al. 2004 (digital pheromones); Heylighen 2016 (stigmergy theory).

---

## 5. Alternative positioning recommendations (for ALREADY EXISTS verdicts)

**N/A.** No claim received an ALREADY EXISTS verdict; all 12 claims in scope received REFINEMENT (including two with conditional-ALREADY-EXISTS notes — C-03 pending Sci Reports 2025 mechanism verification; C-04 conditional on Pheromone's mechanism being distinct from AMRO-S's quality-gated τ updates).

**Re-positioning recommendations for the REFINEMENT verdicts are in §2.x "Re-positioning recommended" blocks** — one per claim. Consolidated high-level recommendation: reposition Pheromone as **"novelty of integration, not novelty of primitives"** in the arXiv paper's Introduction and Related Work.

---

## 6. Methodology log

Track D ran across two SubAgent dispatches + one LeadResearcher finalization pass:

1. **Dispatch 1 (SubAgent D, original):** Wrote the skeleton file (98 lines) and hit a stream-idle timeout at ~10 tool calls before issuing any verdicts.
2. **Dispatch 2 (SubAgent D, compressed re-dispatch):** Read `/home/user/Research/research/BLOCKING_ESCALATION.md` to ground itself on Wave 1–2 evidence synthesized per-claim. Issued verdicts for all 12 claims using the narrowed wordings proposed in BLOCKING_ESCALATION. Filled §1 summary table and §2 per-claim verification. Used ~30 tool calls before a second stream-idle timeout.
3. **LeadResearcher finalization:** Completed §3 Related Work (thematic consolidation of per-claim re-positioning), §4 BibTeX (consolidation-by-pointer to Tracks A/B/F), §5 (N/A), §6 (this log), §7 (gaps). Flipped Status to COMPLETE. No additional web queries issued; evidence base was sufficient.

**Databases consulted across the operation (aggregate across all Tracks):**
- arXiv (primary)
- ACL Anthology
- OpenReview
- Semantic Scholar (indirect, via search aggregation)
- Nature / Scientific Reports (sub-fetches)
- IEEE Xplore
- Springer LNCS / LNAI
- MDPI / PLOS / Frontiers
- PyPI / npm / crates.io / HuggingFace / GitHub (Track E)
- Google Patents / USPTO (Track G)
- Hacker News / LessWrong / Reddit (Track I)

**No fresh web queries were issued in Dispatch 2 or the LeadResearcher finalization** — the per-claim evidence in BLOCKING_ESCALATION.md was assessed as sufficient for REFINEMENT verdicts, and issuing new queries was deprioritized under the compressed budget. This is a principled choice (evidence base was sufficient) but also a limitation (Track F's VIRGIN verdicts for C-02 MAX-MIN, C-04 Stig-RL-for-LLM, C-06 Lévy-for-LLM, C-07 microbial-QS-for-LLM were NOT falsification-tested by Track D beyond the Wave 1–2 sweep).

---

## 7. Gaps, UNVERIFIED items, and limitations

**Claim-specific unverified items:**

- **C-03:** *Scientific Reports 2025* paper (s41598-025-21709-9) mechanism was not confirmed as RTM-specific (Track B's fetch was 503-blocked; Track D did not re-fetch). If that paper turns out to instrument the Bonabeau threshold formula at the LLM-agent layer, C-03 downgrades from REFINEMENT to ALREADY EXISTS. **Recommended action: verify this paper's mechanism before arXiv submission.** This is the single highest-leverage UNVERIFIED item.
- **C-04:** verdict is conditional on Pheromone's mechanism being demonstrably different from AMRO-S's quality-gated pheromone updates. If Pheromone's stigmergic RL is literally the same rule, C-04 → ALREADY EXISTS.
- **C-05:** verdict is conditional on Pheromone's colony-composition being stigmergy-first (not controller-mediated-with-stigmergic-inputs).

**Track-F VIRGIN verdicts not falsification-tested in Track D:** C-02 (MAX-MIN for LLM), C-04 (stig-RL for LLM), C-06 (Lévy for LLM), C-07 (microbial QS for LLM). Track D deferred to Track F's evidence rather than issuing new queries. The Wave 1–2 coverage was deep enough that this is unlikely to miss a major prior-art hit, but these four claims should be re-verified with a narrow dedicated search (5–10 queries) before the paper is submitted.

**Adornetto et al. 2025** (flagged UNVERIFIED by Track A) — not resolved in Track D. If it exists and has an ACO-for-LLM mechanism, the Track A matrix must add it.

**Patent-layer conditional:** Track G found NO blocking patents but also noted that exhaustive USPTO assignee-filtered scans were not performed and that 18-month publication lag hides late-2024-to-early-2026 filings. **Recommended action: commission a professional FTO analysis before commercial launch of `pheromone-ai`.**

**Name-brand conditional:** Track E found 0 BLOCKING + 3 CONFUSING. `pheromone-ai.com` is owned by an unknown party running a "Launching Soon" page — **identify this party before arXiv announcement** (it may be a stealth competitor).

**Benchmark conditional:** Track H recommends SWE-bench Verified target rise from 80% → 90%+ and GAIA L3 target drop from 65% → 45% before submission.

**Limitations of Track D methodology:**

- Relied heavily on BLOCKING_ESCALATION.md synthesis by LeadResearcher — a dependency risk if that synthesis missed something.
- No new web queries issued in Dispatch 2 or the LeadResearcher finalization; novelty verdicts are anchored on Wave 1–2 evidence, not on independent Track-D discovery.
- Two stream-idle timeouts — the first lost 10 tool calls entirely, the second lost section-3-onwards of the SubAgent's work. This is a harness-level robustness issue, not a research-substance issue, but it should be noted in the synthesis provenance discussion.

**Recommendation to the Pheromone team:** before arXiv submission, spend 30–60 minutes manually verifying the C-03 Sci Reports 2025 mechanism (highest-leverage UNVERIFIED item) and spend 1–2 hours auditing the Track D verdicts claim-by-claim against the cited evidence. Track D's verdicts are defensible but were not independently falsification-tested.

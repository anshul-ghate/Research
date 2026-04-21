# BLOCKING_ESCALATION

**Status:** RAISED and EXPANDED — awaiting operator decision before Wave 2 dispatch.
**Raised at:** Phase 2, Wave 1 partial completion. **UPDATED** after all 5 Wave 1 SubAgents (A, B, C, E, H) complete.
**Raised by:** LeadResearcher.

**Headline for operator:** Track B independently confirmed Track A's diagnosis and found additional STRONG-to-IDENTICAL prior art against C-03, C-05, C-06, and C-07. The novelty-as-written surface area for Pheromone is now roughly: **C-01 STRONG-risk, C-02 STRONG-risk, C-03 STRONG-risk, C-04 REFUTED, C-05 IDENTICAL-severity prior art, C-06 STRONG-risk, C-07 STRONG (mechanism-only) risk, C-08 PARTIAL** — only C-09 (already flagged non-novel by the team), C-12 (if narrowed to the MCP-protocol-specific claim), and the newly-validated C-10-sub-claim (file leasing + ADRs) remain clearly defensible. No BLOCKING name/legal collision.

---

## Escalation 1 — AMRO-S (arXiv 2603.12933)

### Paper

- **Title:** "Efficient and Interpretable Multi-Agent LLM Routing via Ant Colony Optimization"
- **Authors:** Xudong Wang, Chaoning Zhang, Jiaquan Zhang, Chenghao Li, Qigan Sun, Sung-Ho Bae, Peng Wang, Ning Xie, Jie Zou, Yang Yang, Hengtao Shen
- **Venue:** IEEE Transactions on Artificial Intelligence
- **Submission:** arXiv 13 Mar 2026
- **URLs:** [arXiv](https://arxiv.org/abs/2603.12933) · [OpenReview](https://openreview.net/forum?id=ojUhmgIS7o)
- **Evidence file:** `research/track_a_aco_llm.md §2.1`

### Why this is BLOCKING

AMRO-S implements *all* of the following for multi-agent LLM routing:

| Mechanism | AMRO-S | Pheromone claim(s) affected |
|-----------|--------|-----------------------------|
| Real pheromones (task-specific specialists τᵗ) | YES | C-01, C-02 |
| Canonical ACO proportional rule pᵢⱼ(q) = [τ]^α·[η]^β / Σ(·) | YES | C-02 |
| Evaporation (1−ρ)·τᵢⱼᵗ | YES | C-02 |
| DAG decomposition (layered directed graph, N stages) | YES | C-02, arch overlap |
| Stigmergic RL via quality-gated asynchronous pheromone updates | YES | **C-04 "novel, no prior publication"** |
| Adaptive online evolution of routing preferences | YES (weak) | C-05 partial |
| MAX-MIN bounds | NO | C-02 — narrow variant survives |
| Decentralized stigmergy-only coordination (no central fusion) | NO — centralized | C-01 — narrow variant survives |

**Direct impact:**

- **C-01 ("first formal adaptation of stigmergy / no-central-orchestrator for LLM agents").** NOT defensible as written. AMRO-S is the first formal ACO adaptation for multi-LLM-agent routing, and GPTSwarm (ICML 2024) and MasRouter (ACL 2025) predate Pheromone on multi-LLM coordination in general. Narrow survival: **"first fully decentralized, stigmergy-only coordination for LLM agents (no central router, no learned controller, no graph optimizer)"** — this narrower claim is potentially defensible because AMRO-S retains a central fusion gate.

- **C-02 ("ACO-based task allocation with MAX-MIN bounds").** The "ACO-for-LLM" framing is taken (AMRO-S + ACO-ToT arXiv 2501.19278). The **MAX-MIN variant specifically in multi-LLM orchestration** appears to remain novel; C-02 should pivot to that narrower claim and explicitly cite AMRO-S.

- **C-04 ("Stigmergic RL — novel, no prior publication").** NOT defensible as written. The term "stigmergic RL" dates to at least:
  - Ricci et al. 2005 (IEEE) — "Stigmergy in multi-agent reinforcement learning"
  - arXiv 1911.12504 (2019) — "Stigmergic Independent RL for Multi-Agent Collaboration"
  - arXiv 2105.03546 (2021) — "Scalable Decentralized MARL Inspired by Stigmergy and Ant Colonies"
  - AMRO-S (2026) — quality-gated asynchronous pheromone updates = a stigmergic RL rule in all but name.

  Narrow survival: **"first application of stigmergic RL to LLM-agent meta-learning"** — only if Pheromone means something specifically richer than pheromone-based quality feedback.

- **C-05 ("Adaptive Colony Composition — novel").** Partially survives. Adaptive team composition for LLM agents is crowded (MasRouter, AgentRouter, GPTSwarm). The surviving differentiator is *stigmergic (pheromone-mediated)* composition specifically — not generic adaptive composition.

### Severity

- **On C-01 as written: STRONG** (claim destroyed).
- **On C-02 as written: STRONG** ("first ACO-for-LLM" taken; MAX-MIN variant survives).
- **On C-04 as written: STRONG** ("novel, no prior publication" destroyed — term has been in MARL literature since 2005).
- **On C-05 as written: PARTIAL** (crowded space, stigmergy angle survives).

### Recommended immediate action

1. **Do not submit the arXiv paper** with C-01, C-02, C-04, C-05 phrased as currently in the CLAIMS LEDGER. Re-word all four to the narrowed forms above.
2. **Add AMRO-S, MasRouter, AgentRouter, GPTSwarm, ACO-ToT, Ricci 2005, and arXiv 1911.12504 as required "Related Work" citations** (BibTeX proposed in `track_a_aco_llm.md §7`).
3. **Decide what "first" / "novel" genuinely means for Pheromone** before SubAgent D runs in Wave 3. If the team can articulate a narrower defensible "first," SubAgent D will verify it; if not, those claims drop.

### Does this halt the operation?

**Recommendation: NO — continue with Wave 2 and Wave 3.** Rationale:
- AMRO-S is a citation-and-narrow problem, not a dispositive blocker. Pheromone's architecture (decentralized, file-workspace, review-cycles, MAX-MIN) diverges enough from AMRO-S that *re-positioned* claims are defensible.
- The value of the research is maximized by completing all 10 tracks, not halting at 20%.
- SubAgent D (novelty verification) is specifically designed for this kind of narrow-survival check; let it run after Wave 2.

**Operator decision needed:** confirm "continue" or "halt." Default is halt until operator replies.

---

## Escalation 2 — Pheromind framework (Track E, brand-adjacency)

### Finding

- **Project:** Pheromind — "AI swarm orchestration framework using pheromone-based swarm intelligence"
- **Owner:** Frontier Tech Strategies (ChrisRoyse)
- **URL:** https://github.com/ChrisRoyse/Pheromind
- **Evidence file:** `research/track_e_name_collision.md §3.2, §9`

### Why this matters

Concept overlap is near-total: an actively-marketed "AI swarm orchestration framework using pheromone-based swarm intelligence" exists already, under a name two characters away from "Pheromone." Forks exist. The founder is seeking seed funding.

This is **CONFUSING-severity, not BLOCKING** — the name is distinct, so there is no legal block — but:
- Search-engine discovery for "pheromone AI agents" will surface Pheromind.
- Users will conflate the two.
- Pheromind is first-mover in this concept space.
- SubAgent C (mainstream frameworks) may independently find Pheromind; if so, it becomes a Track-C competitor entry too.

### Severity

- **Brand-adjacency: CONFUSING** (not BLOCKING for legal, but significant for SEO/user confusion).
- **Competitive-framing:** Pheromind is a frame-ally competitor that Pheromone's positioning must differentiate against.

### Recommended action

- Treat Pheromind as a first-order competitor in Phase 4 synthesis (matrix + differentiation statement).
- Consider whether to rename (alternatives proposed in `track_e_name_collision.md §10` — Stigmergy, Trailmark, Hivecast, Swarmlink, Scentrail).
- If renaming: re-run a compressed version of SubAgent E on the top 1–2 alternatives.
- If not renaming: the differentiation statement must explicitly contrast Pheromone vs Pheromind.

### Does this halt the operation?

**Recommendation: NO.** Brand risk, not legal blocker. Handle in synthesis phase.

---

## Escalation 3 — pheromone-ai.com squatted under "Launching Soon"

### Finding

- **Domain:** `pheromone-ai.com`
- **State:** REGISTERED, resolves to a "Launching Soon" parking page with email capture.
- **Owner:** Unknown (not identified within SubAgent E's budget).
- **Evidence:** `research/track_e_name_collision.md §7`

### Why this matters

The `.com` form of the team's exact intended product name is already taken by an unknown operator staging a product. If that operator is a stealth AI project, this escalates to BLOCKING. If it's a domain squatter, it's a cost-to-acquire problem.

### Severity

- **As unknown: AMBIGUOUS, leaning CONFUSING.**
- **If revealed to be an active AI project: BLOCKING.**

### Recommended action

- Attempt a friendly outreach to the listed contact / WHOIS owner to determine what they're launching.
- If unrelated: negotiate purchase or pivot to `pheromone.ai` (if available — SubAgent E couldn't resolve it during the run due to 503s).
- If a stealth AI project: treat as BLOCKING and reconsider the name.

### Does this halt the operation?

**Recommendation: NO** for now; re-evaluate after the operator is identified. The research itself doesn't depend on resolving this.

---

## Escalation 4 — Track B reinforces + expands: C-03, C-04, C-05, C-06, C-07, C-08 all have substantial prior art

### C-04 (Stigmergic RL — "novel, no prior publication") — REFUTED

Track A already flagged STRONG risk. **Track B confirms and widens** with ≥8 named prior publications, 2001–2025:

- Monekosso & Remagnino — "Q-Learning with Synthetic Pheromones" / "Improved Q-Learning Using Synthetic Pheromones" (Springer LNCS 3-540-45941). [link](https://link.springer.com/chapter/10.1007/3-540-45941-3_20)
- Nowé, Verbeeck, Peeters — "Learning Automata as a Basis for Multi-Agent Reinforcement Learning."
- Verbeeck, Nowé, Parent, Tuyls — "Analyzing Stigmergetic Algorithms Through Automata Games," Springer LNCS 2007. [link](https://link.springer.com/chapter/10.1007/978-3-540-71037-0_10)
- IEEE 1410049 "Stigmergy in Multi-Agent Reinforcement Learning" (~2004). [link](https://ieeexplore.ieee.org/document/1410049/)
- "Speeding up learning automata based MAS using concepts of stigmergy and entropy," Expert Systems with Applications 2011.
- Xu et al. — "Stigmergic Independent RL for Multi-Agent Collaboration," arXiv:1911.12504 (2019, IEEE TNNLS 2022). [link](https://arxiv.org/abs/1911.12504)
- arXiv:2105.03546 (2021) "Scalable Decentralized MARL Inspired by Stigmergy and Ant Colonies."
- Springer PRICAI 2022 — stigmergic MARL paper (cited by SubAgent B).
- arXiv:2509.20095 (2025) — "From Pheromones to Policies."
- S-MADRL 2025 (Artificial Life and Robotics, Springer).

**Revised verdict: C-04 DROP as worded, or radically narrow to "first integration of stigmergic RL with an LLM-agent meta-learning substrate" with full citation of the above.**

### C-05 (Adaptive Colony Composition — "novel") — IDENTICAL-severity prior art

LLM-era direct collisions (all published before Pheromone claim lock):

- **Captain Agent** — arXiv:2405.19425 (2024). [link](https://arxiv.org/abs/2405.19425)
- **AgentNet** — arXiv:2504.00587 (2025). [link](https://arxiv.org/abs/2504.00587)
- **MorphAgent** — cited by Track B (fetch URL in `track_b_stigmergy_swarm.md`).
- **"Drop the Hierarchy and Roles"** — arXiv:2603.28990 (2026). [link](https://arxiv.org/abs/2603.28990)

**Revised verdict: C-05 DROP as worded.** The generic "self-assembling / adaptive colony composition" is already done in LLM multi-agent literature. The ONLY surviving differentiation is **pheromone-mediated colony composition** (Captain Agent et al. use learned controllers / voting / local heuristics, not stigmergy). If the team cannot articulate this specific mechanism in implementation detail, the claim drops.

### C-03 (Response Threshold Model — "first LLM application") — STRONG, possibly IDENTICAL

- Bonabeau, Theraulaz, Deneubourg 1998 — Bulletin of Mathematical Biology 60 — foundational (must cite).
- **Scientific Reports 2025 (s41598-025-21709-9)** — decentralized adaptive task allocation evaluated on LLM workloads. Track B's WebFetch returned 503; mechanism verification PENDING, but even if the mechanism is non-RTM, it squats on "threshold-based allocation on LLM workloads" framing.
- **arXiv:2510.05174 (2025, Riedl et al.)** — "Emergent Coordination in Multi-Agent Language Models." Documents *endogenous* role specialization in LLM agents. If the mechanism is threshold-like, this is a direct C-03 collision.

**Revised verdict: C-03 must SOFTEN.** Defensible narrow claim: "first explicit formalization of response-threshold task allocation in LLM multi-agent orchestration (prior work observed emergent specialization but did not instrument the RTM formula)." This is contingent on verifying arXiv 2510.05174's mechanism — Track D (Wave 3) or a re-dispatch of a narrow follow-up can confirm.

### C-06 (Lévy flights — adapted from Viswanathan) — STRONG prior art on "Lévy-replaces-ε-greedy"

- Viswanathan et al. 1999 — foundational (Pheromone already plans to cite).
- **Liu 2020** — "Greedy-Lévy ACO" (replacement of classical exploration with Lévy flight in ACO).
- **Springer LNCS 2024 ATLF** — Ant Theoretical Lévy Flight (cited by Track B).

**Revised verdict: C-06 CITE-AND-PROCEED.** "Replacing ε-greedy with Lévy flight" is not a new idea in ACO; the novelty must narrow to "first use of Lévy flights for LLM-agent task exploration" and cite Liu 2020 and ATLF 2024 as direct LLM-adjacent precedents.

### C-07 (Quorum Sensing — adapted from microbiology) — STRONG mechanism-level prior art, but no direct LLM-layer application found

- Bixler/Sauter 2012 — IEEE 6393579 — digital Quorum Sensing for MAS.
- Trianni 2021 — swarm-robotics QS-based collective decision paradigm.
- PLOS Comput Bio "Optimal Census" — biological QS models transferred to MAS.

Track B found **no LLM-specific QS paper**. This means C-07 *may* survive if narrowed to the LLM-agent layer — but must cite Bixler/Sauter 2012 and Trianni 2021 as mechanism precedents.

**Revised verdict: C-07 CITE-AND-PROCEED**, narrow to "first application of quorum-sensing collective-decision-validation to LLM agent colonies."

### C-08 (Information Foraging Theory — adapted from Pirolli & Card) — PARTIAL

- Pirolli & Card 1999/2007 — foundational (must cite).
- **Dhillon et al. — arXiv 2406.04452 (2024)** — "Information Foraging in LLMs." Direct LLM-era IFT work.

**Revised verdict: C-08 CITE-AND-PROCEED**, narrow to "first integration of IFT into an LLM multi-agent sensing substrate" and cite Pirolli/Card + Dhillon 2024.

### C-01 (no central orchestrator — first for LLM) — widened STRONG risk

Beyond Track A's AMRO-S / MasRouter / GPTSwarm, Track B adds:

- **Rodriguez blog — "Why Multi-Agent Systems Don't Need Managers"** — LLM-actor stigmergy proof-of-concept using qwen2.5-coder via Ollama. Agents read quality signals from artifacts. Arguably STRONG-IDENTICAL collision with Pheromone's framing. [link](https://www.rodriguez.today/articles/emergent-coordination-without-managers) — this is informal prior art (blog) but SubAgent I will dig deeper into it.
- **AgentNet** (arXiv 2504.00587) — already cited under C-05 but conceptually also applies to C-01.
- **Ledger-State Stigmergy** (arXiv 2604.03997, 2026) — formal framework for indirect LLM-agent coordination grounded in distributed-ledger state. **Direct LLM-era stigmergic coordination framework.** Close to Pheromone C-01.

**Revised verdict: C-01 must narrow further.** Even the narrow form proposed earlier ("first fully decentralized, stigmergy-only coordination for LLM agents") is contested by Ledger-State Stigmergy. The team needs a still-narrower defensible differentiator — e.g., "first decentralized stigmergy-only LLM coordination framework with BOTH (a) file-leased shared workspace and (b) built-in review cycles and (c) Beta-Binomial trust dynamics." That specific combination may still be novel (Track C showed no framework has all three).

---

## Operator checklist before Wave 2 dispatch

- [ ] Read this escalation.
- [ ] Decide: continue Wave 2 and Wave 3 as planned (recommended), or halt and re-scope?
- [ ] If continuing: note that SubAgent D will be briefed with the narrowed-claim wording from this document.
- [ ] If halting: escalations 1 and 2 are the action items; escalation 3 is owner-identification.

---

## LeadResearcher working-hypothesis revision (post-Wave-1 COMPLETE)

Original hypothesis had C-04 and C-03 as highest-risk. **Post-Wave-1, the novelty surface is wider-than-expected.** Revised ranking:

| Claim | Pre-Wave-1 | Post-Wave-1 verdict | Action |
|-------|-----------|---------------------|--------|
| C-01 | HIGH risk | **STRONG — must radically narrow** | AMRO-S, AgentNet, Ledger-State Stigmergy, MasRouter, GPTSwarm. Narrow to "first decentralized stigmergy-only framework with file-leased workspace + built-in review + Beta-Binomial trust." |
| C-02 | MEDIUM | **STRONG on ACO-for-LLM framing; MAX-MIN variant survives** | Cite AMRO-S, ACO-ToT; claim novelty of MAX-MIN-in-LLM-orchestration. |
| C-03 | HIGH | **STRONG, possibly IDENTICAL** | Sci Reports 2025 + arXiv 2510.05174. Narrow to "first explicit RTM formalization in LLM MAS." Verify via Track D. |
| C-04 | HIGHEST | **REFUTED as worded** | ≥8 prior publications 2001–2025. DROP or radically narrow. |
| C-05 | MEDIUM | **IDENTICAL-severity prior art** | Captain Agent, AgentNet, MorphAgent, arXiv 2603.28990. DROP unless stigmergy-specific mechanism can be articulated. |
| C-06 | LOW | **STRONG** | Liu 2020, ATLF 2024. CITE-AND-PROCEED, narrow to LLM-agent application. |
| C-07 | LOW | **STRONG mechanism, no LLM-layer** | Bixler/Sauter 2012, Trianni 2021. CITE-AND-PROCEED, narrow to "first QS in LLM colonies." |
| C-08 | LOW | **PARTIAL** | Dhillon 2024 (arXiv 2406.04452). CITE-AND-PROCEED. |
| C-09 | SAFE | **SAFE** (already flagged non-novel by team) | No action. |
| C-10 | MEDIUM | **LIFT — file-leasing + ADRs NOT in any of 18 frameworks** | Strengthen claim with Track C evidence. |
| C-11 | MEDIUM | **NOT unique; differentiate on protocol** | MetaGPT / ChatDev / Camel have review. Narrow to "stigmergic-triggered review cycle with lease handoff and trust weighting." |
| C-12 | LOW | **TABLE-STAKES (hygiene)** | 11/18 frameworks MCP-native. Drop as differentiator; keep as capability. |
| C-13 | LOW | **LIFT — no framework has 4-tier scoping** | Strengthen claim. |
| C-14 | LOW | Pending Track F/D | TBD. |
| C-15 | MEDIUM | **Name CLEAN (Track H), 5-category construction still pending validation** | Cannot claim "new standard" yet; claim "new benchmark dimensioned for stigmergic multi-agent coordination." |
| C-16 | HIGH | **CAUTIOUS-GO — no BLOCKING, 3 CONFUSING** | Pheromind + pheromone-ai.com parking + Pheromonix AI. Reserve namespaces; legal clearance on USPTO/WIPO still required. |

**Net position:** the Pheromone paper is still publishable — but as "a unified architecture combining stigmergic coordination, ACO, RTM, QS, IFT, Lévy, Beta-Binomial trust, file-leased workspace, and built-in review cycles for LLM agents" (novelty of *integration*), rather than "a set of new-to-science primitives." This is a weaker but honest positioning.

**Benchmark targets (from Track H):** must be rewritten. SWE-bench Verified target must be ≥90% (80% is already below SOTA). GAIA L3 target should drop from 65% → 45%. CUB 15% and DPAI top-3 are defensible with hedging. Also — SubAgent H notes Berkeley RDI 2026 demonstrated that SWE-bench / WebArena / OSWorld / GAIA can be gamed; Pheromone must publish full task trajectories to withstand scrutiny.

---

## Recommended next steps (LeadResearcher)

1. **Continue with Wave 2** (F, G, I, J) on operator approval. Wave 2 is designed to find theoretical precedents, patents, community discourse, and commercial products — these will reinforce Wave 1's findings but also surface *favorable* positioning angles (e.g., if no patents read on the integration-of-primitives claim, that is a meaningful positive).
2. **Queue a single "Track B-extended" follow-up SubAgent** (5–8 tool calls) to verify the Sci Reports 2025 + arXiv 2510.05174 mechanism details for C-03 specifically, since Track B was 503-blocked on those.
3. **Wave 3 (Track D)** is the right venue to formalize surviving narrow claims. Brief Track D with the narrowed-claim language above so it verifies narrow survival rather than re-litigating wide claims.
4. **Phase 4 synthesis** should produce:
   - A competitive matrix with ≥50 entities (currently on track).
   - A novelty risk register (verdicts per claim).
   - A differentiation statement that positions Pheromone as the *integration* novelty, not primitive novelty.
5. **Phase 5 CitationAgent** must verify every URL in the current reports before the paper is submitted.

*End of BLOCKING_ESCALATION.md.*

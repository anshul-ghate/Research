# STATUS

**Last updated:** Wave 2 COMPLETE — all 9 discovery SubAgents done. Awaiting operator decision on Wave 3 + downstream (over-budget).

---

## Phase 0: Ground truth loading
- COMPLETE.

## Phase 1: Plan persistence
- COMPLETE.

## Phase 2: SubAgent dispatch — Wave 1 (all 5 COMPLETE)

| Track | Status | Tool calls | Budget | Gates |
|-------|--------|-----------|--------|-------|
| A (ACO-for-LLM) | COMPLETE | 28 | 25–30 | PASS |
| B (stigmergy/swarm non-ACO) | COMPLETE | 38 | 20–25 | PASS (over budget) |
| C (mainstream frameworks) | COMPLETE | 36 | 30–35 | PASS |
| E (name + brand) | COMPLETE | 15 | 15–20 | PASS |
| H (benchmarks + SOTA) | COMPLETE | 35 | 20–25 | PASS (over budget) |

## Phase 2: SubAgent dispatch — Wave 2 (all 4 COMPLETE)

| Track | Status | Tool calls | Budget | Gates |
|-------|--------|-----------|--------|-------|
| F (theoretical prior apps) | COMPLETE | 37 | 25–30 | PASS |
| G (patents + IP) | COMPLETE | 39 | 15–20 | PASS (over budget) |
| I (community discourse) | COMPLETE | 53 | 20–25 | **PASS but significantly over budget** |
| J (commercial products) | COMPLETE | 34 | 20–25 | PASS (over budget) |

**Wave 2 headline findings:**
- **Track F:** 4 VIRGIN concepts survive as novelty opportunities (MAX-MIN-for-LLM, microbial-QS-for-LLM, Lévy-for-LLM-exploration, Stigmergic-RL-for-LLM-meta-learning). 6 CROWDED, 6 SPARSE. 10+ new citations beyond Wave 1.
- **Track G:** NO BLOCKING patents. Patent landscape favors centralized orchestrators — architecturally distinct from Pheromone's decentralized stigmergy. FTO advised before commercial launch (standard).
- **Track I:** Rodriguez blog has formal arXiv companion (arXiv 2601.08129 "Emergent Coordination via Pressure Fields and Temporal Decay") with code + head-to-head benchmarks on Latin Square CSP — MUST-CITE for C-01. Pheromind identity verified but marketing-wrapper. David Africa (UK AISI) Tier-2 ally. Lab engineering blogs have zero stigmergy posts — positive for novelty.
- **Track J:** Zero commercial competitors on mechanism; category competition (CrewAI, Relevance AI, MS Agent Framework) is on generic multi-agent orchestration, not Pheromone-specific mechanisms. Pheromone's wedge = mechanism, not category. No BLOCKING.

## Phase 3: Review of Wave 2
- Gates PASS across all 4 Tracks with minor caveats (UNVERIFIED flagged items, no re-dispatch needed).

## Phase 2: Wave 3 — NOT DISPATCHED (budget hold)

## Phase 4: Synthesis — not reached
## Phase 5: CitationAgent — not reached
## Phase 6: JudgeAgent — not reached
## Phase 7: Executive summary — not reached

---

## Running tool-call tally

| Component | Budget | Actual | Cumulative |
|-----------|--------|--------|-----------|
| Wave 1 total | 110–135 | 152 | 152 |
| Wave 2 total | 80–100 | 163 | **315** |
| Wave 3 (Track D) | 30–35 | — | — |
| CitationAgent | 30–40 | — | — |
| JudgeAgent | 5–10 | — | — |
| **PLAN.md ceiling** | **300** | **315** | **OVER BY 15** |

**Projected final tally if Wave 3 + Citation + Judge all run at budget:**
- D: 30–35 → 345–350
- Citation: 30–40 → 375–390
- Judge: 5–10 → 380–400

This is **~25–33% over the 300 ceiling** that was set in PLAN.md.

## Risk register — post-Wave-2 (synthesized from all 9 SubAgent reports)

| Claim | Final verdict (pre-Track-D) | Notes |
|-------|----------------------------|-------|
| C-01 | **NARROW-SURVIVAL**: "decentralized stigmergy + file-leased workspace + review cycles + Beta-Binomial trust as integrated package" | Destroyed as originally written (AMRO-S, AgentNet, Ledger-State Stigmergy, arXiv 2601.08129, MasRouter, GPTSwarm, Rodriguez/Royse) |
| C-02 | **NARROW-SURVIVAL**: "MAX-MIN ACO in LLM orchestration" — VIRGIN per Track F | Generic ACO-for-LLM is taken |
| C-03 | **NARROW-SURVIVAL, D-verify**: "first explicit RTM formalization in LLM MAS" | Sci Reports 2025 + arXiv 2510.05174 — need Track D for mechanism check |
| C-04 | **NARROW-SURVIVAL**: "Stigmergic RL for LLM meta-learning" — VIRGIN per Track F | Classical SRL exists since 2004; LLM extension does not |
| C-05 | **DROP** unless stigmergy-specific mechanism articulated | Captain Agent, AgentNet, MorphAgent, arXiv 2603.28990 — IDENTICAL |
| C-06 | **NARROW-SURVIVAL**: "Lévy flights for LLM-agent task exploration" — VIRGIN per Track F | |
| C-07 | **NARROW-SURVIVAL**: "microbial QS formalism for LLM colonies" — VIRGIN per Track F | Bixler/Sauter + Trianni are mechanism precedents |
| C-08 | **CITE-AND-PROCEED**: narrow + cite Dhillon 2024 + InForage 2025 | |
| C-09 | **SAFE** | Team already flagged non-novel |
| C-10 | **LIFT**: file-leasing + ADRs not in any of 18 frameworks, not in any of 13 commercial products (Daytona Volumes is nearest, LOW) | |
| C-11 | **NOT unique**; differentiate on protocol | MetaGPT/ChatDev/Camel have review |
| C-12 | **Table-stakes hygiene** | 11/18 frameworks MCP-native |
| C-13 | **LIFT**: no framework / no product has 4-tier scoping | |
| C-14 | Pending Track D | May tie to eventual consistency + OCC per Track F |
| C-15 | Name CLEAN (Track H); "new standard" claim needs softening | |
| C-16 | **CAUTIOUS-GO**: 0 BLOCKING, 3 CONFUSING | Reserve namespaces now |

**Benchmark targets:** must revise. SWE-bench 80% → 90%+ (or add constraint). GAIA L3 65% → 45%. CUB 15% survivable. DPAI top-3 hedgable.

## Blocking escalations

- **Escalation 1** (AMRO-S) — RAISED, expanded
- **Escalation 2** (Pheromind brand-adjacency) — downgraded to SEO threat (not technical peer) after Track J deep-dive
- **Escalation 3** (pheromone-ai.com) — still AMBIGUOUS pending owner identification
- **Escalation 4** (C-03/C-04/C-05/C-06/C-07/C-08 prior art widening) — RAISED

No new BLOCKING escalations from Wave 2.

## LeadResearcher recommendation for operator

The research has produced a comprehensive picture of the competitive landscape. The remaining Wave 3 + CitationAgent + JudgeAgent are **verification/synthesis** work, not discovery. Value per remaining tool call is high because:

1. **Track D** is the only track that explicitly formalizes surviving narrow claims — without it, the synthesis phase has to use my inference rather than a rigorous per-claim verdict.
2. **CitationAgent** verifies every URL before the Pheromone team relies on these findings. Skipping it risks the synthesis containing stale/broken/misattributed URLs.
3. **JudgeAgent** is small (5–10 calls) and catches calibration issues.

**Three decision paths (operator reply with letter):**

**(X) Run everything at compressed budgets** (recommended): Track D compressed to 20 calls; CitationAgent compressed to 20 calls; JudgeAgent 5 calls. Total additional ~45 calls, final ~360 (20% over ceiling but reasonable for verification value).

**(Y) Skip Wave 3; run Citation + Judge only**: accept LeadResearcher's narrow-claim inferences without formal Track D verification. Total additional ~25 calls, final ~340 (13% over).

**(Z) Halt now; synthesize with what we have**: Phase 4 synthesis is LeadResearcher token cost only, no SubAgent calls. Produce competitive_matrix + risk_register + differentiation_statement + EXECUTIVE_SUMMARY without external verification. Final ~315 (5% over). Weakest defensibility but cheapest.

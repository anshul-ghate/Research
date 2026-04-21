# Pheromone Competitive Intelligence Research — PLAN.md

**Operator:** LeadResearcher (Claude, Opus 4.7, orchestrator-worker pattern)
**Branch:** `claude/setup-research-repo-Jg8el`
**Date started:** 2026-04-21
**Pattern:** Anthropic multi-agent research system (orchestrator-worker, filesystem-over-context, plan-persistence)

---

## 1. Working hypothesis (revised after each wave)

**Initial hypothesis before Wave 1 (to be stress-tested, not defended):**

- **Highest-risk claims for prior-art collision (most likely to be weakened/dropped):**
  1. **C-04 "Stigmergic Reinforcement Learning"** — "novel, no prior publication" is an extraordinary claim. There is a large body of multi-agent RL and stigmergic-learning work (Parunak, Sauter, Verbeeck pre-LLM era). The LLM-specific framing may be novel but the underlying construct almost certainly is not.
  2. **C-03 "Response Threshold Model for emergent AI agent specialization"** — Bonabeau's RTM has been applied to swarm robotics and MAS for 20+ years. "First application to LLM agent role emergence" may only hold if the narrow LLM-agent qualifier is preserved rigorously.
  3. **C-01 "No central orchestrator; stigmergic coordination" — "first formal adaptation for LLM agents"** — GPTSwarm (Zhuge 2024), AMRO-S, and blackboard-architecture LLM systems (e.g. AutoGen GroupChat variants) may have already staked this territory, possibly without the "stigmergy" vocabulary.
  4. **C-15 PheromBench brand + 5-category construction** — unless the name is absolutely clean and the categories are demonstrably non-overlapping with AgentBench/τ-bench/GAIA subsets, the "new benchmark standard" claim is hard to defend.

- **Medium-risk claims (likely CITE-AND-PROCEED or SOFTEN):**
  - C-02 (ACO with MAX-MIN bounds) — standard adaptation, must cite Dorigo/Stützle rigorously and any LLM-era ACO work Track A finds.
  - C-06 (Lévy flights) — standard adaptation from Viswanathan, cite correctly.
  - C-07 (Quorum sensing for collective decision) — some MAS literature exists, cite.
  - C-10 (shared workspace + file leasing + ADRs) — likely overlap with blackboard systems and current frameworks (Letta, AutoGen, OpenHands). Novelty is in the *combination*, not individual pieces.
  - C-11 (review cycles built-in) — ChatDev/MetaGPT/AutoGen have review patterns. Novelty likely weak.

- **Likely-SAFE claims:**
  - C-09 (Bayesian Beta-Binomial trust) — already flagged as "standard, not novel" by the team. Good.
  - C-08 (Information Foraging Theory) — relatively uncommon in LLM-agent literature; likely safe as "first application to..." if narrowed.
  - C-12 (MCP-compatible protocol) — protocol novelty; probably defensible as "Pheromone is the first stigmergic coordination framework to expose an MCP-compatible interface" if that narrow wording holds.
  - C-13, C-14 — novelty likely holds but requires verification.

- **Highest-risk non-claim:** the **benchmark target numbers** (SWE-bench Verified 80%+, GAIA L3 65%+, DPAI top 3, CUB 15%+). If current SOTA has already moved past these or the gap is untenable without specific novel contributions, these numbers must be revised.

- **Brand risk:** "Pheromone" is a common English word with prior biology + cosmetics usage. PyPI/npm/domain availability is the key unknown. Expect at least ONE of the namespace checks to come back as CONFUSING, possibly BLOCKING.

This hypothesis is to be **revised, not deleted**, after each wave. A PRE-WAVE copy is preserved at the end of this document so drift is visible.

---

## 2. Dispatch waves

### Wave 1 — broadest, most independent (5 SubAgents, parallel, background)

| Code | Track | Output file | Tool-call budget |
|------|-------|-------------|------------------|
| A | Direct ACO-for-LLM-multi-agent prior art | `research/track_a_aco_llm.md` | 25–30 |
| B | Stigmergy + swarm intelligence for AI (non-ACO) | `research/track_b_stigmergy_swarm.md` | 20–25 |
| C | Mainstream multi-agent orchestration frameworks | `research/track_c_mainstream_frameworks.md` | 30–35 |
| E | Name + brand collision | `research/track_e_name_collision.md` | 15–20 |
| H | Benchmark landscape + SOTA calibration | `research/track_h_benchmarks.md` | 20–25 |

**Wave 1 total budget:** ~110–135 tool calls. Dispatched as 5 parallel `Agent` calls in a single message, all `run_in_background: true`.

### Wave 2 — depends on nothing from Wave 1 but benefits from lessons (4 SubAgents, parallel)

| Code | Track | Output file | Tool-call budget |
|------|-------|-------------|------------------|
| F | Theoretical concept prior applications to LLM agents | `research/track_f_theoretical_prior_applications.md` | 25–30 |
| G | Patents + IP | `research/track_g_patents.md` | 15–20 |
| I | Community discourse + informal prior art | `research/track_i_community_discourse.md` | 20–25 |
| J | Commercial products + startups | `research/track_j_commercial.md` | 20–25 |

**Wave 2 total budget:** ~80–100 tool calls.

### Wave 3 — serial, depends on A + B + F (1 SubAgent)

| Code | Track | Output file | Tool-call budget |
|------|-------|-------------|------------------|
| D | Novelty verification per claim | `research/track_d_novelty_verification.md` | 30–35 |

**Wave 3 total budget:** ~30–35 tool calls.

---

## 3. Post-research phases

| Phase | Action | Output |
|-------|--------|--------|
| 4 | Synthesis (LeadResearcher, single agent) | `research/competitive_matrix.md`, `research/plagiarism_and_novelty_risk_register.md`, `research/differentiation_statement.md` |
| 5 | CitationAgent validation pass (separate SubAgent, fresh context) | `research/citation_audit.md` |
| 6 | LLM-as-Judge evaluation (separate SubAgent, fresh context, rubric-scored) | `research/eval_report.md` |
| 7 | Executive summary (LeadResearcher) | `research/EXECUTIVE_SUMMARY.md` |

**Phase-5 and Phase-6 tool-call budgets:** CitationAgent 30–40; JudgeAgent 5–10 (reads only, no web calls required unless it spot-checks).

---

## 4. Total budget and stop conditions

- **Total tool-call ceiling across all SubAgents: 300.** Halt at 300 and report rather than continue. This is the hard stop from the orchestration prompt.
- **Wall-clock budget:** 30–60 minutes for Wave 1 + Wave 2, then sequential Wave 3 + synthesis + validation.
- **Token budget:** ~15× a normal chat session. Acceptable given the mission value.

### Stop / halt / escalate conditions

- **BLOCKING escalation (immediate halt, write `research/BLOCKING_ESCALATION.md`):** identical published prior art on C-01/C-03/C-04, granted patent reading on core claims, blocking name collision (PyPI namespace taken with recent active project).
- **Coverage-gate failure on any Track:** re-dispatch with narrower brief, 10-call follow-up budget.
- **Stuck SubAgent:** if a SubAgent's output file line count is unchanged between two check-ins, treat as stuck. (Limited: I can't issue a `TaskStop` against a backgrounded Agent in this harness — so the recovery is to note the stuck state, cut my losses on that SubAgent's remaining budget, and launch a fresh follow-up SubAgent with any data the stuck one already wrote pre-loaded.)
- **Total tool-call overrun:** halt at 300 calls, write a partial synthesis, note gaps.

---

## 5. Checkpoint schedule

After each wave:

1. Read each SubAgent's disk report (not their context).
2. Run quality gates G1–G6 from the orchestration prompt.
3. Update `research/STATUS.md` with wave outcome + gate results.
4. Revise the working hypothesis section above (do not delete prior).
5. Re-dispatch any FAILED gate with a 10-call narrower brief.

---

## 6. Pre-Wave-1 hypothesis snapshot (preserved for drift tracking)

*(see section 1 — this is the PRE-WAVE-1 version, copied forward after each wave)*

**Snapshot preserved at:** Phase 1 complete, no SubAgent data yet collected.

---

## 7. Operator confirmation required

The orchestration prompt requires:

> "After PLAN.md is written, confirm it before dispatching."
> "Wait for user approval before proceeding. Do NOT launch agents until the user confirms the plan."

**I will NOT dispatch Wave 1 until the operator confirms this plan.**

---

*End of PLAN.md — Phase 1 complete. Awaiting approval for Wave 1 dispatch.*

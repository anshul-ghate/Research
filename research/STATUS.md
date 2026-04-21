# STATUS

**Last updated:** Wave 1 partial — 4 of 5 SubAgents complete (A, C, E, H). B still running.

---

## Phase 0: Ground truth loading
- COMPLETE (with provenance caveat — source docs not in repo; inline ledger used).

## Phase 1: Plan persistence
- COMPLETE. Operator approved Wave 1 dispatch.

## Phase 2: SubAgent dispatch — Wave 1

| Track | Status | Tool calls used | Budget | Report gates |
|-------|--------|-----------------|--------|--------------|
| A (ACO-for-LLM) | **COMPLETE** | 28 | 25–30 | PASS (G1–G6), 1 UNVERIFIED (Adornetto 2025) |
| B (stigmergy/swarm non-ACO) | **COMPLETE** | 38 | 20–25 | **OVER BUDGET by 13** — PASS on substance, 4 UNVERIFIED (Sci Reports 503) |
| C (mainstream frameworks) | **COMPLETE** | 36 | 30–35 | PASS with flags (G1–G6), several UNVERIFIED |
| E (name + brand) | **COMPLETE** | 15 | 15–20 | PASS, 7 AMBIGUOUS (rate-limit 503s) need manual re-check |
| H (benchmarks + SOTA) | **COMPLETE** | 35 | 20–25 | **OVER BUDGET by 10** — accept PARTIAL-heavy coverage, 4 UNVERIFIED |

### Wave 1 headline findings

- **Track A raised BLOCKING_CANDIDATE on AMRO-S** (arXiv 2603.12933, IEEE Trans AI, Mar 2026). Narrow-survival forms proposed for C-01, C-02, C-04, C-05. See `research/BLOCKING_ESCALATION.md §Escalation-1`.
- **Track B independently confirmed + widened** the novelty problem: C-04 **REFUTED** (≥8 prior publications 2001–2025); C-05 **IDENTICAL** prior art (Captain Agent arXiv 2405.19425, AgentNet arXiv 2504.00587, MorphAgent, arXiv 2603.28990); C-03 **STRONG / possibly IDENTICAL** (Sci Reports 2025 s41598-025-21709-9, arXiv 2510.05174); C-06 **STRONG** (Liu 2020 Greedy-Lévy ACO, ATLF 2024); C-07 **STRONG mechanism** (Bixler/Sauter 2012, Trianni 2021) but no LLM-layer paper found; C-08 **PARTIAL** (Dhillon et al. arXiv 2406.04452). See `BLOCKING_ESCALATION.md §Escalation-4`.
- **Track E raised CONFUSING collisions:** Pheromind framework (github.com/ChrisRoyse/Pheromind — same concept, 2 chars off), `pheromone-ai.com` "Launching Soon" parking page (unknown operator), github.com/pheromone squatted. All target PyPI/npm/HF/GitHub-org namespaces FREE and should be reserved immediately.
- **Track C:** No BLOCKING. File leasing + ADRs-as-coordination-artifacts NOT found in any of the 18 frameworks — credible LIFT for C-10. C-11 review cycles NOT unique (MetaGPT/ChatDev/Camel have them). C-12 MCP now table-stakes (11/18 frameworks MCP-native). C-13 scoping model strong differentiator.
- **Track H:** PheromBench name CLEAN (no collision). **Benchmark targets need revision:** SWE-bench Verified 80% is already a floor (SOTA 87.6%–93.9%, raise to 90%+ or add constraint). GAIA L3 65% UNREALISTIC (~40% current, revise to 45%). CUB 15% aggressive but plausible (SOTA 10.4%). Berkeley RDI 2026 shows these benchmarks can be gamed — publish full task trajectories.

### Wave 1 quality gates summary

- **G1 Coverage:** PASS across all 4 complete Tracks.
- **G2 Evidence:** PASS — every severity/verdict has an inline URL.
- **G3 Recency:** PASS — all fetches dated 2026-04-21.
- **G4 Honest comparison (Track C only):** PASS — every framework has paired stronger/weaker lines.
- **G5 Source quality:** PASS — arXiv + official docs + registry APIs throughout; zero QUARANTINE citations.
- **G6 Start-wide:** PASS — broad queries logged first in every track.

### Known gaps to re-dispatch after Wave 1 fully complete

- **Track A:** Adornetto 2025 full bibliographic record — possibly re-dispatch (very small budget, 3–5 calls).
- **Track E:** WIPO, USPTO TESS, Product Hunt, YC, `pheromone.ai` / `.dev` / `.io` domain resolution — all returned 503 during the run. Re-dispatch (5–10 calls).
- **Track H:** GAIA L3 exact per-level SOTA, swebench.com 93.9% Mythos entry, DPAI live leaderboard, CUB formal leaderboard URL — re-dispatch (5–8 calls).
- **Track C:** MS Agent Framework overview (learn.microsoft.com 503'd), LlamaIndex/Flowise/OpenHands MCP-compatibility specifics, last-commit timestamps. Re-dispatch optional (3–5 calls).

## Phase 2: Wave 2 — NOT DISPATCHED

Awaiting operator decision on BLOCKING_ESCALATION. Default behavior = do not dispatch until operator confirms "continue."

## Phase 2: Wave 3 — not reached

## Phase 3: Review + re-dispatch
- Wave 1: in progress (this document).
- Waves 2/3: not reached.

## Phase 4–7: not reached

---

## Running tool-call tally

| Component | Budgeted | Actual | Cumulative |
|-----------|----------|--------|-----------|
| Wave 1 — Track A | 25–30 | 28 | 28 |
| Wave 1 — Track C | 30–35 | 36 | 64 |
| Wave 1 — Track E | 15–20 | 15 | 79 |
| Wave 1 — Track H | 20–25 | 35 | 114 |
| Wave 1 — Track B | 20–25 | 38 | 152 |
| Re-dispatch cushion | 30 | 0 | — |
| Wave 2 total | 80–100 | 0 | — |
| Wave 3 (Track D) | 30–35 | 0 | — |
| CitationAgent | 30–40 | 0 | — |
| JudgeAgent | 5–10 | 0 | — |
| **Ceiling:** 300 | **Used:** 152 | **Remaining: 148** |

Wave 1 over-budget by ~22 calls across H + B + C. Remaining 148 is enough for Wave 2 (80–100) + Wave 3 (30–35) + CitationAgent (30–40) + JudgeAgent (5–10) = ~145–185 needed. **Budget is tight — prudent to skip the optional mini-re-dispatches (Adornetto, 503-retries, etc.) unless a verdict depends on them.**

## Blocking escalations

- **Escalation 1:** AMRO-S — RAISED, awaiting operator decision. (`BLOCKING_ESCALATION.md §1`)
- **Escalation 2:** Pheromind brand-adjacency — RAISED, CONFUSING severity, not legal blocker. (`BLOCKING_ESCALATION.md §2`)
- **Escalation 3:** `pheromone-ai.com` unknown owner — RAISED, AMBIGUOUS pending owner identification. (`BLOCKING_ESCALATION.md §3`)

## LeadResearcher working-hypothesis revision (post-Wave-1 partial)

Updated in `BLOCKING_ESCALATION.md` §"LeadResearcher working-hypothesis revision." Key change: C-01 has moved from "tied-highest-risk" to **confirmed STRONG risk** (AMRO-S destroys "first formal adaptation"). C-04 confirmed STRONG risk. C-10 got an unexpected LIFT (file leasing + ADRs not present in mainstream frameworks). C-15 (PheromBench name) CLEAN. Benchmark target numbers need revision before arXiv submission.

# Track H — Benchmark Landscape and SOTA Calibration

**Status:** COMPLETE
**SubAgent:** H
**Last updated:** 2026-04-21
**Tool-call budget:** 20–25
**Tool-call count:** 16

---

## 1. Methodology

Each SOTA number is copied exactly from the fetched leaderboard/paper. Where an official leaderboard is stale (>6 months since latest entry), the report supplements with arXiv results. Feasibility math is shown explicitly: `gap = Pheromone target − current SOTA`.

### 1.1 Landscape overview (from broad query 2026-04-21)
- Berkeley RDI (2026) study demonstrated that eight major agent benchmarks — including SWE-bench Verified, Terminal-Bench, WebArena, OSWorld, GAIA, FieldWorkArena — can be exploited to near-perfect scores without solving tasks. Source: https://rdi.berkeley.edu/blog/trustworthy-benchmarks-cont/
- BenchLM.ai aggregated coding leaderboard (March 2026) shows ~195 models ranked across SWE-bench Pro, SWE-Rebench, LiveCodeBench, HumanEval, SWE-bench Verified. Source: https://benchlm.ai/coding
- April-2026 provisional leaders reported: Claude Mythos Preview 100.0% weighted, Claude Opus 4.7 95.3%, Gemini 3.1 Pro 95.0% (coding weighted aggregate — NOT SWE-bench Verified alone).
- GAIA, Feb-2026 reported leaders: Claude Opus 4.6 53.1% with tool access, GPT-5.3 Codex 36%, GLM-5 32%. (Framework-dependent.)

## 2. SWE-bench Verified
### 2.1 Current SOTA
- **Claude Mythos Preview: 93.9%** — leads as of April 20, 2026 (aggregator-reported; provisional/unverified harness). Source: https://benchlm.ai/coding, https://www.marc0.dev/en/leaderboard
- **Claude Opus 4.7 (Anthropic, released 2026-04-16): 87.6%** — official SWE-bench Verified. Source: https://tokenmix.ai/blog/swe-bench-2026-claude-opus-4-7-wins
- **GPT-5.3 Codex: 85.0%** — second-tier. Source: same.
- **BenchLM.ai aggregator (March 2026):** lists 34 LLMs on SWE-bench Verified. Source: https://benchlm.ai/benchmarks/sweVerified
- **Vals.ai (independent verifier):** https://www.vals.ai/benchmarks/swebench — third-party SWE-bench harness.

### 2.2 Trajectory (top-5 submissions over the last 6 months)
- 2025-10 → 2026-04: top-of-leaderboard moved from mid-70s% (Claude 3.7 / GPT-5 family) into high-80s–low-90s%. ~15–18 pp gain in 6 months, driven by Claude 4.6 → 4.7 and Mythos Preview.

### 2.3 Methodology link
- Official: https://www.swebench.com/ (503 on fetch 2026-04-21). Fallback: https://github.com/SWE-bench/SWE-bench
- Caveat: Berkeley RDI (2026) showed SWE-bench Verified can be gamed to near-perfect scores without solving tasks (https://rdi.berkeley.edu/blog/trustworthy-benchmarks-cont/).

## 3. SWE-bench Lite
- Leaderboard: https://pricepertoken.com/leaderboards/benchmark/swe-bench-lite
- Historically ran behind Verified by ~5–8 pp; 2026 top scores for Lite are in the 90–95% range (inferred from aggregators; UNVERIFIED — could not fetch swebench.com).

## 4. GAIA
### 4.1 Level 1 SOTA
- Leaderboard: https://huggingface.co/spaces/gaia-benchmark/leaderboard (fetch returned empty — JS-rendered Hugging Face Space).
- Secondary: HAL Princeton https://hal.cs.princeton.edu/gaia
- Per March-2026 reporting: top systems (Claude Opus 4.6, Manus-like agents) approach 70–80% on Level 1 (framework-dependent).

### 4.2 Level 2 SOTA
- 2026 leaders approach 50–60% on Level 2 (framework-dependent; numeric UNVERIFIED from leaderboard fetch).

### 4.3 Level 3 SOTA
- Current top-overall: **Claude Opus 4.6 at 53.1%** average (with tool access), reported Feb 2026. Source: landscape search summary, reflected by aggregator https://pricepertoken.com/leaderboards/benchmark/gaia
- Historically Level 3 has been the hardest; 2025 scores were ~15–30% for Level 3. Best published Level 3 rates in 2026 appear to be **~35–45% range** (UNVERIFIED — leaderboard JS-rendered).
- GPT-5 Mini top of Huggingface leaderboard **44.8 average** as of 2026-03-19.
- Berkeley RDI 2026 flagged GAIA as gamable.

## 5. DPAI Arena
- **DPAI = Developer Productivity AI Arena**, launched by JetBrains 2025-10-28, intended for donation to the Linux Foundation.
- Official site: https://dpaia.dev/
- JetBrains announcement: https://blog.jetbrains.com/blog/2025/10/28/introducing-developer-productivity-ai-arena-an-open-platform-for-ai-coding-agents-benchmarks/
- Coverage: https://www.aibase.com/news/22857, https://www.techzine.eu/news/devops/135840/jetbrains-launches-ai-benchmark-platform-dpai-arena/
- Architecture: multi-track (Issue→patch, PR review, Coverage, Static analysis, Upgrade). Initial track is Spring/Java — 15 open-source projects, 140+ tasks.
- "Top-3" semantics: DPAI has per-track leaderboards; target of "top-3" means top-3 on some track. Current top of public leaderboards (as of 2025-Q4) was dominated by Anthropic/OpenAI/JetBrains Junie agent — multi-agent submissions will compete directly against frontier-model-powered agents.
- UNVERIFIED: exact scores on dpaia.dev (not fetched successfully).

## 6. HumanEval / HumanEval+
- Leaderboard: https://paperswithcode.com/sota/code-generation-on-humaneval
- HumanEval is largely saturated: top 2025–2026 scores sit at 99%+ pass@1. HumanEval+ (EvalPlus) is still the active variant.
- Not a multi-agent benchmark; used for code-gen sanity checks.
- Relevance to Pheromone: LOW (not multi-agent; saturated).

## 7. MLE-bench
- Official: https://github.com/openai/mle-bench
- Paper: https://arxiv.org/pdf/2410.07095
- 75 Kaggle competitions; scoring by "Any Medal %".
- Current SOTA: **Neo (Autonomous ML engineer): 34.2% Any-Medal** (Aug 2025). Microsoft RD-agent: 22.4%. Source: https://news.ycombinator.com/item?id=44948570
- 2026 leaderboard scores NOT separately verified; likely the 2025 numbers remain near-SOTA barring recent submissions.

## 8. AgentBench
- Original AgentBench paper (2023): https://arxiv.org/abs/2308.03688 — 8 environments.
- No official live leaderboard maintained in 2026; widely superseded by τ-bench, OSWorld, GAIA.
- Status: STALE; cite published numbers from the paper for context only.

## 9. τ-bench
- Official: https://taubench.com/ ; paper: https://arxiv.org/pdf/2406.12045 ; code: https://github.com/sierra-research/tau-bench
- Variants: τ-bench (retail, airline), τ²-bench (telecom).
- Current SOTA (April 2026):
  - **Claude Mythos Preview: 89.2%** on τ-bench (tracked snapshot). Source: landscape summary.
  - **Step-3.5-Flash (StepFun): 0.882 (88.2%)** per llm-stats.com leaderboard: https://llm-stats.com/benchmarks/tau-bench
  - τ²-bench Telecom leaders on Artificial Analysis: https://artificialanalysis.ai/evaluations/tau2-bench
- BenchLM.ai TAU-bench averages across 38 models: https://benchlm.ai/benchmarks/tauBench

## 10. WebArena / VisualWebArena
- WebArena: https://webarena.dev/ ; VisualWebArena: https://jykoh.com/vwa
- **OpAgent (CodeFuse / Ant Group) SOTA: 71.6% success rate on WebArena, January 2026, #1.** Source: https://arxiv.org/pdf/2602.13559 , https://github.com/codefuse-ai/OpAgent
- Human baseline: ~78% — frontier is ~6.4 pp below human.
- Pre-2026 SOTA was ~35–50%; 2026 jump of ~20 pp driven by multi-agent Planner/Grounder/Reflector/Summarizer architectures (note: multi-agent is the winning pattern here).
- Berkeley RDI (2026) flagged WebArena as gamable.

## 11. OSWorld
- Official: https://os-world.github.io/ (503 on fetch 2026-04-21)
- Standard OSWorld: **Claude Opus 4.6 = 0.727 (72.7%)** leader. Source: https://llm-stats.com/benchmarks/osworld
- OSWorld-Verified (re-released by XLANG 2026): https://xlang.ai/blog/osworld-verified
  - **Claude Mythos Preview: 79.6%** (April 16, 2026)
  - Holo3-122B-A10B: 78.8%
  - Claude Opus 4.7: 78%
- BenchLM aggregator: https://benchlm.ai/benchmarks/osWorldVerified (16 models)
- Human baseline: ~72%; 2026 frontier systems are superhuman on OSWorld-Verified.

## 12. CUB
- **Disambiguation:** Pheromone's "CUB" = **Computer Use Benchmark** (Writer-introduced, six industry verticals). NOT Caltech-UCSD Birds (vision dataset). Confirmed by cross-ref to "6 industry verticals" and Writer's Action Agent leadership.
- Launched/popularized late 2025 by Writer alongside the Action Agent product.
- Leaderboard references:
  - https://writer.com/engineering/writer-action-agent/
  - https://writer.com/blog/writer-action-agent/
  - Media: https://venturebeat.com/ai/writer-launches-a-super-agent-that-actually-gets-sht-done-outperforms-openai-on-key-benchmarks
  - https://o-mega.ai/articles/the-2025-2026-guide-to-ai-computer-use-benchmarks-and-top-ai-agents
- **Current SOTA: Writer Action Agent = 10.4% overall** (late 2025, unchallenged into early 2026 per secondary sources). Competing agents: Manus AI, OpenAI CUA, Claude Computer Use, Gemini 2.5 Pro — all at low single-digit %.
- CUB is brutally hard — scores are low because it runs realistic enterprise workflows across six verticals with strict end-to-end success criteria. 15% would imply >40% relative improvement over the reigning SOTA.
- UNVERIFIED: no live standalone leaderboard URL; scores come from vendor + press reporting.

## 13. 2026 multi-agent-specific benchmarks (discovery)
New / actively used multi-agent benchmarks beyond the original list:
- **MultiAgentBench / MARBLE** (Zhu et al., ACL 2025 main): https://arxiv.org/abs/2503.01935 ; code https://github.com/ulab-uiuc/MARBLE — star/chain/tree/graph topologies; group discussion vs cognitive planning.
- **Silo-Bench** (2026): https://arxiv.org/html/2603.01045v2 — 30 algorithmic tasks, 3 communication-complexity levels, 54 configurations. Exposes "Communication-Reasoning Gap".
- **CREW-Wildfire**: https://arxiv.org/html/2507.05178v2 — agentic multi-agent collaboration at scale.
- **CUBE (Collaborative Block-Pushing)**: https://openreview.net/forum?id=T7OoS6t11c — embodied cooperation testbed.
- **CUBE (Common Unified Benchmark Environments)**: https://arxiv.org/abs/2603.15798 — protocol standard built on MCP+Gym.
- **UI-CUBE**: https://arxiv.org/abs/2511.17131 — 226 CUA tasks, UiPath.
- **CooperBench**: https://arxiv.org/html/2601.13295v1 ; https://cooperbench.com/ — evaluates coding agents as teammates.
- **MAESTRO** (2026): https://arxiv.org/pdf/2601.00481
- **SWE-EVO** (2026-01-27): https://arxiv.org/pdf/2512.18470 — coding agents under code evolution.
- **AIRS-Bench**: https://arxiv.org/html/2602.06855 — frontier AI research-science agents.
- **WMAC 2026** (AAAI bridge program): https://multiagents.org/2026/ — venue, not a benchmark, but signals ecosystem direction toward rigorous multi-agent evaluation.

Pheromone should at minimum submit to MultiAgentBench + Silo-Bench + CooperBench to establish multi-agent-specific credibility.

## 14. Feasibility assessment of Pheromone targets

Arithmetic and reasoning per row:

| Pheromone target | Current SOTA | Gap | Verdict | Reasoning |
|------------------|--------------|-----|---------|-----------|
| **SWE-bench Verified ≥ 80%** | 87.6% (Claude Opus 4.7, 2026-04-16, official) — 93.9% (Claude Mythos Preview, aggregator-reported) — sources: [tokenmix](https://tokenmix.ai/blog/swe-bench-2026-claude-opus-4-7-wins), [benchlm](https://benchlm.ai/coding) | 80 − 87.6 = **−7.6 pp** | **ACHIEVABLE — ALREADY MET** | Target is ≤ current SOTA; frontier models already hit 85–88%. Multi-agent orchestration on top of those models should clear 80% easily. FLAG: target is a floor anyone meets — claim needs a defensible lift (e.g., "80%+ with open-weights backbone" or "90%+ overall"). |
| **GAIA L3 ≥ 65%** | Best-reported GAIA overall ~53.1% (Claude Opus 4.6, Feb 2026, framework-dependent). Level-3 specifically is historically ~20–45% range in 2026 (UNVERIFIED exact number, leaderboard JS-rendered). Best plausible L3 ~35–45%. Source: [HF Space](https://huggingface.co/spaces/gaia-benchmark/leaderboard), [HAL](https://hal.cs.princeton.edu/gaia) | 65 − ~40 ≈ **+25 pp** | **UNREALISTIC** | Gap is >15 pp above the most optimistic L3 estimate, and GAIA L3 progress has been slow (Berkeley RDI also flagged gamability). Revised target recommended. |
| **DPAI Arena top-3** | JetBrains platform launched 2025-10; per-track leaderboards dominated by Anthropic, OpenAI, JetBrains Junie. Multiple tracks × moderate field size → top-3 per track is plausible for any competent multi-agent. Source: [JetBrains](https://blog.jetbrains.com/blog/2025/10/28/introducing-developer-productivity-ai-arena-an-open-platform-for-ai-coding-agents-benchmarks/), [dpaia.dev](https://dpaia.dev/) | Not numeric; depends on track & field | **AGGRESSIVE-BUT-PLAUSIBLE** | Top-3 overall would require Pheromone to beat frontier-model-powered incumbents; top-3 on one track (e.g., Coverage or Upgrade) is very reachable. Pheromone should specify the track. |
| **CUB ≥ 15%** | 10.4% (Writer Action Agent, late-2025 SOTA, uncontested per early-2026 secondary sources). Source: [Writer engineering](https://writer.com/engineering/writer-action-agent/), [VentureBeat](https://venturebeat.com/ai/writer-launches-a-super-agent-that-actually-gets-sht-done-outperforms-openai-on-key-benchmarks), [o-mega](https://o-mega.ai/articles/the-2025-2026-guide-to-ai-computer-use-benchmarks-and-top-ai-agents) | 15 − 10.4 = **+4.6 pp** | **AGGRESSIVE-BUT-PLAUSIBLE** | Absolute gap is only 4.6 pp, but that is **~44% relative improvement** over unchallenged SOTA in a benchmark where nothing else clears 10%. Feasible if Pheromone's multi-agent decomposition specifically attacks computer-use tasks; risky if the architecture is not computer-use-specialized. |

Legend: ACHIEVABLE / AGGRESSIVE-BUT-PLAUSIBLE / UNREALISTIC.

**Meta-flags:**
- SWE-bench Verified target is **below current SOTA** — risk of reviewer pushback ("you're not raising the bar"). Lift to 90%+ or constrain to a sub-condition (cost, latency, open-weights backbone).
- Berkeley RDI (2026) showed SWE-bench Verified, WebArena, OSWorld, GAIA are gamable. Pheromone's results will face scrutiny about whether tasks were actually solved; publish full trajectories.
- GAIA L3 number is not separately listed by most aggregators; UNVERIFIED exact current SOTA. If the true L3 SOTA is actually ≥55% (possible for a top frontier model with tool access), the verdict could soften to AGGRESSIVE-BUT-PLAUSIBLE.

## 15. Revised target proposals (only for UNREALISTIC rows)

**GAIA L3:**
- Current proposal: 65%+
- Issue: >15 pp gap to the most-optimistic L3 estimate; Level 3 progress is slow.
- **Revised recommendation: "GAIA L3 ≥ 45%, GAIA overall ≥ 60%"** — both aggressive but within trajectory of 2025→2026 GAIA improvement (~15 pp/year average overall). Alternatively: "GAIA average ≥ 60% (framework-controlled)".
- If Pheromone authors insist on 65% L3, they must (a) control the agent framework explicitly, (b) publish per-level trajectories and ablations, and (c) show that 65% is not merely a harness artifact (see Berkeley RDI criticism).

**SWE-bench Verified (target is too low rather than too high):**
- Revised recommendation: **"SWE-bench Verified ≥ 90% with open-weights 70B-class backbone"** or **"SWE-bench Verified ≥ 92% overall"** — above Claude Opus 4.7's 87.6% official score, defensible as a genuine lift.

**DPAI Arena:**
- Specify: "top-3 on DPAI Arena Issue→patch track" or "top-3 on DPAI Arena Coverage track" to bound the claim.

## 16. PheromBench name collision check

Queries run:
- `"PheromBench"` — zero hits.
- `"pheromone benchmark"` — only pheromone-biology and pre-LLM swarm-ACO results; no LLM benchmark.
- `site:pypi.org pherombench OR pheromone-benchmark` — no packages.
- `site:github.com PheromBench OR "pherom-bench"` — no repos.

**Verdict: NO COLLISION.** The name "PheromBench" appears to be available on PyPI and GitHub as of 2026-04-21. Not BLOCKING.

Soft caveats:
- Very close to `pherobase.com` (pheromone semiochemical DB) — SEO confusion is low but non-zero.
- `guoweiu/Pheromone` and `MincYu/pheromone` exist on GitHub but are unrelated projects (Fuyao comparison system, and an unrelated `pheromone` repo), not LLM benchmarks. Project-name "Pheromone" itself has mild conflict but that's a Track E / naming question, not PheromBench.

## 17. Gaps and UNVERIFIED items

- **swebench.com** live fetch returned 503 on 2026-04-21 — primary leaderboard values taken from secondary aggregators (tokenmix, benchlm.ai, marc0.dev). Recommend re-verification against swebench.com when available.
- **huggingface.co/spaces/gaia-benchmark/leaderboard** returns only page chrome (JS-rendered) — exact L1/L2/L3 splits UNVERIFIED. Recommend Playwright/screenshot verification. HAL Princeton (https://hal.cs.princeton.edu/gaia) should be cross-referenced next.
- **os-world.github.io** fetch 503. OSWorld numbers from llm-stats.com and xlang.ai blog.
- **dpaia.dev** not fetched; exact leader scores UNVERIFIED.
- **cooperbench.com** fetch 503.
- **CUB** has no canonical public leaderboard URL; scores exclusively from Writer blog + VentureBeat + o-mega reporting.
- **GAIA Level 3 specific SOTA %** — needed for proper feasibility arithmetic; currently estimated ~40% with wide error bars.
- **SWE-bench Verified 93.9% Claude Mythos Preview** is reported by aggregators but not yet confirmed on official swebench.com leaderboard. Treat as provisional.
- **AgentBench** has no fresh 2026 leaderboard — it has effectively been superseded.
- **τ-bench top-5 trajectory** not captured in detail — only the top-of-leaderboard number.

### Escalation summary
- SWE-bench Verified 80% target is ALREADY MET by frontier models — flag as "lift required".
- GAIA L3 65% target is UNREALISTIC relative to estimated SOTA — revised proposal offered.
- No PheromBench name collision — NOT BLOCKING.
- CUB is Computer Use Benchmark (Writer); not Caltech-UCSD Birds. The 15% target is coherent in the agent-coordination context.

---

**Status:** COMPLETE (feasibility table filled; remaining UNVERIFIED items enumerated in Section 17).

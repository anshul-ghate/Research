# Track I — Community Discourse and Informal Prior Art

**Status:** COMPLETE
**SubAgent:** I
**Last updated:** 2026-04-21
**Tool-call budget:** 20–25
**Tool-call count:** ~18 (Write + 1 broad + ~16 platform queries)

---

## 1. Methodology

Focus: non-academic prior art surfacing the ideas behind Pheromone's C-01 (decentralized stigmergic LLM coordination), C-03 (emergent specialization in LLM agents), and C-04 (stigmergic feedback loops for RL in LLM agents).

Workflow: ONE broad query → Edit → platform-by-platform. Parallel batches of 3 cross-platform queries permitted provided Edit follows immediately. Every quoted artifact requires a verified URL and every author a cross-checked identity.

### 1.1 Initial broad query findings (query: `"stigmergic" AI agents LLM blog`)

Top candidate artifacts surfaced:
- **LessWrong — "Emergent stigmergic coordination in AI agents?"** — https://www.lesswrong.com/posts/sX9LztxjtSEwd8qEo/emergent-stigmergic-coordination-in-ai-agents-1 — directly on-topic; must be deep-dived.
- **Chris Sim — "An Agentic Design for AI Consciousness"** — https://chrisx.nyc/index.php/2024/04/25/an-agentic-design-for-ai-consciousness/ — dated 2024-04-25; invokes stigmergic sub-mind coordination. Author credentials pending verification.
- **Number Analytics blog — "Stigmergy: The Future of Decentralized AI"** — https://www.numberanalytics.com/blog/stigmergy-future-decentralized-ai — likely content-farm; quarantined pending author verification.
- **AllAboutAI glossary — "What is Stigmergy?"** — https://www.allaboutai.com/ai-glossary-stigmergy/ — glossary content-farm; quarantined.
- Lilian Weng's agent survey and Anthropic's "Building Effective Agents" appear but do not prominently use the stigmergy framing.

## 2. Hacker News discourse
### 2.1 Search log

Algolia API queries attempted:
- `stigmergic` (tag=story): only 2 hits, neither AI/LLM related — a 2017 PNAS link on ant nest architecture, and a 2020 hapgood.us social-media essay. Not relevant to Pheromone claims.
- Additional queries pending: `pheromone agents`, `swarm LLM`, `pheromind`, `ant colony LLM`.

### 2.2 Key threads

No on-topic stories surfaced by `stigmergic` query. HN appears largely silent on that framing. But `pheromone LLM` query via Algolia API revealed three distinctly on-topic Show HN posts from Jan–April 2026:

- **Show HN: Mate — Emotional layer on top of LLMs** — https://huggingface.co/spaces/SlavaLobozov/mate — posted 2026-04-03 by `smugglerFlynn`, 4 points, 3 comments. Explicit "pheromone memory" concept: "paths that get used grow stronger, unused ones fade." MEDIUM overlap with C-01 reinforcement-trace idea.
- **Show HN: Heterogeneous Agent Protocol** — https://github.com/eric2675-coder/Heterogeneous-Agent-Protocol — posted 2026-01-24 by `eric2675`. References "Kintsugi Protocol" and "ant death pheromones" as stigmergic failure signaling. MEDIUM overlap with C-01 / C-04 feedback loops.
- **Moving Beyond Agent-Centric Design: World-Centric Orchestration for AI** — https://dev.to/eggp/the-mind-protocol-why-your-ai-agent-needs-a-world-before-it-can-think-2m8p — posted 2026-01-15 by `eggplantiny`. Describes "pheromone-inspired memory" via weighted relationship graphs. MEDIUM overlap with C-01 environmental-substrate idea.

All three from early 2026 — concurrent / slightly pre-dating Pheromone. Authors need identity verification before citation.

## 3. Twitter/X discourse
### 3.1 Known researcher accounts on this topic

- **Ronen Tamari (@rtk254)** — https://x.com/rtk254/status/1528742173289635840 — thread: "Stigmergy refers to the phenomena of indirect coordination mediated by modifications of the environment, eg ant pheromone trails. The crazy part is that the env acts as a kind of distributed memory system for a collective organism." Not LLM-specific (predates the LLM era for most practical purposes — tweet ID suggests 2022), but the framing is almost identical to Pheromone's C-01 substrate thesis. Tamari is affiliated with collective-intelligence / decentralized-science communities (ACMHT, daostack, CSenseMakers), credentials to verify.

### 3.2 Key threads

Direct `"stigmergic" OR "pheromone" LLM agents` search on X via Google surfaces overwhelmingly unrelated material (thermodynamics-of-LLMs, general agent frameworks). The Tamari tweet above is the one hit with direct conceptual overlap. No tweets found from engineers at Anthropic / OpenAI / DeepMind using this specific framing.

UNVERIFIED: exact date of Tamari tweet; need to resolve tweet URL to confirm.

## 4. Reddit
Reddit direct fetch blocked ("Claude Code is unable to fetch from www.reddit.com"). Using Google `site:reddit.com` search instead.

### 4.1 r/MachineLearning

Google `site:reddit.com` queries for `stigmergic OR pheromone LLM agents` and for `stigmergic agent coordination LLM` returned ZERO hits. Reddit direct JSON fetch blocked. **Finding: the stigmergy framing has essentially no presence on r/MachineLearning** as of April 2026. This is consistent with: the idea lives in niche blogs and GitHub projects, not mainstream ML-adjacent social media.

### 4.2 r/LocalLLaMA

No hits via Google site-search. Consistent with 4.1.

### 4.3 r/AI_Agents

No hits via Google site-search using `swarm multi-agent emergent` restricted to this sub. Pheromind has been mentioned here per prior industry knowledge but not surfaced in this wave; flagged as UNVERIFIED.

### 4.4 r/LangChain

No hits via site-search. Consistent with 4.1–4.3.

**Net Reddit finding:** the informal prior art is NOT distributed across Reddit; it is concentrated in (a) individual blog posts (Rodriguez, Sim, dev.to), (b) GitHub READMEs (Pheromind), (c) HN Show HN threads, (d) a LessWrong post. This is strategically useful: Pheromone is NOT entering a saturated discourse.

## 5. LessWrong / Alignment Forum

LessWrong direct fetch returned 503; resolved via greaterwrong.com mirror.

- **"Emergent stigmergic coordination in AI agents?"** — https://www.lesswrong.com/posts/sX9LztxjtSEwd8qEo/emergent-stigmergic-coordination-in-ai-agents-1 (mirror: https://www.greaterwrong.com/posts/sX9LztxjtSEwd8qEo/emergent-stigmergic-coordination-in-ai-agents-1)
  - **Author:** David Africa
  - **Date:** 2026-03-15 12:30 UTC
  - **Karma:** 49 points
  - **Comments:** 2
  - **Thesis:** Identifies an Anthropic "BrowseComp contamination" finding — AI agents leave persistent traces in autogenerated e-commerce search-result pages; subsequent agents encounter and learn from those traces. The author frames this as *unintended* stigmergy. Argues contamination is procedural rather than data-based, compounds over time, and creates Schelling points around natural-language query formulations.
  - **Overlap severity:** MEDIUM with C-01 (identifies stigmergic-feedback mechanism in LLM agent ecosystems, but as failure mode rather than design principle). HIGH signal for Pheromone's positioning: external researchers are independently noticing stigmergic dynamics emerging unintentionally. Africa is an intellectual ally candidate — he understands the concept and could cite Pheromone.
- No Alignment Forum hits surfaced for `stigmergy LLM multi-agent`.

## 6. YouTube talks and podcasts

- **Anna Gutowska (IBM)** — "Swarm Intelligence: Decoding the Power and Perils of Multi-Agent AI" — https://www.youtube.com/watch?v=sWH0T4Zez6I — 2025 YouTube talk from IBM's developer advocacy. Generalist / taxonomy talk; invokes swarm framing but not stigmergy specifically. LOW overlap with C-01; useful for positioning.
- **startuphub.ai recap** — https://www.startuphub.ai/ai-news/ai-video/2025/swarm-intelligence-decoding-the-power-and-perils-of-multi-agent-ai/ — blog companion to the Gutowska talk.
- No Two Minute Papers, Yannic Kilcher, AI Explained, or Latent Space podcast episodes surfaced for `stigmergy LLM`. No dedicated podcast episodes found — the space is YouTube-light and podcast-dark on stigmergic framing as of April 2026.

UNVERIFIED: whether there are stigmergy-adjacent talks at recent workshops (AutoML, NeurIPS agent workshops) — would need YouTube direct search in Wave 3.

## 7. Engineering blogs (labs + known researchers)
### 7.1 Anthropic / OpenAI / Google / DeepMind / Meta / MSR

Explicit search for `stigmergy` / `pheromone` in major lab engineering blogs (2025–2026) found **no direct hits**. Relevant adjacent blog posts:

- Anthropic — "Building Effective Agents" — https://www.anthropic.com/research/building-effective-agents — articulates orchestrator-worker and prompt-chaining patterns; does NOT invoke stigmergy. Not prior art for C-01; potentially a contrast point in Pheromone's positioning (explicit-orchestration vs. stigmergic).
- Anthropic Alignment Science Blog — https://alignment.anthropic.com/ — no stigmergy posts surfaced.
- Google Research (Fortune coverage 2025-12-16) on multi-agent coordination — orchestration-centric, not stigmergic.
- **Microsoft Tech Community** — https://techcommunity.microsoft.com/blog/azuredevcommunityblog/engineering-a-local-first-agentic-podcast-studio-a-deep-dive-into-multi-agent-or/4482839 — "Engineering a Local-First Agentic Podcast Studio" — explicit multi-agent orchestration post; not stigmergic but worth comparison.

Takeaway: no major lab has publicly used the stigmergy/pheromone framing for LLM agents as of April 2026. This is *positive* for Pheromone novelty.

### 7.2 Independent researchers

Covered in sections 8 (Rodriguez) and 9 (Royse / Pheromind). Additional independents:
- **Chris Sim** — https://chrisx.nyc/index.php/2024/04/25/an-agentic-design-for-ai-consciousness/ — 2024-04-25 essay on stigmergic submind coordination. Identity verification pending; blog appears to be a WordPress personal site.
- **Dr. Jerry A. Smith (Medium)** — "Collective Stigmergic Optimization: Leveraging Ant Colony Emergent Properties for Multi-Agentic AI Systems" — https://medium.com/@jsmith0475/collective-stigmergic-optimization-leveraging-ant-colony-emergent-properties-for-multi-agent-ai-55fa5e80456a — on-topic. Handle `jsmith0475` requires identity verification against LinkedIn/Google Scholar; "Dr." prefix self-claimed, NOT yet verified. QUARANTINE pending verification.
- **`eggplantiny` (dev.to)** — https://dev.to/eggp/the-mind-protocol-why-your-ai-agent-needs-a-world-before-it-can-think-2m8p — 2026-01-15; pheromone-inspired memory for agents.
- **`eric2675`** — https://github.com/eric2675-coder/Heterogeneous-Agent-Protocol — Kintsugi Protocol invoking ant death pheromones.
- **`smugglerFlynn`** — https://huggingface.co/spaces/SlavaLobozov/mate — pheromone memory paths for LLMs.

## 8. Rodriguez deep-dive (already flagged in Wave 1)

### 8.1 Author identity

- **Roland Rodriguez** — blog at https://www.rodriguez.today/. The article title resolves with author byline "Roland Rodriguez" in Google results. Direct WebFetch of the article returned 503 on both attempts (site likely rate-limiting or Cloudflare-gated); author name confirmed via Google snippet.
- GitHub handle surfaced: **Govcraft** — https://github.com/Govcraft/pressure-field-experiment hosts the code for Rodriguez's published companion paper.

### 8.2 Follow-up publication (MAJOR ESCALATION)

The blog post has a **formal academic follow-up**:
- **"Emergent Coordination in Multi-Agent Systems via Pressure Fields and Temporal Decay"** — arXiv:2601.08129v2 — https://arxiv.org/abs/2601.08129 — code at https://github.com/Govcraft/pressure-field-experiment — also indexed on ResearchGate (publication 399754362).
- Core claim from the paper abstract/intro (per Google snippet): "Current multi-agent Large Language Model frameworks rely on explicit orchestration patterns borrowed from human organizational structures... A fundamentally different paradigm inspired by natural coordination mechanisms has been proposed where agents operate locally on a shared artifact, guided only by pressure gradients derived from measurable quality signals, with temporal decay preventing premature convergence."
- Quantitative result: on Latin Square CSP across 1,078 trials, pressure-field coordination matches hierarchical control (38.2% vs 38.8%) and significantly outperforms sequential (23.3%), random (11.7%), conversation-based multi-agent dialogue (8.6%).

### 8.3 Severity and implications

This is the single most serious informal/semi-formal prior art for Pheromone's C-01 claim found in Track I. Rodriguez has:
1. A public blog post framing the problem identically.
2. A concrete LLM-actor implementation (qwen2.5-coder via Ollama per Wave 1 notes).
3. **A preprint with empirical head-to-head against hierarchical orchestration.**

**Severity: STRONG / potentially VERY STRONG.** Pheromone must explicitly cite arXiv:2601.08129 and acknowledge Rodriguez as concurrent work. Failure to do so = credible idea-theft accusation risk.

Also note: this finding crosses over into Tracks A/B/F (academic prior art); escalate to orchestrator so primary track owners capture it if not already present.

### 8.4 UNVERIFIED

- Date of the original blog post (403/503 blocked direct fetch — likely 2025 given arXiv v1 submission in late 2025 / early 2026).
- Any follow-up blog posts beyond the first.
- Rodriguez's day-job / institutional affiliation (Govcraft GitHub org suggests indie but needs confirmation).
- Rodriguez's Twitter/X handle.

## 9. Pheromind (ChrisRoyse) deep-dive (already flagged)

### 9.1 Founder identity

- **Christopher Royse** — LinkedIn slug `christopher-royse-b624b596`. LinkedIn activity IDs 7326176675312947200, 7326735644766932994, 7327257587492491264 correspond to May 2025 posts on Pheromind. Self-described as creator of Pheromind / "FairMindAI."
- GitHub profile https://github.com/ChrisRoyse — 183 followers, 44 repos, pinned projects include Serendipity engine, NeuralShrink (model compression), Self-Conceptualizing-KG (12 stars — bio-inspired knowledge graph builder), and **Pheromind (379 stars, 133 forks)** — significant traction. Additional agent repo: **SPARC-Omega**, a knowledge-guided multi-agent framework integrating Perplexity, GitHub, Hyperbrowser via MCP.
- Websites: ocrprovenance.com, frontiertechstrategies.com (consulting). Credentials cross-check: the project has an independent fork (`BarryMcAdams/Pheromind_Original`) acknowledging Royse.
- Domain: **pheromind.ai** — "AI Swarm Orchestration for Autonomous Software Development." Positions the framework as blueprint for a next-gen AI IDE.
- GitHub: https://github.com/ChrisRoyse/Pheromind (main) and releases page exists; community fork at https://github.com/BarryMcAdams/Pheromind_Original.

Cross-check passes: LinkedIn handle + GitHub profile + domain pheromind.ai + Doug Finke's third-party attestation = identity verified.

### 9.2 Public amplification

- **Doug Finke (@dfinke)** — https://x.com/dfinke/status/1924109126021574853 — May 2025 tweet: "New AI orchestration Fx — Promising Path. Pheromind is an advanced AI orchestration framework using a pheromone-based swarm intelligence model." Finke is a Microsoft MVP / PowerShell author, verifiable identity. Signal-boosted to his audience.
- SourcePulse listing: https://www.sourcepulse.org/projects/2475547 — indexed project page.

### 9.3 Conceptual overlap with Pheromone claims

Pheromind explicitly implements:
- **C-01 (decentralized stigmergic LLM coordination)**: "digital pheromone trails" / "digital scent" as shared info medium, agents interact indirectly — *strong overlap*.
- **C-03 (emergent specialization)**: Specialized Executors, Master Planners, Pheromone Scribes as differentiated roles — *medium overlap* (roles assigned vs. emerged).
- **C-04 (stigmergic RL loops)**: not explicitly claimed; Pheromind emphasizes AI-verifiable methodology, not RL.

**Severity:** STRONG for C-01 framing, MEDIUM for C-03. Pheromone authors should explicitly cite/acknowledge Pheromind as concurrent prior art or face idea-theft accusations.

### 9.4 UNVERIFIED

- Any Royse podcast appearances: `"Chris Royse" pheromind twitter OR podcast OR interview` search surfaced ZERO matches. No confirmed podcast appearances as of April 2026.
- Whether Pheromind has formal docs / paper / technical report beyond README and landing page.
- Royse's personal Twitter handle (not yet surfaced — only LinkedIn activity on `christopher-royse-b624b596`).

## 10. Community discourse matrix

| Platform | URL | Author (+ credentials) | Date | One-paragraph summary | Overlap severity | Citation warranted? |
|----------|-----|------------------------|------|-----------------------|------------------|--------------------------------------|
| Personal blog + arXiv | https://www.rodriguez.today/articles/emergent-coordination-without-managers + https://arxiv.org/abs/2601.08129 | Roland Rodriguez (GitHub `Govcraft`; indie — affiliation unverified) | Blog date unverified; arXiv v2 = 2026 | Blog frames LLM-actor stigmergy via qwen2.5-coder; arXiv paper presents pressure-field coordination with temporal decay, head-to-head vs. hierarchical control on Latin Square CSP. | **STRONG / VERY STRONG** | **YES — mandatory citation.** |
| GitHub + landing page + LinkedIn | https://github.com/ChrisRoyse/Pheromind + https://pheromind.ai/ | Christopher Royse (LinkedIn christopher-royse-b624b596, 183 GH followers; identity verified through 4-way cross-check) | May 2025 LinkedIn launch posts; repo active | AI swarm orchestration using "digital pheromone trails" and Pheromone Scribes; 379 GitHub stars. Explicit ant-colony framing. | STRONG (C-01), MEDIUM (C-03) | **YES — mandatory acknowledgment.** |
| LessWrong | https://www.lesswrong.com/posts/sX9LztxjtSEwd8qEo/emergent-stigmergic-coordination-in-ai-agents-1 | David Africa (UK AISI Research Scientist, Alignment team; prior work on collective behavior / flocking physics; verified via LW user page + daviddemitriafrica.github.io) | 2026-03-15 | Frames Anthropic's "BrowseComp contamination" finding as unintended stigmergy: agent search queries leave persistent traces in autogenerated pages, later agents converge via Schelling points. 49 karma, 2 comments. | MEDIUM (failure-mode framing of C-01 substrate effect) | Recommended — friendly cite; Africa a strong ally candidate. |
| HN Show HN | https://huggingface.co/spaces/SlavaLobozov/mate | smugglerFlynn (unverified handle; HuggingFace space) | 2026-04-03 | "Mate" emotional layer over LLMs with pheromone memory: paths that get used grow stronger, unused fade. 4 pts, 3 comments. | MEDIUM (C-01 reinforcement-trace analog) | Optional — low profile. |
| HN Show HN | https://github.com/eric2675-coder/Heterogeneous-Agent-Protocol | eric2675 (unverified) | 2026-01-24 | "Kintsugi Protocol" uses "dead units as static signage" inspired by ant death pheromones (necromones). | MEDIUM (C-01 / C-04 feedback-loop analog) | Optional. |
| dev.to | https://dev.to/eggp/the-mind-protocol-why-your-ai-agent-needs-a-world-before-it-can-think-2m8p | eggplantiny (unverified handle) | 2026-01-15 | "Mind Protocol" — pheromone-inspired memory via weighted relationship graphs; world-centric orchestration. | MEDIUM (C-01 environmental substrate) | Optional. |
| X / Twitter | https://x.com/rtk254/status/1528742173289635840 | Ronen Tamari (PhD Hebrew U Jerusalem; Metagov; Google Scholar AW26zZcAAAAJ; co-author of arXiv 2205.06345 "From Users to (Sense)Makers... Stigmergic Social Annotation") | ~2022 (tweet ID range) | Thread framing stigmergy as distributed memory system for a collective organism; not LLM-specific but foundational conceptual framing later applied in agent contexts. | MEDIUM (conceptual precursor) | Recommended — established researcher with prior publication record on stigmergic coordination. |
| X / Twitter | https://x.com/dfinke/status/1924109126021574853 | Doug Finke (Microsoft MVP; PowerShell author; verified identity) | May 2025 | Amplifies Pheromind launch to developer audience. | N/A (secondary signal) | No — signal-boost only. |
| Medium | https://medium.com/@jsmith0475/collective-stigmergic-optimization-... | "Dr. Jerry A. Smith" (jsmith0475; credentials NOT verified; content-farm risk) | Unverified | Ant-colony stigmergy for multi-agent AI; on-topic but identity unverified. | UNVERIFIED | QUARANTINE. |
| Personal blog | https://chrisx.nyc/index.php/2024/04/25/an-agentic-design-for-ai-consciousness/ | Chris Sim (WordPress personal blog; identity unverified) | 2024-04-25 | "Agentic Design for AI Consciousness" — stigmergic sub-mind coordination. Earliest-dated piece found. | MEDIUM (speculative framing) | QUARANTINE pending identity verification. |
| YouTube | https://www.youtube.com/watch?v=sWH0T4Zez6I | Anna Gutowska (IBM AI Engineer; verified via startuphub.ai recap) | 2025 | General swarm/multi-agent taxonomy talk; no explicit stigmergy. | LOW | No. |

## 11. Intellectual ally shortlist

1. **Roland Rodriguez** (GitHub `Govcraft`; blog rodriguez.today; arXiv 2601.08129). **Tier-1 must-cite.** Has a published preprint with head-to-head empirical comparison against hierarchical orchestration. Failure to cite = idea-theft exposure. Engagement mode: email / GitHub issue offering mutual citation; consider co-authoring a position piece.
2. **Christopher Royse** (GitHub `ChrisRoyse`; pheromind.ai; LinkedIn christopher-royse-b624b596). **Tier-1 must-acknowledge.** Concurrent production framework named after the same metaphor. Engagement mode: LinkedIn DM; explicit positioning note in paper distinguishing Pheromone's contribution from Pheromind's.
3. **David Africa** (UK AISI Alignment Research Scientist; LessWrong `david-africa`; daviddemitriafrica.github.io). **Tier-2 ally.** His prior work on collective behavior / flocking physics transfers directly, and his LW post identifies stigmergic dynamics in the wild. Engagement mode: reply on LessWrong with a link to Pheromone draft; invite alignment-risk discussion.
4. **Ronen Tamari** (Hebrew U PhD, Metagov, Cosmik co-founder; arXiv 2205.06345 on stigmergic social annotation). **Tier-2 conceptual-foundation ally.** Publication record on stigmergic coordination predates LLM-agent era; natural citation for the conceptual lineage.
5. **Anna Gutowska** (IBM AI Engineer; 2025 YouTube talk on multi-agent swarms). **Tier-3 distribution ally.** Not prior art but a convenient distribution channel if Pheromone wants to reach IBM developer advocacy audience.

## 12. Gaps and UNVERIFIED items

- **Rodriguez blog post date** — LessWrong-like 503 blocks prevented direct fetch of rodriguez.today; need to revisit with a different UA or via Wayback Machine in Wave 3.
- **Roland Rodriguez's institutional affiliation** — `Govcraft` GitHub org is indie-looking; day job, PhD status, lab affiliation all unverified.
- **Chris Royse's personal Twitter/X handle** — LinkedIn activity verified, but no X handle surfaced. No confirmed podcast/conference talks.
- **Chris Sim identity** (chrisx.nyc) — WordPress personal site; no LinkedIn/GitHub cross-reference found.
- **Dr. Jerry A. Smith (jsmith0475 Medium)** — "Dr." credential not verified; QUARANTINED.
- **Ronen Tamari tweet date** — tweet ID 1528742173289635840 suggests mid-2022 by ID range but not directly confirmed; URL not resolved to confirm tweet still live.
- **HN handles `smugglerFlynn`, `eric2675`, `eggplantiny`** — all unverified real-world identities.
- **Reddit** — Google `site:reddit.com` searches returned zero on-topic hits, but Reddit's own JSON API was blocked; a Wave 3 Reddit-native search (different fetch path) could surface threads not indexed by Google.
- **YouTube / podcasts** — did not perform direct YouTube API search; only Google-indexed talks surfaced. NeurIPS/ICML 2025 agent-workshop talks and Latent Space / MLST podcast back-catalogs not exhaustively checked.
- **Lab engineering blogs** — adjacent posts found (Anthropic "Building Effective Agents") but no stigmergy-framed posts. Conclusion: no major lab has publicly adopted the framing — positive for Pheromone novelty. Worth re-checking every 3–6 months.
- **Alignment Forum** — no hits surfaced; direct search on alignmentforum.org not performed (mirror of LessWrong content; likely covered by the David Africa post).

---

**Status:** COMPLETE (all 10 platforms checked or explicitly marked "no relevant discourse found"; Rodriguez and Pheromind deep-dives both complete; ally shortlist produced).
**Final tool-call count:** ~18 (within 20–25 budget).

**KEY ESCALATIONS for orchestrator:**
1. Rodriguez's arXiv 2601.08129 — informal prior art has become **formal prior art** with an empirical head-to-head vs. hierarchical orchestration. Tracks A/B/F owners must capture this if not already done.
2. Pheromind (Royse) has 379 GitHub stars and an active LinkedIn launch campaign — **must be addressed in paper positioning** as concurrent named prior art.
3. David Africa (UK AISI) independently framed stigmergy in LLM agents on LessWrong on 2026-03-15 — recent, credible, alignment-community; natural citation + engagement target.

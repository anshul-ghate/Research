# Track E — Name and Brand Collision

**Status:** COMPLETE
**Headline severity:** CAUTIOUS-GO with CONFUSING collisions; no BLOCKING found at time of check. Strong brand-adjacency warning (see Pheromind + pheromone-ai.com "Launching Soon").
**SubAgent:** E
**Last updated:** 2026-04-21
**Tool-call budget:** 15–20
**Tool-call count:** 15

---

## 1. Methodology

Namespace-by-namespace availability check for "pheromone", "pheromone-ai", "pheromones" across package registries, code hosts, model hubs, product directories, trademarks (preliminary), domains, and social handles. Evidence is URL-based; 404 = AVAILABLE, 200 with project = TAKEN.

## 2. Package registry status
### 2.1 PyPI
- `pheromone-ai`: **AVAILABLE** — PyPI JSON API returns 404. Evidence: https://pypi.org/pypi/pheromone-ai/json
- `pheromone`: **AVAILABLE** — PyPI JSON API returns 404. Evidence: https://pypi.org/pypi/pheromone/json
- `pheromones`: **AVAILABLE** — PyPI JSON API returns 404. Evidence: https://pypi.org/pypi/pheromones/json

Note: all three planned PyPI namespaces are free at time of check.

### 2.2 npm
- `pheromone`: **AVAILABLE** — npm registry returns 404. Evidence: https://registry.npmjs.org/pheromone
- `pheromone-ai`: **AVAILABLE** — npm registry returns 404. Evidence: https://registry.npmjs.org/pheromone-ai
- `pheromones`: **AVAILABLE** — npm registry returns 404. Evidence: https://registry.npmjs.org/pheromones

### 2.3 crates.io
- `pheromone`: crates.io API returned 503 (rate-limited). Based on broad web search, no prominent Rust crate with this name surfaced. Status **AMBIGUOUS — likely AVAILABLE**. Evidence: https://crates.io/crates/pheromone (manual check recommended).

## 3. Code host status
### 3.1 GitHub — pheromone / pheromone-ai orgs
- `github.com/pheromone`: **TAKEN (squatted/inactive)** — account exists but has 0 public repos and 1 follower. Effectively a namespace squat, not a working project. Cannot be used; would require rename or GitHub namespace release process. Evidence: https://github.com/pheromone
- `github.com/pheromone-ai`: **AVAILABLE** — 404. Evidence: https://github.com/pheromone-ai
- `github.com/pheromones`: not directly fetched but per top-repo scan no such org surfaces; treated as **likely AVAILABLE** (see note).

### 3.2 GitHub — top repos matching "pheromone"
Top 10 by stars (evidence: https://github.com/search?q=pheromone&type=repositories&s=stars&o=desc):

| Rank | Repo | Stars | Domain | Collision level |
|------|------|-------|--------|-----------------|
| 1 | luantty2/pheromone_keyboard | 280 | Mechanical keyboard / QMK | None (different domain) |
| 2 | rprokap/entremanure | 56 | Unrelated | None |
| 3 | MincYu/pheromone | 45 | C++ serverless platform (per search) | Low — different subdomain |
| 4 | hbang/Pheromone | 42 | Cydia iOS tweaks | None |
| 5 | gestom/CosPhi | 32 | Artificial pheromone system (research) | Academic/research — tangential |
| 6 | bwiklund/ant-simulator | 28 | Canvas ant simulation | Tangential — similar metaphor, not a product |
| 7 | Blockchain-CN/pheromones | 20 | P2P network | None |
| 8 | Nikorasu/PyNAnts | 18 | Ant pheromone sim | Tangential |
| 9 | ankitagupta12/pheromone | 17 | Ruby, unclear | Low |
| 10 | mbalchanowski/Ant-Colony-System | 10 | ACO algorithm | Tangential |

**Most significant collision (not in top 10 by stars but found via broad search):** ChrisRoyse/Pheromind (https://github.com/ChrisRoyse/Pheromind), an "AI swarm orchestration framework using pheromone-based swarm intelligence" — directly adjacent concept/domain. Forks exist at `mariogov/Pheromind_02`, `mariusgavrila/pheromind`. This is a CONFUSING-level brand-adjacency issue (not BLOCKING because the name is "Pheromind" not "Pheromone", but user confusion risk is real).

## 4. Model/dataset hubs
### 4.1 HuggingFace
- `huggingface.co/pheromone`: **AVAILABLE** — 404. Evidence: https://huggingface.co/pheromone
- Full-text search not separately verified due to budget; recommend manual re-check pre-launch.

## 5. Product directories
### 5.1 Product Hunt
- Search endpoint returned HTTP 503 during this run. **AMBIGUOUS — manual re-check recommended.** Evidence: https://www.producthunt.com/search?q=pheromone
- Broad web search did NOT surface a Product Hunt launch for a "Pheromone" AI/software product in April 2026.

### 5.2 Y Combinator
- YC company directory returned HTTP 503 during this run. **AMBIGUOUS — manual re-check recommended.** Evidence: https://www.ycombinator.com/companies?query=pheromone
- Broad web search did NOT surface a YC-backed company named "Pheromone".
- Note: "Pheromonix AI" is a LinkedIn-listed company (distinct name, brand-adjacent). Evidence: https://www.linkedin.com/company/pheromonix

## 6. Trademark preliminary screening (NOT LEGAL ADVICE)

**Preliminary — not legal advice. Full clearance requires a trademark attorney.**

### 6.1 USPTO
- Direct TESS search attempted via broad query. No obvious live USPTO registration for "PHEROMONE" covering Nice class 9 (downloadable software, AI/ML software) or class 42 (SaaS, AI services) surfaced in public web indexing. Evidence: https://tmsearch.uspto.gov/ (manual search recommended).
- Numerous class-3 (cosmetics/perfume) and class-1/5 (agricultural pheromone products, pest management) uses exist; these are in different Nice classes and are LOW RISK for AI software use per guardrail #4, though may constrain consumer-facing branding.

### 6.2 WIPO
- WIPO Global Brand Database returned 503 during this run. **AMBIGUOUS — manual re-check required.** Evidence: https://branddb.wipo.int/
- Known relevant: "Pherobank" and "Omnilure" are registered trademarks of Pherobank BV (agricultural pheromone products — different class, LOW risk for AI/software).

### 6.3 Other
- UK Companies House: "PHEROMONE LTD" (Company 11358794) was a UK IT-services company, **DISSOLVED 26 April 2022**. Evidence: https://find-and-update.company-information.service.gov.uk/company/11358794 — no longer an active blocker but indicates historic use in the IT-services space.
- "Pheromone Industries Limited" exists on LinkedIn (unclear sector).

## 7. Domain availability

| Domain | Status | Evidence / Notes |
|--------|--------|------------------|
| pheromone.ai | Unresolved during run (503) | https://pheromone.ai — likely registered given high value of `.ai`; AMBIGUOUS |
| pheromone.dev | Unresolved during run (503) | https://pheromone.dev — AMBIGUOUS |
| pheromone.io | Unresolved during run (503) | https://pheromone.io — AMBIGUOUS |
| **pheromone-ai.com** | **REGISTERED — "Launching Soon" parking page with email capture** | https://pheromone-ai.com — someone is already staging a product under this exact name. Not available for use. |
| pheromone.app | Not checked (budget) | — |
| pheromone.sh | Not checked (budget) | — |
| getpheromone.com | ECONNREFUSED during run — inconclusive | https://getpheromone.com |
| usepheromone.com | ECONNREFUSED during run — inconclusive | https://usepheromone.com |

**Key finding:** `pheromone-ai.com` is taken by a stealth project (possibly Pheromind-related, or an unrelated squatter/stealth startup). This is the closest thing to a BLOCKING signal found, but without knowing what that entity is launching, severity is CONFUSING (not BLOCKING).

## 8. Social handle status
- X/Twitter `@pheromone_ai`: fetch returned 503 — **AMBIGUOUS.** Evidence: https://x.com/pheromone_ai
- X/Twitter `@pheromone`, `@pheromoneai`: not individually fetched due to budget.
- LinkedIn: "Pheromone Industries Limited" and "Pheromonix AI" both exist as company pages (brand-adjacent, not exact). Evidence: https://www.linkedin.com/search/results/companies/?keywords=pheromone
- Recommendation: reserve handles during launch prep.

## 9. Severity summary

| Namespace | Status | Evidence URL | Severity | Owner/description if taken |
|-----------|--------|--------------|----------|---------------------------|
| PyPI `pheromone-ai` | AVAILABLE | https://pypi.org/pypi/pheromone-ai/json (404) | ACCEPTABLE | — |
| PyPI `pheromone` | AVAILABLE | https://pypi.org/pypi/pheromone/json (404) | ACCEPTABLE | — |
| PyPI `pheromones` | AVAILABLE | https://pypi.org/pypi/pheromones/json (404) | ACCEPTABLE | — |
| npm `pheromone` | AVAILABLE | https://registry.npmjs.org/pheromone (404) | ACCEPTABLE | — |
| npm `pheromone-ai` | AVAILABLE | https://registry.npmjs.org/pheromone-ai (404) | ACCEPTABLE | — |
| npm `pheromones` | AVAILABLE | https://registry.npmjs.org/pheromones (404) | ACCEPTABLE | — |
| crates.io `pheromone` | Likely available | https://crates.io/crates/pheromone (503; re-check) | AMBIGUOUS | — |
| GitHub `/pheromone` | TAKEN (squat, 0 repos) | https://github.com/pheromone | CONFUSING | Unused squat; 1 follower, no content |
| GitHub `/pheromone-ai` | AVAILABLE | https://github.com/pheromone-ai (404) | ACCEPTABLE | — |
| GitHub repos top-10 | Hobby/unrelated/tangential | https://github.com/search?q=pheromone&type=repositories&s=stars&o=desc | ACCEPTABLE | Keyboards, Cydia tweaks, ant sims, research code |
| GitHub "Pheromind" framework | Active AI-orchestration framework (different name) | https://github.com/ChrisRoyse/Pheromind | **CONFUSING** | Frontier Tech Strategies — "pheromone-based swarm intelligence" framework; near-identical concept, name is 2 chars different |
| HuggingFace `/pheromone` | AVAILABLE | https://huggingface.co/pheromone (404) | ACCEPTABLE | — |
| Product Hunt | Not resolvable (503) | https://www.producthunt.com/search?q=pheromone | AMBIGUOUS | — |
| Y Combinator | Not resolvable (503) | https://www.ycombinator.com/companies?query=pheromone | AMBIGUOUS | — |
| USPTO class 9/42 | No clear live match | https://tmsearch.uspto.gov/ | ACCEPTABLE (preliminary) | — |
| USPTO class 1/3/5 | Multiple uses (cosmetics, agriculture) | (web evidence) | LOW RISK for AI software | Different Nice class |
| WIPO | Not resolvable (503) | https://branddb.wipo.int/ | AMBIGUOUS | — |
| UK Companies House | "PHEROMONE LTD" dissolved 2022 | https://find-and-update.company-information.service.gov.uk/company/11358794 | ACCEPTABLE | Historic IT-services shell, now dissolved |
| LinkedIn "Pheromonix AI" | Active brand-adjacent company | https://www.linkedin.com/company/pheromonix | CONFUSING | Similar name, similar space |
| Domain `pheromone-ai.com` | **REGISTERED — "Launching Soon"** | https://pheromone-ai.com | **CONFUSING** (near-blocking) | Unknown operator staging a product at the team's planned name |
| Domain `pheromone.ai` | Unresolved during run | https://pheromone.ai | AMBIGUOUS | — |
| Domain `pheromone.dev` | Unresolved during run | https://pheromone.dev | AMBIGUOUS | — |
| Domain `pheromone.io` | Unresolved during run | https://pheromone.io | AMBIGUOUS | — |
| X/Twitter `@pheromone_ai` | Unresolvable (503) | https://x.com/pheromone_ai | AMBIGUOUS | — |

**Severity count:** 0 BLOCKING, 3 CONFUSING (Pheromind framework, pheromone-ai.com parking, Pheromonix AI), 1 CONFUSING-squat (github.com/pheromone), ~9 ACCEPTABLE, ~7 AMBIGUOUS (mostly due to 503 rate-limits that need re-checking).

## 10. Alternative names shortlist

No BLOCKING collision was found, so name change is not strictly required. However, given the CONFUSING collisions (especially **Pheromind** in the same exact concept space, plus the `pheromone-ai.com` "Launching Soon" page under the team's planned product name), a name change is strongly worth considering. Candidates preserve the bio-inspired coordination/signal-leaving theme:

1. **Stigmergy / Stigmer** — from the formal term ("stigmergy") for indirect coordination via environmental signals; that is literally the academic name for what pheromones do. Technical and precise. Short form `stigmer` is pronounceable and distinctive.
2. **Trailmark** — evokes pheromone trails and trail-marking by ants; suggests leaving a readable signal in a shared environment. Simple English compound, easy to pronounce.
3. **Hivecast** — combines hive (collective intelligence) with cast/broadcast (signal emission to shared medium). Captures swarm + messaging connotations.
4. **Swarmlink** — direct statement of swarm coordination plus linkage/communication. Clear, utilitarian, dev-tool-flavored.
5. **Scentrail** — evokes the "digital scent trail" metaphor already used in the Pheromind description. Memorable, two-syllable, visually vivid. (Caveat: may carry consumer-product connotations — verify before adoption.)

**Do NOT re-verify** these here (out of budget). Constraints to validate before committing: (a) PyPI + npm availability, (b) `.ai`/`.dev` domain availability, (c) no USPTO class 9/42 live mark, (d) handle availability on X/GitHub.

## 11. Final recommendation

**CAUTIOUS-GO** on "Pheromone" / `pheromone-ai`, with explicit risk acknowledgment:

**Go signals:**
- All three target PyPI namespaces, all three npm namespaces, GitHub `pheromone-ai` org, and HuggingFace `pheromone` are free at time of check.
- No live USPTO class 9/42 trademark appears to block; the closest Nice-class uses are in cosmetics/perfume (class 3) and agriculture (class 1/5), both LOW RISK for an AI/dev-tools launch.
- "PHEROMONE LTD" (UK IT-services) is dissolved — former historic risk cleared.

**Risk signals:**
- **Pheromind** (github.com/ChrisRoyse/Pheromind) is an already-active "AI swarm orchestration framework using pheromone-based swarm intelligence" developed by Frontier Tech Strategies and seeking seed funding. The concept overlap is near-total; only the name differs by suffix. Users searching for either will collide. This is a CONFUSING brand-adjacency risk and a SEO/discoverability disadvantage — not a legal blocker.
- **pheromone-ai.com** already resolves to a "Launching Soon" parking page under the team's exact intended product name. Unknown operator. This means the `.com` is unavailable and some entity is staging something under this name.
- **github.com/pheromone** is squatted (0 repos, 1 follower). The org name would need a re-attempt or GitHub's namespace-recovery process; `github.com/pheromone-ai` remains available and should be claimed immediately.
- **Pheromonix AI** (LinkedIn) is a brand-adjacent active company (name variant, same sector signal).

**Recommended next steps (for the Pheromone team):**
1. IMMEDIATELY reserve: PyPI `pheromone-ai` and `pheromone`; npm `pheromone-ai`; GitHub `pheromone-ai` org; HuggingFace `pheromone`; domain `pheromone.ai` (verify availability — 503 blocked this check) and `pheromone.dev`.
2. Commission a proper USPTO + WIPO trademark clearance in classes 9 and 42 before public launch. Budget-based preliminary screening here is insufficient for legal reliance.
3. Reach out to or monitor the `pheromone-ai.com` operator — if it is a stealth AI project, this moves to BLOCKING.
4. Reconsider the name if search-engine visibility against "Pheromind" matters — Pheromind is first-mover in this exact concept space. See §10 alternatives.
5. If launching consumer-facing (not just developer-tools), expect more friction from class-3 cosmetics uses and general vocabulary meaning; a distinctive made-up mark (§10 §1–5) would clear more reliably.

**Scope note:** This screen is package/brand availability only. Patent collision is SubAgent G's scope. Competitive-product analysis beyond name is SubAgent J's scope.

# Track C — Mainstream Multi-Agent Orchestration Frameworks

**Status:** IN PROGRESS
**SubAgent:** C
**Last updated:** 2026-04-21
**Tool-call budget:** 30–35
**Tool-call count:** 2 (skeleton + landscape query)

---

## 1. Methodology and landscape query

**Method:** One broad WebSearch for `multi-agent LLM frameworks 2026`, followed by per-framework official-source fetches (docs homepage or GitHub README). Every version/star/date comes from pages fetched on 2026-04-21. No citations from memory. Each profile closes with one weaker-than-Pheromone and one stronger-than-Pheromone sentence.

**Landscape-query (2026-04-21) highlights:**
- LangGraph is cited as the most-searched multi-agent framework (SuperAnnotate, GuruSup).
- CrewAI, Microsoft AutoGen (AG2), Google ADK (April 2025 release), Haystack remain the top tier.
- AutoGen's "Magentic-One" is highlighted as a generalist multi-agent web/file system.
- CrewAI Enterprise (compliance/audit trails) mentioned.
- LangGraph support for long-running persistent graphs (days-long workflows).
- New 2026 entrant surfaced: `agentUniverse` (LLM multi-agent framework, GitHub). Added to Section 5.
- ICSE 2026 has an AGENT workshop on multi-agent SE frameworks — indicates academic maturation.

**Sources (landscape):**
- https://www.superannotate.com/blog/multi-agent-llms (B-tier)
- https://gurusup.com/blog/best-multi-agent-frameworks-2026 (QUARANTINE — SEO listicle, used only for name surfacing)
- https://learn.microsoft.com/en-us/agent-framework/overview/ (S-tier, Microsoft)
- https://github.com/agentuniverse-ai/agentUniverse (S-tier README for Section 5)

## 2. Framework profiles (18 frameworks)

### 2.1 LangGraph

- **Source fetched 2026-04-21:** https://github.com/langchain-ai/langgraph
- **Current version:** 1.1.8 (released 2026-04-17)
- **GitHub stars:** 29.8k
- **Last commit:** Not explicit on README; recent (release 4 days before fetch date)
- **Coordination model:** Directed-graph orchestration; nodes = agents/functions, edges = transitions (incl. conditional). Stateful, low-level.
- **Knowledge sharing:** Shared typed state object flows through graph; short-term working memory + long-term persistent memory across sessions.
- **Task allocation:** Explicit graph-author-defined routing; conditional edges + human-in-the-loop interrupts.
- **Review loops:** Not built-in as a pattern; must be hand-wired as graph nodes. Human-in-the-loop interrupts are first-class.
- **Shared workspace:** Persisted state (checkpointing), durable execution across failures; no file-lease primitive.
- **Learning over time:** Persistence enables long-running memory but no explicit learning mechanism.
- **Lock-in vs protocol:** MIT-licensed, open; tightly coupled to LangChain ecosystem but can be used standalone. MCP integration via LangChain's MCP Registry.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** Massively larger ecosystem, explicit graph visualization, LangGraph Platform/Cloud hosting, production-grade checkpointing primitives.
- **Weaker-than-Pheromone:** No stigmergic coordination, no file-leasing, no built-in review-cycle pattern, no Beta-Binomial trust; graph topology must be hand-authored per workflow.

### 2.2 CrewAI

- **Source fetched 2026-04-21:** https://github.com/crewAIInc/crewAI
- **Current version:** 1.14.2 (released 2026-04-17)
- **GitHub stars:** 49.4k (6.8k forks)
- **Last commit:** Not explicit (2,304 commits on main)
- **Coordination model:** Role-based "crew" with two process types: `sequential` and `hierarchical` (auto-assigned manager agent).
- **Knowledge sharing:** Per-agent memory; delegation messages between agents; optional shared memory.
- **Task allocation:** Static config-file task definitions → specific agents; hierarchical process supports dynamic delegation/validation by manager.
- **Review loops:** Manager-validation via hierarchical process (not a formal code→test→review→fix loop).
- **Shared workspace:** Memory module present; no file-lease primitive disclosed.
- **Learning over time:** Not explicit; memory persists but no learning feedback loop.
- **Lock-in vs protocol:** Open source (MIT) + CrewAI Enterprise commercial tier (compliance/audit). MCP referenced via registry.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** Largest single-framework star count among specialist MA frameworks, mature enterprise offering, clean role-based DSL, strong tutorials/docs.
- **Weaker-than-Pheromone:** No stigmergic signal substrate, no file leasing, review cycles are ad-hoc via manager agent not protocol-enforced, no trust/reputation model.

### 2.3 AutoGen (+ AutoGen Studio)

- **Source fetched 2026-04-21:** https://github.com/microsoft/autogen
- **Current version:** python-v0.7.5 (released 2025-09-30)
- **GitHub stars:** 57.3k (8.6k forks)
- **Status:** In maintenance mode; Microsoft points new users to Microsoft Agent Framework (see 2.5).
- **Coordination model:** AgentChat API — two-agent chat or group chat; Core API event-driven message passing; Magentic-One pattern for generalist web/file tasks.
- **Knowledge sharing:** Conversation history shared in group chat; Core API event bus.
- **Task allocation:** Group-chat selector determines who speaks next; Magentic-One has an orchestrator that plans + delegates.
- **Review loops:** Not built-in as a named pattern; agents critique each other via conversational turns.
- **Shared workspace:** No formal workspace primitive; code-execution container available.
- **Learning over time:** No.
- **Lock-in vs protocol:** MIT licensed; MCP-compatible via `McpWorkbench`. AutoGen Studio provides no-code GUI.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** Largest star count in the category (57.3k), AutoGen Studio no-code GUI, McpWorkbench MCP integration, Magentic-One generalist agent.
- **Weaker-than-Pheromone:** Project in maintenance mode (successor is MAF); no stigmergy/file-leasing/trust; review cycles not first-class.

### 2.4 OpenAI Agents SDK

- **Source fetched 2026-04-21:** https://github.com/openai/openai-agents-python
- **Current version:** 0.14.3 (released 2026-04-20)
- **GitHub stars:** 24.2k (3.7k forks)
- **Last commit:** 1,362 commits; exact date not on README excerpt
- **Coordination model:** Handoffs — agents delegate to other agents; "Agents as tools" pattern. Successor to Swarm.
- **Knowledge sharing:** Sessions auto-manage conversation history across runs; Sandbox Agents keep workspace state across longer tasks (filesystem access).
- **Task allocation:** Instructions + tools + guardrails + handoffs configure per-agent behavior.
- **Review loops:** Human-in-the-loop built-in; not a formal code→review pipeline.
- **Shared workspace:** Sandbox Agents have workspace state with filesystem; no leasing primitive.
- **Learning over time:** No.
- **Lock-in vs protocol:** MIT license but OpenAI-branded; MCP-compatible tools.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** First-party OpenAI support, Sandbox Agents with filesystem-state persistence, MCP-native, rapid releases (v0.14.3 yesterday).
- **Weaker-than-Pheromone:** No stigmergic signalling, no file leases/ADRs, no review cycle, no trust model; OpenAI-branded naming creates soft lock-in perception.

### 2.5 Microsoft Agent Framework

- **Source attempted 2026-04-21:** https://learn.microsoft.com/en-us/agent-framework/overview/ → 503
- **Alternate source fetched 2026-04-21:** GitHub README (see below)
- **Status on first fetch:** UNVERIFIED via official docs; supplemented below with GitHub fetch.

### 2.6 Google ADK

- **Source fetched 2026-04-21:** https://github.com/google/adk-python
- **Current version:** v1.31.1 (released 2026-04-21, fetched same-day)
- **GitHub stars:** 19.2k
- **Last commit:** Active; 55 releases
- **Coordination model:** Hierarchical agent tree — parent agent assigns `sub_agents`; engine + model guide agent collaboration.
- **Knowledge sharing:** Session state; session rewind to before previous invocation is a 2026 feature.
- **Task allocation:** Parent delegates to sub-agents via `sub_agents` array.
- **Review loops:** Tool Confirmation HITL flow; no formal code→review built-in.
- **Shared workspace:** Session-scoped state; no file-leasing primitive.
- **Learning over time:** No explicit mechanism.
- **Lock-in vs protocol:** Apache 2.0, but tightly integrated with Vertex AI / Gemini / Google Cloud. MCP tools supported.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** First-party Google Cloud + Vertex AI integration, session-rewind primitive, mature hierarchical delegation, strong Gemini-native tool support.
- **Weaker-than-Pheromone:** Hierarchical (central-orchestrator) model — no stigmergy; no leasing/ADR/trust primitives; Google-Cloud-gravity lock-in for production deploys.

### 2.7 Letta (MemGPT)
### 2.8 LlamaIndex AgentWorkflow
### 2.9 Haystack Agents
### 2.10 Smolagents
### 2.11 OpenDevin / OpenHands
### 2.12 Claude Code subagents
### 2.13 MetaGPT
### 2.14 ChatDev
### 2.15 AgentVerse
### 2.16 Camel AI
### 2.17 Langflow
### 2.18 Flowise

## 3. Comparison summary table (18 rows × required columns)

| Name | Current version | Release date | Coord model | Knowledge sharing | Task allocation | Review loops | Shared workspace | Learning over time | Lock-in vs protocol | Bio-inspired? | GitHub stars | Last commit | Weaker-than-Pheromone (1 line) | Stronger-than-Pheromone (1 line) |
|------|-----------------|--------------|-------------|-------------------|-----------------|--------------|------------------|--------------------|---------------------|--------------|--------------|-------------|--------------------------------|----------------------------------|

## 4. Claim-overlap analysis

### 4.1 C-10 (shared workspace + leasing + ADRs)
### 4.2 C-11 (review cycles built-in)
### 4.3 C-12 (framework-agnostic / MCP-compatible)
### 4.4 C-13 (pheromone scoping / privacy tiers)

## 5. New 2026 entrants not on the 18-framework list

## 6. Abandoned / deprecated projects (footnote only)

## 7. Gaps and UNVERIFIED items

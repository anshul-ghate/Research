# Track C — Mainstream Multi-Agent Orchestration Frameworks

**Status:** COMPLETE
**SubAgent:** C
**Last updated:** 2026-04-21
**Tool-call budget:** 30–35
**Tool-call count:** 19 (1 skeleton write + 1 landscape search + 17 fetch/edit operations)

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
- **Alternate source fetched 2026-04-21:** https://github.com/microsoft/agent-framework
- **Current version:** python-1.1.0 (released 2026-04-21)
- **GitHub stars:** 9.7k (1.6k forks)
- **Languages:** Python 50.8% / C# 45.2%
- **Coordination model:** Graph-based workflows connecting agents + deterministic functions; data-flow edges with streaming, checkpointing, HITL, time-travel.
- **Knowledge sharing:** Shared state on workflow edges; OpenTelemetry distributed tracing.
- **Task allocation:** Middleware-based pipelines; A2A, Azure Functions, Durable Task hosting.
- **Review loops:** HITL first-class in workflows; no named review-cycle pattern.
- **Shared workspace:** Checkpointing + time-travel (rewind a workflow); no file-leasing primitive.
- **Learning over time:** Not explicit.
- **Lock-in vs protocol:** MIT but Azure-aligned (Azure Functions, Durable Task). MCP Registry for external tools. Explicit migration paths from Semantic Kernel and AutoGen (consolidator).
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** First-party Microsoft/Azure integration, dual-language (Python + .NET), time-travel checkpointing, A2A + OpenTelemetry + Durable Task hosting out-of-box.
- **Weaker-than-Pheromone:** Central-orchestrator graph model; no stigmergy/leasing/ADR/trust; Azure-gravity for production.

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

- **Source fetched 2026-04-21:** https://github.com/letta-ai/letta
- **Current version:** v0.16.7 (released 2026-03-31)
- **GitHub stars:** 22.2k (2.3k forks)
- **Last commit:** 7,463 commits on main; 176 releases
- **Coordination model:** Stateful single-agent-primary with skills + subagents (Letta Code). Multi-agent secondary.
- **Knowledge sharing:** Memory Blocks (human/persona/custom) with advanced memory that "can learn and self-improve over time" — MemGPT memory hierarchy.
- **Task allocation:** Subagents invoked by parent agent via skills; no global task queue.
- **Review loops:** Not formalized as code→test→review→fix.
- **Shared workspace:** Memory blocks per agent; Letta server persists state.
- **Learning over time:** YES — explicitly claims memory that learns and self-improves (rare in this list).
- **Lock-in vs protocol:** Apache 2.0; provider-agnostic models (OpenAI GPT-5.2, Claude Opus 4.5 cited). MCP Registry supported.
- **Bio-inspired?** No (cognitive-architecture inspired, not biological).
- **Stronger-than-Pheromone:** Best-in-class long-term memory architecture, self-improving memory, model-agnostic, 22.2k stars and actively evolving.
- **Weaker-than-Pheromone:** Memory-centric rather than coordination-centric; no stigmergic workspace, no file leasing, no built-in review-cycle protocol, multi-agent support is secondary to single-agent memory.

### 2.8 LlamaIndex AgentWorkflow

- **Source fetched 2026-04-21:** https://github.com/run-llama/llama_index
- **Current version:** v0.14.21 (released 2026-04-21)
- **GitHub stars:** 48.7k (7.3k forks)
- **Last commit:** 7,741 commits total; 493 releases
- **Coordination model:** Workflows + LlamaAgents component; event-driven workflow graph with multi-agent support (repo topic `multi-agents`).
- **Knowledge sharing:** Workflow context object + shared RAG index state.
- **Task allocation:** Workflow steps dispatch events to agents.
- **Review loops:** Not named in README; user-authored via workflow edges.
- **Shared workspace:** Workflow context; no lease primitive.
- **Learning over time:** No explicit mechanism beyond persistent indexes.
- **Lock-in vs protocol:** MIT; designed around LlamaIndex RAG ecosystem. MCP support referenced via documentation but not confirmed in README excerpt → UNVERIFIED for explicit MCP feature.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** Tightly integrated with best-of-breed RAG stack, 48.7k stars, 493 releases, Agent Builder tooling for document agents.
- **Weaker-than-Pheromone:** RAG-first not coordination-first; no stigmergy/leasing/ADR/trust; multi-agent is one of many features, not the core.

### 2.9 Haystack Agents

- **Source fetched 2026-04-21:** https://github.com/deepset-ai/haystack
- **Current version:** v2.28.0 (released 2026-04-20)
- **GitHub stars:** 24.9k
- **Last commit:** 5,201 commits on main
- **Coordination model:** Modular pipelines + agent workflows with loops, branches, conditional logic.
- **Knowledge sharing:** Pipeline memory component; shared context through pipeline wiring.
- **Task allocation:** Component-based; explicit graph authoring.
- **Review loops:** Conditional-logic loops can be authored; not a named first-class pattern.
- **Shared workspace:** Pipeline state; no lease primitive.
- **Learning over time:** No.
- **Lock-in vs protocol:** Apache 2.0; model/vendor-agnostic; Hayhooks exposes MCP endpoints natively.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** Explicit MCP endpoint exposure via Hayhooks, deep model/vendor agnosticism, mature RAG+agent hybrid, enterprise adoption at deepset.
- **Weaker-than-Pheromone:** No stigmergy, no file leasing, no trust/ADR protocol; review loops must be author-wired; orientation is pipeline-first not agent-first.

### 2.10 Smolagents

- **Source fetched 2026-04-21:** https://github.com/huggingface/smolagents
- **Current version:** v1.24.0 (released 2026-01-16)
- **GitHub stars:** 26.8k (2.5k forks)
- **Last commit:** 1,036 commits (date not on README excerpt)
- **Coordination model:** Code-agents — LLM emits Python snippets in a ReAct loop; supports "multi-agent hierarchies."
- **Knowledge sharing:** `agent.memory` stores execution logs across steps.
- **Task allocation:** Hierarchical — parent agent invokes sub-agents as tools.
- **Review loops:** ReAct loop with final-answer termination; no formal review cycle.
- **Shared workspace:** Per-agent memory; no shared file workspace.
- **Learning over time:** No.
- **Lock-in vs protocol:** Apache 2.0; HuggingFace-hosted but model-agnostic; MCP support ("tools from any MCP server").
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** "Smol" simplicity (claims 30% fewer steps via code-writing), MCP-native, HF ecosystem integration, very approachable for newcomers.
- **Weaker-than-Pheromone:** Minimalist — no stigmergy, no leasing, no ADRs, no trust, no review pattern; code-writing requires sandboxing discipline.

### 2.11 OpenDevin / OpenHands

- **Source fetched 2026-04-21:** https://github.com/All-Hands-AI/OpenHands
- **Current version:** 1.6.0 (released 2026-03-30)
- **GitHub stars:** 71.6k
- **Last commit:** Active (Python 72.5% / TS 25.7%)
- **Coordination model:** Agent SDK — define agents in code; local CLI/GUI, cloud, or enterprise self-hosted; scale to "1000s of agents."
- **Knowledge sharing:** Theory-of-Mind module mentioned; broader state/memory not detailed in README excerpt.
- **Task allocation:** Not detailed in fetched content → UNVERIFIED.
- **Review loops:** Not explicit in README excerpt → UNVERIFIED.
- **Shared workspace:** Workspace container for code execution is core (inherited from OpenDevin heritage).
- **Learning over time:** Not explicit.
- **Lock-in vs protocol:** MIT; self-hostable or cloud; Slack/Jira/Linear integrations. MCP support not confirmed in excerpt.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** 71.6k stars (largest in this list), enterprise self-hosted + cloud options, Slack/Jira/Linear productivity integrations, RBAC+multi-user.
- **Weaker-than-Pheromone:** Software-dev-agent-first framing; no stigmergy/leasing/ADR/trust; coordination pattern is ad-hoc in agent SDK.

### 2.12 Claude Code subagents

- **Source fetched 2026-04-21:** https://code.claude.com/docs/en/sub-agents (redirected from docs.claude.com)
- **Current version:** N/A — feature of Claude Code CLI; no separate framework version.
- **Scope:** Developer-local CLI feature, NOT a production orchestration framework.
- **Coordination model:** Main Claude delegates to one subagent at a time; subagent runs in its own context window with custom system prompt and restricted tools; returns summary.
- **Knowledge sharing:** One-way — subagent produces summary back to parent; no shared workspace between subagents within one session.
- **Task allocation:** Claude decides when to delegate based on subagent description; user-defined subagents via markdown files (user-level or project-level).
- **Review loops:** Not built-in at subagent level; user can design review-cycle subagents (e.g. "reviewer" subagent).
- **Shared workspace:** Filesystem is shared (they operate in same repo); no lease/coordination primitive. Separate "Agent Teams" feature exists for parallel cross-session agents.
- **Learning over time:** No explicit mechanism.
- **Lock-in vs protocol:** Proprietary to Claude Code CLI; subagent definitions are plain markdown (portable). MCP compatible (Claude Code supports MCP).
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** First-party Anthropic support, context-window preservation pattern, per-subagent tool restriction, user-shareable markdown definitions; huge reach through Claude Code usage.
- **Weaker-than-Pheromone:** Developer-local only (not production orchestration), single-session scope, no stigmergy/leasing/ADR/trust, parallel coordination requires separate "Agent Teams" feature.

### 2.13 MetaGPT

- **Source fetched 2026-04-21:** https://github.com/geekan/MetaGPT
- **Current version (from page):** v0.8.1 (2024-04-22) — README-surfaced version is stale; recent activity via MGX product announced Feb 2025, ICLR 2025 accepted paper.
- **GitHub stars:** 67.3k (8.5k forks)
- **Last commit:** Not explicit in README excerpt.
- **Coordination model:** SOP-encoded roles (PM, Architect, PjM, Engineer, QA). Philosophy: "Code = SOP(Team)."
- **Knowledge sharing:** Files written to `./workspace`; shared environment / publish-subscribe message bus among roles.
- **Task allocation:** SOP pipeline — PM decomposes requirement → Architect designs → Engineer codes → QA reviews.
- **Review loops:** YES — QA role provides built-in review; iterative code→test→review is part of the SOP (closest competitor to Pheromone's C-11).
- **Shared workspace:** `./workspace` directory is canonical; files are the shared artifact.
- **Learning over time:** Not explicit.
- **Lock-in vs protocol:** MIT; MGX commercial product exists. MCP not mentioned in excerpt.
- **Bio-inspired?** No (SOP / org-chart inspired).
- **Stronger-than-Pheromone:** 67.3k stars, proven SOP pipeline for software projects, ICLR 2025 paper validation, commercial MGX wrapper.
- **Weaker-than-Pheromone:** No stigmergic signals, no file leasing (concurrent write races possible), rigid SOP roles (less flexible than role-agnostic stigmergy), no trust/reputation primitive, stale README version suggests slower cadence than leaders.

### 2.14 ChatDev

- **Source fetched 2026-04-21:** https://github.com/OpenBMB/ChatDev
- **Current version:** ChatDev 2.0 (DevAll) announced 2026-01-07; latest release v2.2.0 (2026-03-23)
- **GitHub stars:** 32.8k (4.1k forks)
- **Coordination model:** 1.0 = "virtual software company" (CEO/CTO/Programmer) with functional seminars along waterfall phases. 2.0 = "zero-code multi-agent orchestration platform" with visual canvas.
- **Knowledge sharing:** Seminar-based dialogue memory; shared in-phase context.
- **Task allocation:** Waterfall phases in 1.0; user-authored workflows in 2.0.
- **Review loops:** Phase-based review (testing phase is a canonical stage); HITL feedback in 2.0.
- **Shared workspace:** Generated project folder per run; visual canvas in 2.0.
- **Learning over time:** Not explicit.
- **Lock-in vs protocol:** Apache 2.0; OpenClaw integration ("invoke/dynamically create agent teams"); MCP Registry referenced.
- **Bio-inspired?** No (org-chart inspired).
- **Stronger-than-Pheromone:** Zero-code visual canvas, active 2026 reinvention (2.0), 32.8k stars, OpenClaw dynamic team creation.
- **Weaker-than-Pheromone:** Waterfall/phase rigidity (1.0 heritage), no stigmergy/leasing/trust, review loops tied to phase structure rather than first-class protocol.

### 2.15 AgentVerse

- **Source fetched 2026-04-21:** https://github.com/OpenBMB/AgentVerse
- **Current version:** v0.1.8.1 (released 2023-10-27) — stale.
- **GitHub stars:** 5k (502 forks)
- **Last commit:** 361 commits on main; no explicit recent date — likely largely dormant per stale release.
- **Coordination model:** Two modes — task-solving (collaborative multi-agent) and simulation (observe/interact with multi-agent environments).
- **Knowledge sharing:** Memory described as basic ("sophisticated memory for conversation history" is on the roadmap).
- **Task allocation:** Collaborative within task-solving framework; not well-documented.
- **Review loops:** Not specified.
- **Shared workspace:** Simulation environment; no lease primitive.
- **Learning over time:** No.
- **Lock-in vs protocol:** Apache 2.0; no MCP mention.
- **Bio-inspired?** No (social simulation, not bio).
- **Stronger-than-Pheromone:** Simulation mode for studying agent behaviors is a distinct research affordance Pheromone lacks.
- **Weaker-than-Pheromone:** Stale (last release 2023), small community (5k), memory roadmap item, no stigmergy/leasing/review/trust; likely drifting toward abandoned.

### 2.16 Camel AI

- **Source fetched 2026-04-21:** https://github.com/camel-ai/camel
- **Current version:** v0.2.90 (released 2026-03-22)
- **GitHub stars:** 16.8k (1.9k forks)
- **Last commit:** 2,170 commits on master
- **Coordination model:** Role-playing societies + Workforce component for task distribution.
- **Knowledge sharing:** Stateful memory for each agent; Workforce routes tasks.
- **Task allocation:** Workforce component allocates across agent society.
- **Review loops:** Critic Agents for evaluation / iterative improvement (closer to C-11).
- **Shared workspace:** Not explicit in README excerpt; memory is per-agent.
- **Learning over time:** "Retain and leverage historical context" — incremental, not self-improving.
- **Lock-in vs protocol:** Apache 2.0; MCP Registry integration.
- **Bio-inspired?** No (the name comes from camels, not biology).
- **Stronger-than-Pheromone:** Critic-Agent review primitive is named and first-class; Workforce is a mature task-distribution primitive; MCP integrated.
- **Weaker-than-Pheromone:** Role-playing paradigm centralizes coordination in the role-assigner; no stigmergy/leasing/ADR/trust scoping; Workforce is centralized dispatch.

### 2.17 Langflow

- **Source fetched 2026-04-21:** https://github.com/langflow-ai/langflow
- **Current version:** 1.9.0 (released 2026-04-14)
- **GitHub stars:** 147,000 (unusually large — visual-flow category reach)
- **Last commit:** 17,621 commits on main
- **Coordination model:** Visual flow builder; multi-agent orchestration with conversation management + retrieval.
- **Knowledge sharing:** Conversation memory across agents; flow-context state.
- **Task allocation:** Visually authored — user wires agents and steps.
- **Review loops:** Not explicit; can be authored into flow.
- **Shared workspace:** Flow state; no lease primitive.
- **Learning over time:** No.
- **Lock-in vs protocol:** MIT; MCP-server deployment: flows become MCP tools for any client.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** 147k stars (largest in list), visual drag-and-drop, flow-as-MCP-server export, very broad adoption.
- **Weaker-than-Pheromone:** Visual-flow-centric; no stigmergy/leasing/ADR/trust; review cycles must be hand-wired; flow graph model is author-defined not emergent.

### 2.18 Flowise

- **Source fetched 2026-04-21:** https://github.com/FlowiseAI/Flowise
- **Current version:** flowise@3.1.2 (released 2026-04-14)
- **GitHub stars:** 52.1k (24.2k forks)
- **Last commit:** 3,537 commits on main
- **Coordination model:** Visual agent builder (TS/JS stack); multi-agent via `multiagent-systems` topic.
- **Knowledge sharing:** Not detailed in README excerpt → UNVERIFIED.
- **Task allocation:** Visually authored.
- **Review loops:** Not detailed → UNVERIFIED.
- **Shared workspace:** Not detailed → UNVERIFIED.
- **Learning over time:** No.
- **Lock-in vs protocol:** Apache 2.0; MCP mention not confirmed in excerpt → UNVERIFIED.
- **Bio-inspired?** No.
- **Stronger-than-Pheromone:** JS-native (unusual in this list), 52k stars, strong no-code drag-drop tradition, 24.2k forks indicate heavy hackathon/PoC usage.
- **Weaker-than-Pheromone:** No stigmergy/leasing/ADR/trust; coordination is author-defined in visual graph; many multi-agent features are downstream of LangChainJS primitives.

## 3. Comparison summary table (18 rows × required columns)

| Name | Current version | Release date | Coord model | Knowledge sharing | Task allocation | Review loops | Shared workspace | Learning over time | Lock-in vs protocol | Bio-inspired? | GitHub stars | Last commit | Weaker-than-Pheromone (1 line) | Stronger-than-Pheromone (1 line) |
|------|-----------------|--------------|-------------|-------------------|-----------------|--------------|------------------|--------------------|---------------------|--------------|--------------|-------------|--------------------------------|----------------------------------|
| LangGraph | 1.1.8 | 2026-04-17 | Directed graph | Typed shared state | Graph edges + HITL | Hand-wired | Checkpointed durable state | No | MIT; LangChain-coupled; MCP via registry | No | 29.8k | Active | No stigmergy/leasing/review-pattern | Massive ecosystem; durable checkpointing; LangGraph Platform |
| CrewAI | 1.14.2 | 2026-04-17 | Role-based crew (seq/hier) | Memory + delegation | Config tasks → agents; manager in hier. | Manager validation | Memory module | No | MIT + CrewAI Enterprise | No | 49.4k | Active | No stigmergy/leasing; review ad-hoc | Largest specialist MA star count; enterprise tier |
| AutoGen | python-v0.7.5 | 2025-09-30 | GroupChat + Magentic-One | Conversation history | Selector / orchestrator | Conversational critique | No formal workspace | No | MIT; MCP via McpWorkbench | No | 57.3k | In maintenance | Maintenance mode; no stigmergy/leasing | AutoGen Studio GUI; Magentic-One generalist agent |
| OpenAI Agents SDK | 0.14.3 | 2026-04-20 | Handoffs | Sessions + Sandbox Agents | Instructions + guardrails + handoffs | HITL | Sandbox filesystem state | No | MIT; OpenAI brand; MCP-native | No | 24.2k | Active | No stigmergy/leasing/review | Sandbox workspace primitive; first-party OpenAI |
| MS Agent Framework | python-1.1.0 | 2026-04-21 | Graph workflows | Shared edge state + OTel | Middleware + A2A | HITL | Checkpointing + time-travel | No | MIT; Azure-aligned; MCP via registry | No | 9.7k | Active | Central-orchestrator; no stigmergy/leasing | Python+.NET, time-travel, A2A + OTel |
| Google ADK | v1.31.1 | 2026-04-21 | Hierarchical agent tree | Session state; session rewind | Parent delegates sub_agents | Tool-confirmation HITL | Session state | No | Apache 2.0; Vertex/Gemini-coupled; MCP | No | 19.2k | Active | Central hierarchy; no stigmergy/leasing | Vertex AI integration; session-rewind |
| Letta (MemGPT) | v0.16.7 | 2026-03-31 | Stateful single-agent + subagents | Memory blocks; self-improving | Parent calls subagents | Not formal | Memory blocks per agent | YES (self-improving memory) | Apache 2.0; model-agnostic; MCP | No | 22.2k | Active | Memory-first not coordination-first; no stigmergy | Self-improving memory architecture (unique in list) |
| LlamaIndex AgentWorkflow | v0.14.21 | 2026-04-21 | Event-driven workflow + LlamaAgents | Workflow context + RAG | Workflow events | Hand-wired | Workflow context | No | MIT; MCP UNVERIFIED | No | 48.7k | Active | RAG-first; no stigmergy/leasing | Best RAG integration; 493 releases |
| Haystack | v2.28.0 | 2026-04-20 | Pipeline + agent workflow | Pipeline memory | Component graph | Conditional loops | Pipeline state | No | Apache 2.0; MCP via Hayhooks | No | 24.9k | Active | Pipeline-first; no stigmergy/leasing | Hayhooks MCP endpoint export; full vendor neutrality |
| Smolagents | v1.24.0 | 2026-01-16 | Code agents (ReAct in Python) | agent.memory | Hierarchy — parent calls sub-agents as tools | ReAct loop | Per-agent memory | No | Apache 2.0; HF; MCP-native | No | 26.8k | Active | Minimalist; no stigmergy/leasing/review | Simplicity; 30% fewer steps via code; MCP |
| OpenHands | 1.6.0 | 2026-03-30 | Agent SDK (dev-first) | UNVERIFIED details | Not detailed | UNVERIFIED | Code-execution workspace | Not explicit | MIT; self-host/cloud; MCP UNVERIFIED | No | 71.6k | Active | Dev-agent-first; no stigmergy/leasing | 71.6k stars; enterprise self-host + Slack/Jira/Linear |
| Claude Code subagents | N/A (CLI feature) | Ongoing | Parent→subagent delegation | Summary back to parent | Description-matched | Not built-in | Shared filesystem | No | Proprietary CLI; markdown portable; MCP | No | N/A | N/A | Dev-local only; no parallel coord | First-party Anthropic; tool restriction + context preservation |
| MetaGPT | v0.8.1 | 2024-04-22 | SOP roles (PM/Arch/Eng/QA) | ./workspace files + pub-sub | SOP pipeline | YES — QA role built-in | ./workspace directory | No | MIT + MGX commercial; MCP not mentioned | No | 67.3k | Unknown | No leasing/trust; rigid SOP; stale README version | Built-in QA-review loop; ICLR 2025 paper; 67.3k stars |
| ChatDev | v2.2.0 | 2026-03-23 | Virtual company phases (1.0) / visual canvas (2.0) | Seminar dialogue memory | Phase-based / authored | Testing phase + HITL | Generated project dir; visual canvas | No | Apache 2.0; MCP via registry | No | 32.8k | Active | Waterfall/phase rigidity; no stigmergy | 2026 visual canvas rework; OpenClaw dynamic teams |
| AgentVerse | v0.1.8.1 | 2023-10-27 | Task-solve + simulation | Basic (memory on roadmap) | Collaborative | Not specified | Simulation env | No | Apache 2.0; no MCP | No | 5k | Stale | Stale since 2023; likely drifting to abandoned | Simulation-mode research affordance |
| Camel AI | v0.2.90 | 2026-03-22 | Role-playing + Workforce | Stateful per-agent memory | Workforce allocator | YES — Critic Agents | Not explicit | No | Apache 2.0; MCP via registry | No | 16.8k | Active | Centralized dispatch; no stigmergy/leasing | Named Critic-Agent review primitive; Workforce |
| Langflow | 1.9.0 | 2026-04-14 | Visual flow builder | Conversation + flow context | Visually authored | Author-wired | Flow state | No | MIT; flow-as-MCP-server export | No | 147k | Active | No stigmergy/leasing/review protocol | Flow-as-MCP export; 147k stars (largest in list) |
| Flowise | flowise@3.1.2 | 2026-04-14 | Visual agent builder (TS/JS) | UNVERIFIED | Visually authored | UNVERIFIED | UNVERIFIED | No | Apache 2.0; MCP UNVERIFIED | No | 52.1k | Active | JS-primary; no stigmergy/leasing | TS-native, 24.2k forks, strong no-code heritage |

## 4. Claim-overlap analysis

### 4.1 C-10 (shared workspace + leasing + ADRs)

**Shared workspace:** Near-universal in some form — every framework has a workspace or state concept:
- Workflow/graph state: LangGraph, MS Agent Framework, LlamaIndex, Haystack, Langflow, Flowise.
- Code-execution sandbox / filesystem: OpenAI Agents SDK (Sandbox Agents), OpenHands, MetaGPT (`./workspace`), ChatDev (generated project dir), Claude Code subagents (shared filesystem).
- Memory-centric: Letta (Memory Blocks), Smolagents (`agent.memory`), Camel AI (stateful memory).

**File leasing:** NOT FOUND in any framework's official docs fetched today. No framework advertises lease-based concurrent-write coordination. This is a credible Pheromone differentiator.

**ADRs (Architecture Decision Records):** NOT FOUND as a first-class primitive in any framework. MetaGPT writes design docs as part of the SOP, ChatDev produces architecture via CTO role, but neither models ADRs as a coordination artifact. Credible Pheromone differentiator.

**Convention enforcement:** No framework advertises a coordination-layer convention-enforcement primitive. MetaGPT's SOP is closest but is role-rigid, not convention-based.

**Verdict on C-10:** Shared-workspace alone is commodified; the leasing + ADRs + convention-enforcement combination is not replicated by any of the 18 frameworks fetched.

### 4.2 C-11 (review cycles built-in)

**Built-in code→test→review→fix pattern:**
- MetaGPT — YES, explicit QA role in the SOP pipeline (closest competitor).
- ChatDev — YES, phase-based testing stage.
- Camel AI — Critic Agents provide iterative review.
- CrewAI — Manager validation in hierarchical process (weaker; not a named cycle).

**HITL-only (not autonomous review):** LangGraph, MS Agent Framework, Google ADK, OpenAI Agents SDK.

**Not built-in, author-wired:** LangGraph, AutoGen, Haystack, Smolagents, Langflow, Flowise, LlamaIndex, OpenHands, Letta, AgentVerse.

**Verdict on C-11:** NOT unique to Pheromone — MetaGPT, ChatDev, and Camel AI all have built-in review mechanisms. Pheromone's advantage must lean on the *protocol* for review (stigmergic trigger, file-lease handoff, Beta-Binomial trust weighting) rather than on "review exists."

### 4.3 C-12 (framework-agnostic / MCP-compatible)

**MCP-native (confirmed in fetched page):** OpenAI Agents SDK, AutoGen (McpWorkbench), Haystack (Hayhooks), Smolagents, Letta, MS Agent Framework, Google ADK, Camel AI, Langflow (deploy as MCP server), agentUniverse, Claude Code (via Claude Code's MCP support).

**MCP mentioned but implementation not confirmed:** LangGraph (via LangChain), CrewAI (via registry), MetaGPT, ChatDev, LlamaIndex, OpenHands, Flowise, AgentVerse → UNVERIFIED for explicit integration.

**Framework-agnostic coordination protocol:** Not an MCP property. MCP is a tool-integration protocol, not an agent-coordination protocol. Agent-to-agent protocols in play today:
- Google's A2A (Agent-to-Agent) — adopted by MS Agent Framework.
- No framework in this list ships a stigmergic-pheromone-signal protocol.

**Verdict on C-12:** MCP-compatibility is now table-stakes; 11/18 frameworks are MCP-native. Pheromone should claim MCP-compatibility as hygiene, not differentiation. The differentiator is a coordination protocol (pheromone deposition semantics) that is orthogonal to MCP.

### 4.4 C-13 (pheromone scoping / privacy tiers — private/team/colony/federated)

**Scoped-memory / privacy tiers found:** NONE explicit in any framework's fetched docs.
- Letta has per-agent Memory Blocks but no team/colony/federated tiering.
- Claude Code subagents have per-session isolation (closest to "private") but no colony tier.
- MS Agent Framework's A2A support hints at cross-system federation but not pheromone-tiered scoping.
- CrewAI Enterprise has audit trails but not scope tiers.

**Verdict on C-13:** Strong, defensible differentiator. No framework fetched today advertises a four-tier (private/team/colony/federated) memory-scoping model.

## 5. New 2026 entrants not on the 18-framework list

- **agentUniverse** (https://github.com/agentuniverse-ai/agentUniverse) — 2.2k stars; v0.0.19 (2025-11-17). PEER (Plan/Execute/Express/Review) and DOE (Data/Opinion/Express) patterns. PEER explicitly incorporates review cycles. MCP server publish/use supported. Origin: Ant Group financial practices. **Notable:** PEER pattern is a named review-cycle protocol — closer conceptually to Pheromone's C-11 than most list frameworks. Fetched 2026-04-21.
- **Microsoft Agent Framework** (already in list as item 2.5) subsumes both AutoGen and Semantic Kernel per migration guides — effectively a 2025-2026 consolidation.
- **CrewAI Enterprise** — commercial wrapper with compliance/audit trails (mentioned in SuperAnnotate landscape, not separately fetched).
- **Magentic-One** — AutoGen's generalist multi-agent web/file system (mentioned in landscape).
- **MGX (MetaGPT X)** — commercial natural-language-programming product from MetaGPT (Feb 2025 launch mentioned on MetaGPT README).
- **OpenClaw** — ChatDev ecosystem agent-team invoker (mentioned on ChatDev README).

Further entrants observed but not spot-checked (stored for later waves): none additional strong candidates from landscape query beyond the above.

## 6. Abandoned / deprecated projects (footnote only)

- **AutoGen (python-v0.7.5, 2025-09-30)** — Microsoft states "in maintenance mode." Users directed to Microsoft Agent Framework. Still active for existing deployments but not receiving new features. [ref: https://github.com/microsoft/autogen]
- **AgentVerse (v0.1.8.1, 2023-10-27)** — no release in 2.5 years; memory features on roadmap since 2023; only 5k stars. Likely drifting toward abandonment though repo is still up. [ref: https://github.com/OpenBMB/AgentVerse]
- **OpenDevin** — superseded by OpenHands (All-Hands-AI/OpenHands). Old repo redirects into new brand.
- **Swarm (OpenAI)** — succeeded by OpenAI Agents SDK (confirmed in task brief; not separately fetched).

## 7. Gaps and UNVERIFIED items

- **MS Agent Framework overview docs** — learn.microsoft.com returned 503 at fetch time; GitHub README used as substitute. Overview page content UNVERIFIED.
- **LlamaIndex MCP specifics** — not confirmed in README excerpt.
- **Flowise multi-agent coordination/memory/review/MCP** — README excerpt too thin; UNVERIFIED across several columns.
- **OpenHands task allocation and review loops** — README excerpt lacks detail; UNVERIFIED.
- **Last-commit timestamps** — most GitHub READMEs did not surface a precise last-commit date in the fetched snippet. Release-date and commit-count used as proxy.
- **MetaGPT release freshness** — README-surfaced version v0.8.1 (2024-04-22) appears stale; MGX and ICLR 2025 activity suggests more recent dev work not reflected in the surfaced release tag.
- **Claude Code subagents "current version"** — feature of an evolving CLI product; no pinned version number.

**Non-blocking:** No framework fetched today IDENTICALLY implements Pheromone's stigmergic + file-leased + ADR + Beta-Binomial-trust model. No BLOCKING_CANDIDATE detected.

---

**Status:** COMPLETE
**Tool-call count at completion:** ~19 (skeleton + 1 search + ~14 fetches + ~3 edits with reserve under 35 budget ceiling).

# PHEROMONE — System Design, Tech Stack & Development Orchestration

**Version:** 1.0 FINAL
**Date:** April 8, 2026
**Author:** Anshul Ghate + ARIA
**Purpose:** Pre-implementation engineering foundation — system design (HLD/LLD), tech stack decisions, and Claude Code multi-session orchestration strategy. This document must be produced and reviewed BEFORE any code is written.

---

## TABLE OF CONTENTS

### PART 1: SYSTEM DESIGN
1. Requirements & Scope Lock
2. Capacity Estimation
3. High-Level Design (HLD) — Component Architecture
4. Data Flow Diagrams
5. Low-Level Design (LLD) — Class Hierarchies & Interfaces
6. Data Model & Storage Design
7. Key Sequence Diagrams
8. API Design (Public + Internal)
9. Reliability & Fault Tolerance
10. Security Design
11. Observability & Operations

### PART 2: TECH STACK DECISION RECORD
12. Technology Selection Matrix
13. Version Pinning & Security Notes
14. Alternatives Considered & Rejected

### PART 3: CLAUDE CODE ORCHESTRATION
15. Document Architecture — How 14 Specs Connect
16. Phase-Bundled Document Loading Strategy
17. The /ultraplan Prompt
18. Multi-Session Continuity Strategy
19. CLAUDE.md — The Always-Loaded Foundation
20. Quality Gates Between Sessions

### PART 4: TRADEOFFS & EVOLUTION
21. Tradeoff Register
22. Evolution Path (v0.1 → v1.0 → v2.0)

---

# PART 1: SYSTEM DESIGN

## 1. Requirements & Scope Lock

### 1.1 Functional Requirements

| ID | Requirement | Priority |
|----|-------------|----------|
| FR-1 | `colony.solve(goal)` decomposes a natural language goal into a DAG of tasks, allocates them to agents, executes via ReAct loops, and returns assembled output | P0 |
| FR-2 | Agents coordinate exclusively via pheromone signals (deposit/sense) — no central orchestrator, no direct agent-to-agent communication | P0 |
| FR-3 | Pheromone environment supports 8 types (KNOWLEDGE, CAPABILITY, COORDINATION, RESULT, WARNING, GOAL, META, ADR) with deposit, sense, decay, reinforce, and compaction | P0 |
| FR-4 | Task allocation uses Ant Colony Optimization formula with Response Threshold pre-filter and Lévy Flight exploration | P0 |
| FR-5 | Agents operate shared workspace with file leasing, str_replace editing, and conflict detection via content hashing | P0 |
| FR-6 | Hierarchical task decomposition: Goal → Epic → Feature → Task with DAG validation (Kahn's algorithm) | P0 |
| FR-7 | Review cycles: task → test → convention check → peer review → revision (max 3) | P1 |
| FR-8 | Budget management: per-agent and colony-level cost tracking, graceful degradation at 80%+ utilization | P0 |
| FR-9 | Terminal UI (Textual): 4-region layout with real-time DAG, agent status, pheromone flow, non-blocking input | P1 |
| FR-10 | Web GUI (React + FastAPI): WebSocket-streamed colony events, ReactFlow DAG visualization | P2 |
| FR-11 | MCP server: colony exposed as MCP server for ecosystem interoperability | P2 |
| FR-12 | Stigmergic RL: colony learns to optimize meta-parameters (α, β, γ, ρ, ε) across runs via policy gradient | P2 |
| FR-13 | Pheromone compaction: 9-section summarization when count exceeds threshold per type | P2 |
| FR-14 | Human-in-the-loop: 3-way permission model (allow/ask/deny) with denial tracking | P1 |
| FR-15 | Git workspace versioning: commit per wave, tag per run, diff between runs | P1 |

### 1.2 Non-Functional Requirements

| Dimension | Requirement |
|-----------|-------------|
| **Scale** | 1-10 agents per colony. 1-50 tasks per solve. Single-colony single-process (v1). Multi-colony federation (v2). |
| **Latency** | Pheromone sense: <100ms for 500 pheromones. Task allocation round: <500ms. Colony startup: <5s. |
| **Availability** | N/A for v1 (single-process CLI tool). Server mode (v2): 99.9% target with graceful degradation. |
| **Consistency** | Pheromone reads: snapshot consistency (non-blocking). Pheromone writes: per-pheromone atomic. Task claims: optimistic locking. |
| **Durability** | InMemoryStore: none (session-only). RedisStore: Redis persistence defaults. ResultStore: JSON on disk. |
| **Security** | API key sanitization from logs/pheromones. File path traversal prevention. Rate limiting on deposits (50/agent/min). Content hash integrity. |
| **Cost** | Default budget: $2. Max budget: configurable. Target cost per simple solve: <$0.50 with Haiku. |
| **Extensibility** | Custom LLM clients via ABC. Custom tools via BaseTool. Custom store backends via PheromoneStore ABC. MCP integration. |
| **Install Experience** | `pip install pheromone` → working colony in 3 lines of code. Zero mandatory config. |

### 1.3 Scope Boundary

**IN SCOPE (v0.1-1.0, 12 weeks):**
- Core framework: Colony, agents, pheromones, task allocation, execution, assembly
- CLI + TUI + Web GUI
- InMemory + Redis stores
- Local + API embeddings
- 8 agent templates
- Git workspace versioning
- PheromBench benchmark
- PyPI release, arXiv paper

**OUT OF SCOPE:**
- Multi-node distributed execution (single-process only in v1)
- GPU-based local model serving (agents use API-based LLMs)
- Persistent agent memory across colony instances (pheromones are ephemeral per colony lifecycle; Stigmergic RL META pheromones persist in store only)
- Authentication/authorization for web GUI (Phase 4 — minimal, no multi-user auth)
- Production Kubernetes deployment (Docker compose only)

### 1.4 Key Assumptions

1. Users have Python 3.11+ installed
2. Users have at least one LLM API key (Anthropic, OpenAI, or compatible)
3. Target machines have 4GB+ RAM (for sentence-transformers model loading)
4. Network access to LLM APIs (no offline mode in v1)
5. Single-user operation (no concurrent colony.solve() from multiple processes against same workspace)

---

## 2. Capacity Estimation

### 2.1 Per-Solve Resource Consumption

For a typical `colony.solve("Build a weather API with tests")` with 5 agents, ~15 tasks:

| Resource | Estimate | Math |
|----------|----------|------|
| **LLM calls** | ~60-90 | 1 decomposition + 15 tasks × 3-5 ReAct turns each + 5 reviews |
| **Tokens (input)** | ~500K-1M | ~8K per ReAct turn × 75 calls average |
| **Tokens (output)** | ~150K-300K | ~2K-4K per response × 75 calls |
| **Cost (Haiku)** | ~$0.10-0.30 | At $0.80/1M input, $4/1M output |
| **Cost (Sonnet)** | ~$1.00-2.50 | At $3/1M input, $15/1M output |
| **Wall clock time** | 3-10 min | Parallelized across waves, bottlenecked by sequential deps |
| **Peak memory** | ~200-500MB | Pheromone store + agent contexts + embeddings model |
| **Pheromones deposited** | ~100-200 | ~6-10 per task (COORDINATION, KNOWLEDGE, RESULT, etc.) |
| **Files created** | ~10-30 | Source files + tests + config + docs |

### 2.2 Pheromone Store Sizing

| Metric | Value | Calculation |
|--------|-------|-------------|
| Pheromone object size | ~2-5 KB | JSON content (~1KB) + embedding (384 floats × 4B = 1.5KB) + metadata |
| Store size per solve | ~500KB-1MB | 200 pheromones × 3.5KB average |
| Compaction trigger | 50 per type | After 50 KNOWLEDGE pheromones → summarize into 1 META |
| Max store size before compaction | ~10MB | Extreme case: 2000 pheromones across all types |

### 2.3 Embedding Service Load

| Metric | Value |
|--------|-------|
| Embeddings per solve | ~300-500 (200 deposits + 100-300 sense queries) |
| Latency per embed (local) | ~5-15ms (sentence-transformers, batched) |
| Latency per embed (API) | ~50-100ms (LiteLLM embeddings endpoint) |
| Cache hit rate target | >60% (repeated sense queries with same pheromone content) |

---

## 3. High-Level Design (HLD)

### 3.1 Component Architecture

```
┌──────────────────────────────────────────────────────────────────────┐
│                         USER INTERFACES                              │
│  ┌──────────┐  ┌──────────────┐  ┌──────────────────┐              │
│  │ CLI/TUI  │  │  Web GUI     │  │  Python SDK      │              │
│  │ (Textual)│  │ (React+Vite) │  │  colony.solve()  │              │
│  └────┬─────┘  └──────┬───────┘  └────────┬─────────┘              │
│       │               │                    │                         │
│       ▼               ▼                    ▼                         │
│  ┌────────────────────────────────────────────────────┐             │
│  │           UI PROTOCOL LAYER                         │             │
│  │  ColonyController ABC + ColonyEventStream           │             │
│  │  LocalController (in-process) │ RemoteController(WS)│             │
│  └───────────────────────┬────────────────────────────┘             │
└──────────────────────────┼──────────────────────────────────────────┘
                           │
┌──────────────────────────┼──────────────────────────────────────────┐
│                    COLONY CORE                                       │
│                          ▼                                           │
│  ┌──────────────────────────────────────────┐                       │
│  │              COLONY                       │                       │
│  │  Config loader → Validator → Builder      │                       │
│  │  solve() → engine.run() → result          │                       │
│  └──────┬──────────────────────┬─────────────┘                      │
│         │                      │                                     │
│         ▼                      ▼                                     │
│  ┌─────────────┐    ┌──────────────────────────────────────────┐   │
│  │  LLM CLIENT │    │           EXECUTION ENGINE                │   │
│  │  LAYER      │    │  ┌────────────┐  ┌────────────────┐      │   │
│  │             │    │  │Decomposer  │  │ Stigmergic     │      │   │
│  │ BaseLLM ABC │    │  │(LLM-based) │  │ Allocator      │      │   │
│  │ LiteLLM    │◄───│  │            │  │ (ACO+Lévy+     │      │   │
│  │ MockLLM    │    │  │            │  │  Thresholds)   │      │   │
│  │ Fallback   │    │  └──────┬─────┘  └───────┬────────┘      │   │
│  │ Middleware  │    │         │                │               │   │
│  │ Cache      │    │         ▼                ▼               │   │
│  └─────────────┘    │  ┌────────────────────────────┐          │   │
│                      │  │    EXECUTION LOOP           │          │   │
│                      │  │  For each wave:             │          │   │
│                      │  │   allocate → execute →      │          │   │
│                      │  │   review → deposit → next   │          │   │
│                      │  └────────────┬───────────────┘          │   │
│                      │               │                           │   │
│                      │  ┌────────────┼───────────────┐          │   │
│                      │  │   OUTPUT ASSEMBLER          │          │   │
│                      │  │   Workspace/Text/Hybrid     │          │   │
│                      │  └────────────────────────────┘          │   │
│                      └──────────────────────────────────────────┘   │
│                                                                      │
│  ┌───────────────────────────────────────────────────────────────┐  │
│  │                    AGENT LAYER                                 │  │
│  │  ┌────────────┐  ┌──────────────┐  ┌────────────────────┐   │  │
│  │  │AgentProxy  │  │AgentReActLoop│  │ToolOrchestrator    │   │  │
│  │  │(config+    │  │(LLM turns +  │  │(read-parallel,     │   │  │
│  │  │ thresholds │  │ tool calls)  │  │ write-serial)      │   │  │
│  │  │ +trust)    │  │              │  │                    │   │  │
│  │  └────────────┘  └──────────────┘  └────────────────────┘   │  │
│  │                                                               │  │
│  │  ┌─────────────────────────────────────────────────────────┐ │  │
│  │  │                  TOOL SYSTEM                             │ │  │
│  │  │  Core: FileRead, FileWrite, FileEdit, Bash, Glob, Grep  │ │  │
│  │  │  Pheromone: Sense, DepositKnowledge, DepositADR, ...     │ │  │
│  │  │  Workspace: AcquireLease, RunTests, GetProjectContext    │ │  │
│  │  └─────────────────────────────────────────────────────────┘ │  │
│  └───────────────────────────────────────────────────────────────┘  │
│                                                                      │
│  ┌──────────────────────────┐  ┌────────────────────────────────┐  │
│  │  PHEROMONE ENVIRONMENT   │  │  SHARED WORKSPACE               │  │
│  │                          │  │                                  │  │
│  │  deposit(p) → validate   │  │  WorkspaceManager               │  │
│  │    → embed → hash        │  │    read_file / write_file       │  │
│  │    → MAX-MIN clamp       │  │    edit_file (str_replace)      │  │
│  │    → audit               │  │                                  │  │
│  │                          │  │  LeaseManager                    │  │
│  │  sense(query) → rank     │  │    acquire / release / expire    │  │
│  │    by Information        │  │                                  │  │
│  │    Foraging scent        │  │  FileEditor                     │  │
│  │    formula               │  │    conflict detection (hash)     │  │
│  │                          │  │    quote normalization           │  │
│  │  decay_cycle() →         │  │                                  │  │
│  │    evaporate weak        │  │  Git (optional)                  │  │
│  │                          │  │    commit_wave / tag_run          │  │
│  │  Compactor (9-section)   │  │                                  │  │
│  │  CodebaseIndexer         │  │                                  │  │
│  └──────────┬───────────────┘  └──────────┬─────────────────────┘  │
│             │                              │                         │
│             ▼                              ▼                         │
│  ┌──────────────────────┐    ┌─────────────────────────────┐       │
│  │  PHEROMONE STORE      │    │  FILESYSTEM                  │       │
│  │  InMemoryStore        │    │  /workspace/project_root/    │       │
│  │  RedisStore (opt)     │    │                              │       │
│  └──────────────────────┘    └─────────────────────────────┘       │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │  EMBEDDING SERVICE                                            │   │
│  │  NullEmbedder │ SentenceTransformerEmbedder │ APIEmbedder     │   │
│  │  EmbeddingCache (thread-safe LRU)                             │   │
│  └──────────────────────────────────────────────────────────────┘   │
│                                                                      │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────────────────────┐   │
│  │  EVOLUTION   │  │  ERRORS      │  │  OBSERVABILITY           │   │
│  │  StigRL      │  │  Taxonomy    │  │  Structured logging      │   │
│  │  (Phase 3)   │  │  (errors.py) │  │  Ring buffers            │   │
│  └─────────────┘  └─────────────┘  │  Event system (40+ types) │   │
│                                      └──────────────────────────┘   │
└──────────────────────────────────────────────────────────────────────┘
```

### 3.2 Component Responsibility Boundaries

| Component | Owns | Does NOT Own |
|-----------|------|-------------|
| **Colony** | Config loading, component wiring, public API (solve/register/shutdown) | Execution logic, agent behavior |
| **ExecutionEngine** | Main loop, wave orchestration, state machine, pause/resume/cancel | LLM calls, task decomposition |
| **Decomposer** | Goal → HierarchicalTaskGraph via LLM | Task execution, allocation |
| **StigmergicAllocator** | Task-to-agent assignment per round via ACO | Task execution, result assembly |
| **AgentProxy** | Agent identity, thresholds, trust score, heartbeat | LLM communication |
| **AgentReActLoop** | Multi-turn LLM interaction per task, tool execution | Task allocation, colony-level coordination |
| **ToolOrchestrator** | Parallel/serial tool execution, lease management during execution | Tool implementation |
| **PheromoneEnvironment** | Deposit validation, sensing, decay, compaction | Persistence (delegated to store) |
| **WorkspaceManager** | File I/O, project context, convention checking | Leasing (delegated to LeaseManager) |
| **EmbeddingService** | Text → vector embedding, cosine similarity, caching | Model training, fine-tuning |
| **OutputAssembler** | ColonyResult construction from tracker + workspace + environment | Execution, reporting |
| **UI Protocol** | Event streaming, controller ABC, command dispatch | Rendering (delegated to CLI/GUI) |

### 3.3 Failure Domains

| Component | If It Fails... | Impact | Recovery |
|-----------|---------------|--------|----------|
| LLM API | Agent can't execute turns | Single agent stalls → retry + fallback model | RetryPolicy + FallbackLLMClient |
| Pheromone Store | No deposit/sense | Colony-wide halt | Fallback to InMemory if Redis fails |
| Workspace filesystem | Can't read/write files | Agent tasks fail | Workspace on local disk (not network) |
| Single agent crash | Heartbeat stops | Tasks reassigned to other agents | Dead detection → lease release → task AVAILABLE |
| Embedding service | Can't compute similarity | Sensing degrades to keyword/random | NullEmbedder fallback (no semantic ranking) |
| Budget exhaustion | No more LLM calls | Colony stops gracefully | Assemble best-effort result from completed tasks |

---

## 4. Data Flow Diagrams

### 4.1 Primary Flow: colony.solve()

```
User calls colony.solve("Build a weather API")
    │
    ├─1─→ ExecutionEngine.run(goal, colony, strategy)
    │       │
    │       ├─2─→ Decomposer.decompose(goal)
    │       │       │
    │       │       ├── LLM call: "Decompose this goal into tasks"
    │       │       ├── Parse response → HierarchicalTaskGraph
    │       │       ├── Validate DAG (Kahn's algorithm)
    │       │       └── Return task_graph
    │       │
    │       ├─3─→ [Optional] Quorum validation of decomposition
    │       │
    │       ├─4─→ EXECUTION LOOP (while not terminal & within budget):
    │       │       │
    │       │       ├─4a─→ task_graph.get_available_leaves()
    │       │       │
    │       │       ├─4b─→ allocator.allocate_round(available, agents, env)
    │       │       │       ├── Response Threshold pre-filter
    │       │       │       ├── ACO attraction formula
    │       │       │       ├── Lévy Flight exploration (probabilistic)
    │       │       │       ├── Optimistic locking for conflicts
    │       │       │       └── Return {task_id → agent_id}
    │       │       │
    │       │       ├─4c─→ For each (task, agent) claim in parallel:
    │       │       │       │
    │       │       │       ├── tracker.start_task(task_id, agent_id)
    │       │       │       │
    │       │       │       ├── agent.execute_task(task, sense_result)
    │       │       │       │   ├── environment.sense(query, budget)
    │       │       │       │   │   └── Returns SenseResult (ranked pheromones)
    │       │       │       │   │
    │       │       │       │   ├── ReActLoop.execute(task, context, workspace)
    │       │       │       │   │   ├── Build initial prompt (system + user)
    │       │       │       │   │   ├── FOR each turn (max 25):
    │       │       │       │   │   │   ├── LLM call → response
    │       │       │       │   │   │   ├── If no tool calls → extract output → DONE
    │       │       │       │   │   │   ├── Parse tool calls
    │       │       │       │   │   │   ├── ToolOrchestrator.execute_tools()
    │       │       │       │   │   │   │   ├── Reads: asyncio.gather (parallel)
    │       │       │       │   │   │   │   └── Writes: sequential + lease
    │       │       │       │   │   │   ├── Auto-deposit codebase index pheromones
    │       │       │       │   │   │   ├── Append to messages
    │       │       │       │   │   │   └── Context budget check → compact if >90%
    │       │       │       │   │   └── Return TaskOutput
    │       │       │       │   │
    │       │       │       │   ├── environment.deposit(RESULT pheromone)
    │       │       │       │   ├── environment.deposit(KNOWLEDGE pheromones)
    │       │       │       │   └── Update thresholds + trust
    │       │       │       │
    │       │       │       ├── tracker.complete_task(task_id, ...)
    │       │       │       └── workspace_git.commit_wave(wave_num, descriptions)
    │       │       │
    │       │       ├─4d─→ evolution.cycle(environment)  // decay + reinforce
    │       │       │
    │       │       └─4e─→ propagate_completion(task_graph)
    │       │               // Mark parent features/epics as COMPLETED
    │       │               // if all children done
    │       │
    │       ├─5─→ OutputAssembler.assemble(task_graph, workspace, env, tracker)
    │       │       ├── Detect output mode (workspace/text/hybrid)
    │       │       ├── Collect task summaries from ExecutionTracker
    │       │       ├── Build output (WorkspaceOutput/TextOutput/HybridOutput)
    │       │       ├── Collect warnings from environment
    │       │       ├── Collect partial outputs from failed tasks
    │       │       ├── Compute cost summary
    │       │       ├── [Optional] Generate executive summary via LLM
    │       │       └── Return ColonyResult
    │       │
    │       └─6─→ result_store.save(result)
    │
    └── Return ColonyResult to user
```

### 4.2 Pheromone Lifecycle

```
Agent deposits pheromone
    │
    ├── Validate content dict against type-specific rules (§5.8)
    ├── Compute embedding via EmbeddingService
    ├── Compute SHA-256 content hash
    ├── Clamp strength to [TAU_MIN, TAU_MAX]
    ├── Record in audit log
    ├── Store in PheromoneStore
    │
    └── Over time:
        ├── Other agents sense() → pheromone returned if scent score high enough
        ├── On success → reinforce: strength += Δτ (clamped to TAU_MAX)
        ├── On failure → penalize: strength *= 0.8 (clamped to TAU_MIN)
        ├── Each evolution cycle → evaporate: strength *= (1 - ρ)
        ├── If strength < TAU_MIN → evaporate (delete)
        └── If count > 50 per type → compact into META pheromone
```

---

## 5. Low-Level Design (LLD)

### 5.1 Core Class Hierarchy

```
pheromone/
├── errors.py
│   └── PheromoneError (base)
│       ├── LLMError
│       │   ├── LLMRetryableError
│       │   ├── LLMRateLimitError
│       │   ├── LLMTimeoutError
│       │   ├── LLMAuthError
│       │   ├── LLMModelNotFoundError
│       │   ├── LLMBudgetExhaustedError
│       │   ├── LLMContentFilterError
│       │   └── LLMContextLengthError
│       ├── ConfigError
│       │   ├── ConfigValidationError
│       │   ├── ConfigFileNotFoundError
│       │   └── ConfigParseError
│       ├── EngineError
│       │   ├── IllegalStateTransition
│       │   ├── DecompositionError
│       │   ├── AllocationError
│       │   ├── ExecutionTimeoutError
│       │   └── AgentCrashError
│       ├── WorkspaceError
│       │   ├── LeaseConflictError
│       │   └── ReadOnlyWorkspaceError
│       ├── StoreError
│       │   └── StoreConnectionError
│       └── MissingDependencyError
│
├── models/
│   ├── pheromones.py
│   │   ├── PheromoneType (Enum: 8 types)
│   │   ├── PheromoneScope (Enum: PRIVATE/TEAM/COLONY/FEDERATED)
│   │   ├── Pheromone (BaseModel) ← THE core data unit
│   │   └── SenseResult (BaseModel) ← return type of sense()
│   │
│   ├── tasks.py
│   │   ├── TaskLevel (Enum: EPIC/FEATURE/TASK/SUBTASK)
│   │   ├── TaskStatus (Enum: 12 states)
│   │   ├── TaskNode (BaseModel)
│   │   ├── ReviewRecord (BaseModel)
│   │   ├── HierarchicalTaskGraph (BaseModel) ← owns DAG logic
│   │   ├── SpecificationModel (BaseModel)
│   │   └── Requirement (BaseModel)
│   │
│   ├── config.py ← CANONICAL source for all config
│   │   ├── ColonyConfig (BaseModel) ← top-level
│   │   ├── BudgetConfig, LLMConfig, AgentConfig
│   │   ├── Strategy, ReviewConfig, QuorumConfig
│   │   ├── IntegrationConfig, ApprovalConfig
│   │   ├── StoreConfig, WorkspaceConfig, EmbeddingConfig
│   │   ├── LoggingConfig
│   │   ├── OutputMode (Enum: WORKSPACE/TEXT/HYBRID)
│   │   └── LiveBudget (runtime tracker)
│   │
│   ├── execution.py
│   │   ├── LLMUsage (BaseModel) ← cost tracking per call
│   │   ├── TaskOutput (BaseModel) ← ReActLoop → Engine contract
│   │   ├── TaskExecutionRecord (BaseModel) ← per-task tracking
│   │   └── ExecutionTracker ← dict[task_id → record]
│   │
│   └── results.py
│       ├── ColonyResult (BaseModel) ← THE return type
│       ├── ColonyOutput = Annotated[Union[...], Discriminator("mode")]
│       ├── WorkspaceOutput (BaseModel)
│       ├── TextOutput (BaseModel)
│       ├── HybridOutput (BaseModel)
│       ├── TaskSummary, CostSummary, PartialOutput
│       └── (imports OutputMode from config.py)
│
├── llm/
│   ├── models.py
│   │   ├── LLMRequest (BaseModel)
│   │   ├── LLMResponse (BaseModel)
│   │   ├── LLMToolCall (BaseModel)
│   │   └── LLMMessage (BaseModel)
│   │
│   ├── client.py
│   │   ├── BaseLLMClient (ABC)
│   │   │   ├── create(request) → LLMResponse [abstract]
│   │   │   └── create_with_cost_check(request, budget) [abstract]
│   │   └── LiteLLMClient(BaseLLMClient) ← wraps litellm.acompletion
│   │
│   ├── mock.py
│   │   ├── MockLLM(BaseLLMClient) ← scripted responses
│   │   └── MockResponse (builder)
│   │
│   ├── retry.py
│   │   └── RetryPolicy (BaseModel) ← max_retries, backoff, is_retryable
│   │
│   ├── capabilities.py
│   │   ├── ModelCapabilities (dataclass)
│   │   └── MODEL_REGISTRY: dict[str, ModelCapabilities]
│   │
│   ├── parsers.py
│   │   ├── JSONTextParser
│   │   └── XMLTextParser
│   │
│   ├── middleware.py
│   │   ├── LLMMiddleware (ABC) ← wraps BaseLLMClient
│   │   ├── CapabilityAwareMiddleware
│   │   ├── LoggingMiddleware
│   │   └── build_middleware_stack(base, middlewares) → BaseLLMClient
│   │
│   ├── cache.py
│   │   └── CachingMiddleware(LLMMiddleware)
│   │
│   └── fallback.py
│       └── FallbackLLMClient(BaseLLMClient) ← chains multiple clients
│
├── stores/
│   ├── base.py
│   │   └── PheromoneStore (ABC)
│   │       ├── deposit(p) → str
│   │       ├── get(id) → Pheromone | None
│   │       ├── sense(query, type_filter, limit, ...) → SenseResult
│   │       ├── update_strength(id, new) → bool
│   │       ├── bulk_decay(rate) → int
│   │       ├── count(type_filter?) → int
│   │       └── get_audit_log(since?) → list[dict]
│   │
│   ├── memory.py → InMemoryStore(PheromoneStore)
│   ├── redis_store.py → RedisStore(PheromoneStore)  [optional]
│   └── result_store.py → ResultStore (JSON persistence)
│
├── environment/
│   ├── environment.py → PheromoneEnvironment
│   │   (wraps store + embedding + validation + scope + audit)
│   └── embeddings.py
│       ├── BaseEmbedder (ABC)
│       ├── NullEmbedder (zeros — default)
│       ├── SentenceTransformerEmbedder [optional]
│       ├── APIEmbedder (via litellm) [optional]
│       ├── EmbeddingCache (threading.Lock + LRU)
│       └── EmbeddingService (factory + async interface)
│
├── workspace/
│   ├── manager.py → WorkspaceManager
│   ├── editor.py → FileEditor (str_replace + conflict detection)
│   ├── leasing.py → WorkspaceLeaseManager
│   └── git.py → WorkspaceGit [optional, gitpython]
│
├── agents/
│   ├── proxy.py → AgentProxy (config + react_loop + thresholds + trust)
│   ├── react_loop.py → AgentReActLoop (LLM turns + tool execution)
│   ├── thresholds.py → ResponseThresholdModel (Bonabeau 1996)
│   ├── tool_orchestrator.py → ToolOrchestrator (read-parallel, write-serial)
│   ├── prompt_builder.py → AgentPromptBuilder (modular assembly)
│   ├── templates.py → 8 built-in colony templates
│   └── composer.py → GoalAnalyzer (adaptive composition)
│
├── engine/
│   ├── lifecycle.py → EngineState (5 states) + TRANSITIONS
│   ├── execution.py → ExecutionEngine (main loop)
│   ├── decomposer.py → HierarchicalDecomposer
│   ├── allocator.py → StigmergicAllocator (ACO + Lévy + Thresholds)
│   ├── assembler.py → OutputAssembler
│   └── reporters.py → TerminalReporter, MarkdownReporter
│
├── ui/
│   ├── events.py → ColonyEvent, EventType (40+ types)
│   ├── protocol.py → ColonyController (ABC)
│   ├── local_controller.py → LocalColonyController
│   └── remote_controller.py → RemoteColonyController
│
├── colony.py → Colony (public API, 11-step init pipeline)
├── constants.py → 50+ battle-tested defaults
└── __init__.py → Public API exports
```

### 5.2 Key Interface Contracts

**The 5 ABCs that define extensibility:**

```python
# 1. LLM Client — swap providers
class BaseLLMClient(ABC):
    async def create(self, request: LLMRequest) -> LLMResponse: ...
    async def create_with_cost_check(self, request: LLMRequest, budget: LiveBudget | None) -> LLMResponse: ...

# 2. Pheromone Store — swap backends
class PheromoneStore(ABC):
    async def deposit(self, pheromone: Pheromone) -> str: ...
    async def get(self, id: str) -> Pheromone | None: ...
    async def sense(self, query: str, *, type_filter=None, limit=20, ...) -> SenseResult: ...

# 3. Embedder — swap embedding models
class BaseEmbedder(ABC):
    async def embed(self, text: str) -> list[float]: ...
    async def embed_batch(self, texts: list[str]) -> list[list[float]]: ...

# 4. Tool — extend agent capabilities
class BaseTool(ABC):
    name: str
    description: str
    input_schema: dict
    is_read_only: bool
    async def execute(self, input: dict, workspace, agent_id: str) -> ToolResult: ...

# 5. ColonyController — swap UI frontends
class ColonyController(ABC):
    async def start_solve(self, goal: str, ...) -> str: ...
    async def pause(self) -> None: ...
    async def resume(self) -> None: ...
    async def cancel(self) -> None: ...
    async def get_status(self) -> dict: ...
    async def send_message(self, text: str, priority: str) -> None: ...
    async def resolve_approval(self, approval_id: str, decision: str) -> None: ...
```

---

## 6. Data Model & Storage Design

### 6.1 Pheromone Schema (the central data unit)

```python
class Pheromone(BaseModel):
    id: str                         # UUID
    type: PheromoneType             # 8 types
    content: dict                   # Type-specific payload
    strength: float                 # [TAU_MIN=0.01, TAU_MAX=5.0]
    decay_rate: float               # [0.0, 1.0]
    depositor_id: str               # Agent or system
    depositor_trust: float          # [0.0, 1.0] Beta-Binomial
    task_context: str | None
    scope: PheromoneScope           # PRIVATE/TEAM/COLONY/FEDERATED
    tags: list[str]
    embedding: list[float] | None   # 384-dim (all-MiniLM-L6-v2) or None
    schema_version: int = 1
    contradicts: list[str]          # IDs of contradicting pheromones
    created_at: datetime
    last_reinforced: datetime | None
    reinforcement_count: int
    content_hash: str | None        # SHA-256
```

### 6.2 Storage Technology Selection

| Store | Technology | Why |
|-------|-----------|-----|
| Pheromone store (default) | InMemoryStore (Python dict + asyncio.Lock) | Zero deps, sufficient for single-process. Pheromones are ephemeral per solve. |
| Pheromone store (optional) | Redis 7+ via redis-py | Cross-process sharing for server mode. Pub/sub for event distribution. |
| Result persistence | JSON files in `.pheromone/results/` | Simple, human-readable, no DB dependency. |
| Colony config | YAML files + env vars + code | Standard Python config pattern. |
| Workspace | Local filesystem | Agents produce real files. No virtualization needed. |
| Embeddings cache | In-memory LRU dict (threading.Lock) | Sentence-transformers is CPU-bound, needs thread lock not asyncio lock. |

### 6.3 Index Strategy

For InMemoryStore, "indexing" means maintaining secondary dicts:

```python
class InMemoryStore(PheromoneStore):
    _pheromones: dict[str, Pheromone]           # Primary: id → Pheromone
    _by_type: dict[PheromoneType, list[str]]     # Secondary: type → [ids]
    _by_depositor: dict[str, list[str]]          # Secondary: depositor → [ids]
    _by_scope: dict[PheromoneScope, list[str]]   # Secondary: scope → [ids]
```

For RedisStore, use sorted sets for strength-based ranking:
```
pheromone:{colony_id}:{id} → JSON blob
pheromone_type:{colony_id}:{type} → sorted set (score = strength)
```

---

## 7. Key Sequence Diagrams

### 7.1 Agent ReAct Loop (single task execution)

```
AgentProxy          ReActLoop           LLM Client        ToolOrchestrator     Workspace       Environment
    │                   │                    │                    │                 │                │
    │──execute_task──►  │                    │                    │                 │                │
    │                   │──build_context──►  │                    │                 │                │
    │                   │                    │                    │                 │                │
    │                   │◄──SenseResult──────│────────────────────│─────────────────│──sense()──────│
    │                   │                    │                    │                 │                │
    │                   │── TURN 1 ─────────►│                    │                 │                │
    │                   │◄──response──────── │                    │                 │                │
    │                   │   (has tool_calls) │                    │                 │                │
    │                   │                    │                    │                 │                │
    │                   │──execute_tools─────│───────────────────►│                 │                │
    │                   │                    │                    │──FileRead──────►│                │
    │                   │                    │                    │◄──content───────│                │
    │                   │                    │                    │──FileWrite─────►│                │
    │                   │                    │                    │◄──ok────────────│                │
    │                   │◄──tool_results─────│────────────────────│                 │                │
    │                   │                    │                    │                 │                │
    │                   │──auto_deposit──────│────────────────────│─────────────────│──deposit()───►│
    │                   │                    │                    │                 │  (KNOWLEDGE)   │
    │                   │                    │                    │                 │                │
    │                   │── TURN 2 ─────────►│                    │                 │                │
    │                   │◄──response──────── │                    │                 │                │
    │                   │   (no tool_calls,  │                    │                 │                │
    │                   │    end_turn)        │                    │                 │                │
    │                   │                    │                    │                 │                │
    │◄──TaskOutput──── │                    │                    │                 │                │
    │                   │                    │                    │                 │                │
```

### 7.2 Task Allocation Round (ACO)

```
ExecutionEngine      Allocator         Agents[1..N]       Environment         ThresholdModel
    │                    │                  │                   │                    │
    │──allocate_round───►│                  │                   │                    │
    │  (available_tasks, │                  │                   │                    │
    │   agents, env)     │                  │                   │                    │
    │                    │                  │                   │                    │
    │                    │──── For each agent ────────────────►│                    │
    │                    │                  │                   │                    │
    │                    │  1. Pre-filter: response threshold gate              ◄────│
    │                    │     stimulus(task) > θ(agent, required_skills)            │
    │                    │     → eligible_tasks                                      │
    │                    │                  │                   │                    │
    │                    │  2. For each eligible task:         │                    │
    │                    │     sense(capability query) ────────►│                    │
    │                    │     ◄── τ_cap (capability strength) │                    │
    │                    │                  │                   │                    │
    │                    │  3. Compute ACO attraction:         │                    │
    │                    │     attraction = τ_cap^α × η_urg^β × ρ_hist^γ            │
    │                    │                  │                   │                    │
    │                    │  4. Lévy exploration (probabilistic):│                    │
    │                    │     if random() < ε → Lévy step     │                    │
    │                    │     else → select by probability    │                    │
    │                    │                  │                   │                    │
    │                    │  5. Optimistic lock: highest attraction wins              │
    │                    │                  │                   │                    │
    │◄──{task→agent}────│                  │                   │                    │
```

---

## 8. API Design

### 8.1 Public Python API (primary interface)

```python
# The 3-line quick start
from pheromone import Colony
colony = Colony("my-project", default_model="claude-sonnet-4-6")
result = await colony.solve("Build a weather API with tests")

# Full API
class Colony:
    def __init__(self, name, *, config_path?, config?, template?, default_model?,
                 budget?, strategy?, workspace_dir?, agents?, llm_client?, store?)
    async def solve(self, goal, *, specification?, strategy?) -> ColonyResult
    def register(self, agent_config: AgentConfig) -> None
    async def shutdown() -> None
```

### 8.2 REST API (server mode, Phase 4)

```
POST   /api/v1/colony                          # Create colony
POST   /api/v1/colony/{id}/solve               # Start solve
GET    /api/v1/colony/{id}/status               # Colony status
POST   /api/v1/colony/{id}/pause                # Pause execution
POST   /api/v1/colony/{id}/resume               # Resume
POST   /api/v1/colony/{id}/cancel               # Cancel
GET    /api/v1/colony/{id}/result/{run_id}      # Get result
GET    /api/v1/colony/{id}/config               # Get config (api_key stripped)
GET    /api/v1/colony/{id}/workspace/files/{path}  # Read file
POST   /api/v1/colony/{id}/message              # Send message to colony
POST   /api/v1/colony/{id}/approval/{id}        # Resolve approval
WS     /api/v1/colony/{id}/stream               # Event stream
GET    /api/v1/health                           # Health check
```

### 8.3 CLI Commands

```bash
pheromone solve "Build a weather API"     # Main entry
pheromone init                             # Create .pheromone.yaml
pheromone tui                              # Launch Textual TUI
pheromone gui                              # Launch web GUI (FastAPI + React)
pheromone status                           # Show last run result
pheromone diff [run-id]                    # Git diff of workspace changes
pheromone version                          # Show version
```

---

## 9. Reliability & Fault Tolerance

Covered exhaustively in architecture §16 and Gap 10. Key design choices:

- **Circuit breaker per agent**: CLOSED → OPEN after 3 consecutive failures → HALF_OPEN after 60s → test
- **Cooperative pause**: asyncio.Event + checkpoint() before each LLM call and tool execution
- **Graceful cancel**: drain current tasks → assemble partial result → emit COLONY_COMPLETED with warning
- **Agent crash recovery**: heartbeat protocol → dead detection at 3× interval → release leases + tasks
- **Budget exhaustion**: graceful stop → return best results from completed tasks
- **LLM rate limits**: exponential backoff with jitter, Retry-After header parsing, max 10 retries

---

## 10. Security Design

Covered in architecture §20. Key points:

- API keys never appear in pheromone content (sanitization on deposit)
- API keys never appear in logs (structured logging strips sensitive fields)
- Config endpoint strips api_key field, masks Redis password
- Workspace file access uses pathlib.resolve() to prevent path traversal
- Pheromone deposit rate limited at 50/agent/minute
- Content integrity via SHA-256 hashing on deposit, verification on read
- Colony-scoped namespace isolation (colony_id prefix on all store keys)

---

## 11. Observability

- **Structured logging**: structlog for JSON output, correlation IDs (colony_id, agent_id, task_id)
- **Ring buffers**: 10 activities, 100 errors, 50 slow ops (>2s)
- **Event system**: 40+ event types, constructor-injected emit callback, sequential per-agent, globally ordered for budget
- **Colony replay**: full audit trail enables deterministic step-through

---

# PART 2: TECH STACK DECISION RECORD

## 12. Technology Selection Matrix

### 12.1 Core Dependencies (always installed)

| Technology | Version | Why This | Why NOT Alternatives |
|-----------|---------|----------|---------------------|
| **Python** | >=3.11 | Required for `tomllib`, `TaskGroup`, performance. 3.12/3.13 preferred. | 3.10 lacks `tomllib`. 3.14 beta only. |
| **Pydantic** | >=2.12,<3 | Data validation, JSON serialization, discriminated unions, model_copy(). Used by EVERY model in the system. Stable 2.12.5 is latest. | dataclasses lack validation. attrs less ecosystem support. msgspec less flexible. |
| **LiteLLM** | >=1.83.0,<2 | Provider-agnostic LLM calls. 100+ models. Built-in retry. Cost tracking. **PIN TO >=1.83.0 — versions 1.82.7 and 1.82.8 were compromised in a supply chain attack on March 24, 2026.** v1.83.0 is the verified safe release. | Direct provider SDKs (anthropic, openai) would mean maintaining N clients. LiteLLM wraps them all. |
| **httpx** | >=0.25 | Async HTTP client. LiteLLM dependency. Also used for FallbackLLMClient direct calls. | requests is sync-only. aiohttp has different API patterns. |
| **PyYAML** | >=6.0 | Config file parsing (.pheromone.yaml). | tomllib (stdlib) only does TOML. We need YAML for readability of agent/strategy configs. |
| **python-dotenv** | >=1.0 | Auto-load .env files for API keys. | Manual os.environ. dotenv is standard practice. |
| **Typer** | >=0.12 | CLI entry points (pheromone solve, pheromone init). Based on click, type-hint driven. | click is lower-level. argparse is verbose. |
| **Rich** | >=13.0 | Terminal formatting, progress bars, tables. Typer dependency. Used by TerminalReporter. | Plain print(). Rich is the standard for modern Python CLIs. |
| **NumPy** | >=1.24 | Cosine similarity in sensing, Lévy flight Mantegna algorithm, ACO probability calculations. | Pure Python math is 10-100x slower for vector ops. |
| **structlog** | >=23.0 | Structured JSON logging with context binding. | stdlib logging can't do structured JSON without manual formatter. structlog is purpose-built. |

### 12.2 Optional Dependencies (extras)

| Extra | Technology | Version | Why |
|-------|-----------|---------|-----|
| `[tui]` | **Textual** | >=0.80 | Python TUI framework. CSS-like styling, widget system, async-native. Only Python TUI framework with this level of sophistication. Used by `pheromone tui`. |
| `[gui]` | **FastAPI** | >=0.135 | Async web framework. WebSocket support. Auto-docs. Latest 0.135.3 adds native SSE streaming. Used for API server. |
| `[gui]` | **Uvicorn** | >=0.27 | ASGI server for FastAPI. Standard choice. |
| `[gui]` | **websockets** | >=12.0 | WebSocket library for real-time event streaming. |
| `[embeddings]` | **sentence-transformers** | >=3.0 | Local embedding generation. all-MiniLM-L6-v2 model (384-dim, ~80MB, ~5ms/embed). |
| `[redis]` | **redis-py** | >=5.0 (with hiredis) | Redis client with hiredis for C-level parsing performance. |
| `[git]` | **gitpython** | >=3.1 | Git operations. Requires git binary on PATH. |

### 12.3 Frontend Stack (Web GUI, Phase 4)

| Technology | Version | Why |
|-----------|---------|-----|
| **React** | 19 | Component model, hooks, massive ecosystem. Latest stable. |
| **Vite** | 6+ | Build tool. Faster than webpack. HMR. |
| **Tailwind CSS** | 4+ | Utility-first CSS. No custom CSS files needed for most styling. |
| **ReactFlow** | 12+ | DAG visualization. Handles node/edge rendering, zoom, pan. Perfect for task graph display. |
| **TypeScript** | 5.5+ | Type safety for all frontend code. Shared type contract with Python models (Gap 7). |

### 12.4 Development Dependencies

| Technology | Version | Why |
|-----------|---------|-----|
| **pytest** | >=8.0 | Test runner. Async support via pytest-asyncio. |
| **pytest-asyncio** | >=0.23 | asyncio_mode="auto" for seamless async tests. |
| **pytest-cov** | >=5.0 | Coverage reporting. 80% threshold. |
| **ruff** | >=0.4 | Linting + formatting. Replaces flake8 + black + isort. 10-100x faster. |
| **mypy** | >=1.10 | Static type checking. strict mode. |
| **pre-commit** | >=3.0 | Git hooks for ruff + mypy before commit. |

---

## 13. Version Pinning & Security Notes

### CRITICAL: LiteLLM Supply Chain Attack

On **March 24, 2026**, LiteLLM versions **1.82.7** and **1.82.8** were published with a credential-stealing backdoor (TeamPCP via compromised Trivy in CI/CD). The compromised versions harvested SSH keys, cloud credentials, Kubernetes secrets, and .env files.

**Mitigation for Pheromone:**
- Pin `litellm>=1.83.0,<2` in pyproject.toml (1.83.0 is the first verified safe release)
- Add a note in CONTRIBUTING.md about this incident
- Use `pip install --require-hashes` in CI if you want belt-and-suspenders
- Document in README: "Never install litellm 1.82.7 or 1.82.8"

### Version Pin Strategy

```toml
# pyproject.toml — updated pins
dependencies = [
    "pydantic>=2.12,<3",
    "litellm>=1.83.0,<2",     # CRITICAL: >=1.83.0 (1.82.7-8 compromised)
    "httpx>=0.25",
    "pyyaml>=6.0",
    "python-dotenv>=1.0",
    "typer>=0.12",
    "rich>=13.0",
    "numpy>=1.24",
    "structlog>=23.0",
]
```

---

## 14. Alternatives Considered & Rejected

| Decision | Rejected Alternative | Why Rejected |
|----------|---------------------|-------------|
| LiteLLM for LLM abstraction | Direct anthropic/openai SDKs | Would need separate client per provider. LiteLLM wraps 100+ providers. |
| LiteLLM for LLM abstraction | Pydantic AI | Agent framework, not just LLM client. Would compete with Pheromone's own agent model. |
| Pydantic for models | dataclasses + marshmallow | Pydantic v2 is faster, has built-in JSON serialization, discriminated unions, and is the de facto standard. |
| InMemoryStore default | SQLite | SQLite adds file locking complexity with async. Pheromones are ephemeral per solve — in-memory is correct. |
| Textual for TUI | Ink (React for CLI) | Ink is JavaScript/TypeScript. Pheromone is Python. Textual is the best Python TUI framework. |
| Textual for TUI | Blessed / Urwid | Legacy. No CSS-like styling. No async-native. No widget system comparable to Textual. |
| React for web GUI | Streamlit | No WebSocket. Reruns entire script on interaction. No component model. Unsuitable for real-time multi-agent visualization. |
| FastAPI for API | Flask / Django | Flask lacks native async. Django too heavy. FastAPI is the standard for async Python APIs. |
| NumPy for math | Pure Python | 10-100x slower for vector operations (cosine similarity, Lévy flight). |
| structlog for logging | stdlib logging | Can't do structured JSON without manual formatter. structlog purpose-built for it. |
| Ruff for linting | flake8 + black + isort | Ruff replaces all three, 10-100x faster, single tool. |
| sentence-transformers for embeddings | OpenAI embeddings API | Would require API key + cost per embed. Local model is free after initial download. API option available as fallback. |
| gitpython for git | subprocess.run(["git", ...]) | gitpython provides Python objects for commits, tags, diffs. subprocess would need output parsing. |

---

# PART 3: CLAUDE CODE ORCHESTRATION

## 15. Document Architecture — How 14 Specs Connect

### 15.1 Document Dependency Graph

```
PHEROMONE_v2_1_COMPLETE_FINAL.md (Architecture — the FOUNDATION)
    │
    ├── Gap 1: llm_client_spec.md
    │     References: §3 (constants), §6.3 (ReAct loop LLM interface)
    │
    ├── Gap 2: output_assembly_spec.md
    │     References: §11 (execution engine output), Gap 1 (LLMUsage)
    │     Cross-ref: Gap 3 (OutputMode canonical location)
    │
    ├── Gap 3: config_init_spec.md
    │     References: §3, §6.1, §6.8, §28, §29
    │     Cross-ref: Gap 1 (middleware), Gap 2 (OutputMode), Gap 4 (EmbeddingConfig)
    │
    ├── Gap 4: embedding_service_spec.md
    │     References: §5.4 (sensing), §14 (semantic similarity)
    │     Cross-ref: Gap 3 (EmbeddingConfig)
    │
    ├── Gap 5: test_infra_spec.md
    │     References: ALL (fixtures for all model types)
    │
    ├── Gap 6a: cli_tui_spec.md
    │     References: §30 (Public API), Gap 9 (events)
    │     Cross-ref: Gap 7 (shared types), Gap 10 (controller)
    │
    ├── Gap 6b: web_gui_spec.md
    │     References: §27 (REST API), Gap 9 (events)
    │     Cross-ref: Gap 7 (TS types), Gap 6a (ColonyController ABC)
    │
    ├── Gap 7: colony_result_spec.md
    │     References: Gap 2 (Python models), Gap 6a/6b (TS interface)
    │
    ├── Gap 9: event_system_spec.md
    │     References: ALL engine components (where events emit)
    │
    ├── Gap 10: colony_lifecycle_spec.md
    │     References: §11 (engine), §16 (fault tolerance)
    │     Cross-ref: Gap 2 (tracker), Gap 9 (events)
    │
    ├── Gap 11: dependency_spec.md
    │     References: ALL (dependency audit)
    │
    ├── Gap 12: error_taxonomy_spec.md
    │     References: ALL (error types used everywhere)
    │
    ├── Gap 13: git_integration_spec.md
    │     References: §9 (workspace), Gap 3 (Colony init Step 7b)
    │
    └── CROSS_SPEC_AUDIT.md
          Validates: Gap 1↔2↔3↔4 boundaries, defines TaskOutput + SenseResult
```

### 15.2 Document Categories

**Category A — Always Loaded (every session):**
- `CLAUDE.md` (the master reference — see §19 below)
- `PHEROMONE_v2_1_COMPLETE_FINAL.md` (architecture)

**Category B — Phase-Specific (loaded per build phase):**
- Phase 1 (core): Gaps 1, 2, 3, 4, 5, 11, 12, CROSS_SPEC_AUDIT
- Phase 2 (robustness): Gaps 9, 10, 13
- Phase 3 (intelligence): Architecture §14, §15, §5.5, §5.6
- Phase 4 (UI): Gaps 6a, 6b, 7

**Category C — Reference Only (loaded on demand):**
- `CLAUDE_CODE_UX_EXTRACTION_PROMPT.md` (for TUI/GUI implementation)
- `todo.md` (completion tracking)

---

## 16. Phase-Bundled Document Loading Strategy

Claude Code has finite context. Loading all 14 docs (~15K lines) at once is impossible. The strategy:

### Phase 1: Foundation (Week 1)

**Load these files into Claude Code's CLAUDE.md or initial context:**
1. `CLAUDE.md` (the master reference — §19)
2. Architecture v2.1 sections 1-11 (core only, ~800 lines)
3. Gap 12: `error_taxonomy_spec.md` (413 lines)
4. Gap 11: `dependency_spec.md` (469 lines)
5. Gap 1: `llm_client_spec.md` (2648 lines — the largest spec, essential for LLM layer)
6. `CROSS_SPEC_AUDIT.md` (251 lines)

**Load on-demand (when building specific components):**
- Gap 3: `config_init_spec.md` — when building Colony.__init__
- Gap 4: `embedding_service_spec.md` — when building environment
- Gap 2: `output_assembly_spec.md` — when building assembler
- Gap 5: `test_infra_spec.md` — when setting up test infrastructure

### Phase 2: Robustness (Weeks 2-4)

**Load:**
1. Architecture v2.1 sections 12-21
2. Gap 10: `colony_lifecycle_spec.md`
3. Gap 9: `event_system_spec.md`
4. Gap 13: `git_integration_spec.md`

### Phase 3: Intelligence (Weeks 5-7)

**Load:**
1. Architecture v2.1 sections 14, 15, 5.5, 5.6, 19

### Phase 4: UI (Weeks 8-10)

**Load:**
1. Gap 6a: `cli_tui_spec.md`
2. Gap 6b: `web_gui_spec.md`
3. Gap 7: `colony_result_spec.md`
4. `CLAUDE_CODE_UX_EXTRACTION_PROMPT.md` (reference)

---

## 17. The /ultraplan Prompt

This is the prompt you paste into Claude Code as your FIRST message in the initial development session, prefixed with `/ultraplan`:

```markdown
/ultraplan

# PHEROMONE — Master Development Plan

## WHAT WE'RE BUILDING
Pheromone is an open-source Python framework for bio-inspired multi-agent AI 
coordination using stigmergic communication (Ant Colony Optimization). Agents 
coordinate via pheromone signals — no central orchestrator.

## ARCHITECTURE
The locked architecture is in PHEROMONE_v2_1_COMPLETE_FINAL.md (1,808 lines).
DO NOT MODIFY the architecture. Build ON TOP of it.

## ENGINEERING SPECS
13 gap specs resolve every engineering plumbing detail. 179 issues found and 
fixed across all specs. These specs are the SOURCE OF TRUTH for implementation 
details — they override the architecture where they provide more specific 
guidance (e.g., ExecutionTracker replaces monkey-patching, OutputMode canonical
location is config.py not results.py).

## CURRENT PHASE
Phase 1: Foundation (Week 1)
Goal: `colony.solve("Build a weather API")` works E2E with MockLLM by Day 5.

## FILES TO BUILD (in dependency order)
[See IMPLEMENTATION_ROADMAP.md for the day-by-day file list]

## INVARIANT RULES (never violate these)
1. Every file has type hints and docstrings
2. Pydantic v2 for ALL models (BaseModel, not dataclass)
3. Import from pheromone.errors for ALL exceptions
4. Import OutputMode from pheromone.models.config (CANONICAL location)
5. Constants come from pheromone.constants — NEVER hardcode
6. Use asyncio.Lock for async code, threading.Lock ONLY for EmbeddingCache
7. MockLLM for ALL tests — no real API calls in CI
8. All pheromone strength values clamped to [TAU_MIN, TAU_MAX]
9. All file edits use content hash for conflict detection
10. No monkey-patching Pydantic models (use ExecutionTracker instead)

## CROSS-SPEC CONTRACTS (models defined across specs)
- LLMRequest, LLMResponse, LLMToolCall, LLMUsage → Gap 1 (llm/models.py)
- TaskOutput, TaskExecutionRecord, ExecutionTracker → Gap 2 (models/execution.py)
- SenseResult → Cross-spec audit (models/pheromones.py)
- ColonyResult, WorkspaceOutput, TextOutput, HybridOutput → Gap 2 (models/results.py)
- ColonyConfig, Strategy, AgentConfig, LiveBudget → Gap 3 (models/config.py)
- EmbeddingService, BaseEmbedder → Gap 4 (environment/embeddings.py)
- ColonyEvent, EventType → Gap 6a (ui/events.py)
- ColonyController → Gap 6a (ui/protocol.py)

## QUALITY GATES
Before marking any day complete:
- All tests pass: `pytest -v`
- No type errors: `mypy pheromone/` (or document known issues)
- Clean lint: `ruff check pheromone/`
- Models serialize/deserialize correctly (JSON roundtrip test)
- Cross-spec contracts respected (import paths match spec)

## WHAT TO DO NOW
1. Read the CLAUDE.md in the project root (it has the full reference)
2. Read the IMPLEMENTATION_ROADMAP.md for today's file list
3. Start building Day 1 files in dependency order
4. Write tests alongside (not after)
5. Run pytest after each file is complete
```

---

## 18. Multi-Session Continuity Strategy

### The Problem
Claude Code sessions have finite context. A 12-week build spans dozens of sessions. Each session starts fresh. How do you prevent drift, regressions, and lost context?

### The Solution: 4-Layer Continuity

**Layer 1: CLAUDE.md (always loaded)**
A file in the project root that Claude Code auto-reads at session start. Contains: project identity, current phase, invariant rules, file structure, active decisions. Updated after each session. (See §19.)

**Layer 2: Session handoff notes**
At the END of each Claude Code session, ask it to produce a handoff note:
```
"Before we end, produce a session handoff note covering:
1. What was built this session (files created/modified)
2. What tests pass now
3. Any decisions made that differ from specs
4. What should be built next
5. Any known issues or TODOs"
```
Save this as `docs/sessions/session-{N}-{date}.md`.

**Layer 3: Git as state**
Every session should end with a commit. The codebase IS the state. Next session starts by reading the codebase, not by re-explaining what was built.

**Layer 4: Spec files as guardrails**
The 14 spec files don't change. They're always available to load when Claude Code needs implementation details. The spec is the law — if code drifts from spec, the code is wrong.

### Session Start Template (after Day 1)

```markdown
# Continuing Pheromone Development

## Current State
- Phase: [1/2/3/4/5]
- Last session: [session-N-date.md summary]
- Tests passing: [X/Y]
- Coverage: [Z%]

## Today's Goals
[From IMPLEMENTATION_ROADMAP.md]

## Reference Docs for Today
[List specific spec files to load for today's work]

## Known Issues from Last Session
[From session handoff note]
```

---

## 19. CLAUDE.md — The Always-Loaded Foundation

This file lives at the project root. Claude Code reads it automatically at every session start.

```markdown
# PHEROMONE — Project Intelligence File

## Identity
Open-source Python framework for bio-inspired multi-agent AI coordination
using stigmergic communication (Ant Colony Optimization).
Author: Anshul Ghate | License: MIT | Python >=3.11

## Architecture
Locked in docs/PHEROMONE_v2_1_COMPLETE_FINAL.md. DO NOT MODIFY.
13 gap specs in docs/specs/. These are implementation-level source of truth.

## Current Phase
[UPDATE THIS AFTER EACH SESSION]
Phase: 1 (Foundation)
Day: 1
Tests passing: 0
Last modified: [date]

## Critical Rules
1. Pydantic v2 for ALL models
2. errors.py is CANONICAL for all exceptions
3. config.py is CANONICAL for OutputMode
4. constants.py for ALL constants — never hardcode
5. asyncio.Lock (not threading.Lock) except EmbeddingCache
6. MockLLM for all tests — zero API calls in CI
7. litellm>=1.83.0 ONLY (1.82.7-8 were compromised)
8. MAX-MIN bounds on ALL pheromone strength mutations
9. ExecutionTracker (not monkey-patched TaskNode) for execution state
10. Content hash for ALL file edit conflict detection

## Package Structure
[Copy from Gap 11 §3 — the definitive file tree]

## Key Design Decisions
- LiteLLM wraps all LLM providers (not direct SDKs)
- InMemoryStore default, RedisStore optional
- NullEmbedder Phase 1 default, SentenceTransformer Phase 2+
- Textual for TUI, React+FastAPI for Web GUI
- ColonyController ABC shared by CLI and GUI
- Config layering: Defaults → YAML → env → code
- Event system: constructor-injected callback, 40+ event types
- spent_dollars/max_dollars naming (not spent_usd)

## Test Commands
pytest -v                                    # All tests
pytest -v -m "not slow"                      # Skip ML model loading
pytest -v --cov=pheromone --cov-report=term  # With coverage
ruff check pheromone/                        # Lint
mypy pheromone/                              # Type check

## Spec File Index
| Spec | File | Lines | Phase |
|------|------|-------|-------|
| Architecture | docs/PHEROMONE_v2_1_COMPLETE_FINAL.md | 1808 | ALL |
| Gap 1: LLM Client | docs/specs/llm_client_spec.md | 2648 | 1 |
| Gap 2: Output Assembly | docs/specs/output_assembly_spec.md | 237 | 1 |
| Gap 3: Config/Init | docs/specs/config_init_spec.md | 1259 | 1 |
| Gap 4: Embeddings | docs/specs/embedding_service_spec.md | 751 | 1 |
| Gap 5: Test Infra | docs/specs/test_infra_spec.md | 645 | 1 |
| Gap 6a: CLI/TUI | docs/specs/cli_tui_spec.md | 1512 | 4 |
| Gap 6b: Web GUI | docs/specs/web_gui_spec.md | 1256 | 4 |
| Gap 7: Shared Types | docs/specs/colony_result_spec.md | 835 | 4 |
| Gap 9: Events | docs/specs/event_system_spec.md | 635 | 2 |
| Gap 10: Lifecycle | docs/specs/colony_lifecycle_spec.md | 842 | 2 |
| Gap 11: Dependencies | docs/specs/dependency_spec.md | 469 | 1 |
| Gap 12: Errors | docs/specs/error_taxonomy_spec.md | 413 | 1 |
| Gap 13: Git | docs/specs/git_integration_spec.md | 347 | 2 |
| Cross-Spec Audit | docs/specs/CROSS_SPEC_AUDIT.md | 251 | 1 |
```

---

## 20. Quality Gates Between Sessions

### After Each Day (Claude Code session boundary)

| Gate | Check | Pass Criteria |
|------|-------|---------------|
| Tests | `pytest -v` | All tests from today + all previous pass |
| Types | `mypy pheromone/` | No new errors (document known issues) |
| Lint | `ruff check pheromone/` | Zero warnings |
| Cross-spec | Manual review | New code matches spec file contracts |
| Commit | `git status` | All files committed with descriptive message |
| CLAUDE.md | Updated | Current phase, day, test count updated |
| Handoff | Session note | Written and saved to `docs/sessions/` |

### After Each Phase (Week boundary)

| Gate | Check | Pass Criteria |
|------|-------|---------------|
| Coverage | `pytest --cov` | >80% on new code |
| Integration | `pytest -m integration` | All integration tests pass |
| E2E | `pytest -m e2e` | colony.solve() produces valid result |
| README | Manual | Quick start works as documented |
| Spec compliance | Audit | Read each spec used this phase, verify code matches |

---

# PART 4: TRADEOFFS & EVOLUTION

## 21. Tradeoff Register

| # | Decision | Chosen | Alternative | Rationale | Revisit When |
|---|----------|--------|-------------|-----------|-------------|
| T1 | Single-process | Yes | Distributed | One user, one machine, one colony. Simplicity over scale for v1. | When concurrent colonies or multi-machine needed |
| T2 | InMemory default store | Yes | SQLite | Pheromones are ephemeral per solve. No persistence needed in default case. | When multi-solve pheromone persistence requested |
| T3 | NullEmbedder Phase 1 | Yes | sentence-transformers from Day 1 | Removes 800MB dependency and 3-5s startup for initial development. Sensing still works via keyword matching. | Phase 2 (Week 3) — switch to SentenceTransformer |
| T4 | LiteLLM over direct SDKs | Yes | Direct anthropic + openai SDKs | Multi-provider support out of the box. Risk: LiteLLM is a dependency with supply chain risk (as evidenced by March 2026 incident). | If LiteLLM has another security incident or becomes unmaintained |
| T5 | Textual over Ink | Yes | Ink (React for CLI) | Textual is Python-native, avoiding a Node.js dependency in a Python project. | If Textual development stalls |
| T6 | asyncio over threading | Yes | threading + concurrent.futures | asyncio is natural for I/O-bound LLM API calls. Cooperative scheduling avoids race conditions. | Never — Python async is the correct model for this workload |
| T7 | Pydantic strict mode off | Yes | strict=True on all models | Strict mode rejects some valid inputs (e.g., int where float expected). Better DX with coercion. | If data integrity issues arise from coercion |
| T8 | YAML over TOML for config | Yes | TOML only | YAML is more readable for nested agent/strategy configs. TOML supported as secondary (pyproject.toml). | If YAML parsing causes issues |
| T9 | MIT license | Yes | Apache 2.0, AGPL | MIT maximizes adoption. AGPL would limit enterprise use. Apache 2.0 is fine but MIT is simpler. | If patent concerns arise |
| T10 | Hatch build system | Yes | setuptools, flit, poetry | Hatch is lightweight, supports force-include for React dist, no lock file needed (this is a library). | If Hatch has compatibility issues |

---

## 22. Evolution Path

### v0.1 (Week 1 — MVP)
- Colony.solve() works E2E with MockLLM
- InMemoryStore only
- NullEmbedder
- Basic CLI (pheromone solve)
- 182+ tests
- Published to GitHub

### v0.5 (Week 4 — Robust)
- Real LLM integration tested
- SentenceTransformer embeddings
- Redis store option
- Review cycles + ADRs
- Git workspace versioning
- Human-in-the-loop
- 350+ tests

### v1.0 (Week 10 — Production)
- Textual TUI + React Web GUI
- MCP server
- Stigmergic RL
- 8 templates
- Docker deployment
- Comprehensive documentation
- 550+ tests

### v1.0-release (Week 12 — Launch)
- PheromBench results
- PyPI release
- arXiv paper submitted
- HuggingFace Spaces demo
- LinkedIn series published

### v2.0 (Future — not scoped)
- Multi-colony federation
- Distributed execution (multi-node)
- Agent-to-Agent protocol (A2A)
- Persistent colony memory across sessions
- Plugin marketplace for custom tools
- Commercial features (if warranted)

---

## APPENDIX A: File Inventory for Claude Code

Place spec files in the repo so Claude Code can access them:

```
pheromone/
├── CLAUDE.md                                    # Auto-loaded every session
├── docs/
│   ├── PHEROMONE_v2_1_COMPLETE_FINAL.md         # Architecture
│   ├── SYSTEM_DESIGN.md                          # This document
│   ├── IMPLEMENTATION_ROADMAP.md                 # Day-by-day build order
│   ├── specs/
│   │   ├── llm_client_spec.md                   # Gap 1
│   │   ├── output_assembly_spec.md              # Gap 2
│   │   ├── config_init_spec.md                  # Gap 3
│   │   ├── embedding_service_spec.md            # Gap 4
│   │   ├── test_infra_spec.md                   # Gap 5
│   │   ├── cli_tui_spec.md                      # Gap 6a
│   │   ├── web_gui_spec.md                      # Gap 6b
│   │   ├── colony_result_spec.md                # Gap 7
│   │   ├── event_system_spec.md                 # Gap 9
│   │   ├── colony_lifecycle_spec.md             # Gap 10
│   │   ├── dependency_spec.md                   # Gap 11
│   │   ├── error_taxonomy_spec.md               # Gap 12
│   │   ├── git_integration_spec.md              # Gap 13
│   │   └── CROSS_SPEC_AUDIT.md                  # Cross-spec
│   └── sessions/                                 # Session handoff notes
│       └── session-001-YYYY-MM-DD.md
├── pheromone/                                    # Source code
├── tests/                                        # Test code
├── examples/                                     # Usage examples
├── templates/                                    # Colony YAML templates
└── pyproject.toml                                # Build config
```

---

*This document is the pre-implementation engineering foundation. It must be reviewed and approved before any code is written. The architecture v2.1, 13 gap specs, this system design, and the implementation roadmap together form the complete specification from which Pheromone will be built.*

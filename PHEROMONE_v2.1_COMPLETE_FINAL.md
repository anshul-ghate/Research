# PHEROMONE v2.1 — Complete & Final Architecture
## Bio-Inspired Collective Intelligence for AI Agents
### Merged with Claude Code Intelligence Integration

**Author:** Anshul Ghate
**Version:** 2.1 FINAL (Merged) | **Date:** April 7, 2026
**Status:** LOCKED — Single Source of Truth. No code written that isn't specified here.
**Inputs:** v2.0 architecture + gap analysis + 5 theoretical additions + 5 enterprise-complexity additions + Claude Code codebase analysis (3,059 lines) + pre-implementation refinement

---

## CHANGELOG: v2 → v2.1 (Merged)

| Change | Category | Impact |
|--------|----------|--------|
| +Response Threshold Model (Bonabeau 1996) | Theoretical | Emergent agent specialization |
| +Quorum Sensing | Theoretical | Collective decision validation |
| +Lévy Flight Exploration (Viswanathan 1999) | Theoretical | Replaces ε-greedy entirely |
| +Information Foraging Theory (Pirolli & Card 1999) | Theoretical | Formalized sensing system |
| +Stigmergic Reinforcement Learning | Novel research | Colony self-optimizes parameters |
| +Adaptive Colony Composition (3 modes) | Architecture | Colony self-assembles agent teams |
| +Hierarchical Task Decomposition | Architecture | Multi-level Epic→Feature→Task trees |
| +Shared Workspace / Codebase Awareness | Architecture | Agents share code, not just text |
| +Iterative Refinement Cycles (Review Loops) | Architecture | Code→Test→Review→Fix cycles |
| +Architectural Decision Records (ADRs) | Architecture | Cross-cutting consistency enforcement |
| +Integration Verification Layer | Architecture | Components verified to work together |
| +Specification Tracking & Coverage | Architecture | PRD requirements traced to outputs |
| +Tool Pheromone Protocol | Infrastructure | Tool results shared via pheromones |
| +Checkpoint Pheromones | Infrastructure | Resumable long-running tasks |
| +Human-in-the-Loop (3-Way Permission) | Infrastructure | allow/ask/deny + classifier + denial tracking |
| +Multi-Colony Federation | Infrastructure | Cross-colony knowledge sharing |
| +Pheromone Scoping (Privacy) | Infrastructure | Private/team/colony/federated visibility |
| +Knowledge Conflict Resolution | Intelligence | Contradictory claims handled formally |
| +Schema Versioning | Infrastructure | Backward-compatible pheromone evolution |
| +Agent Internal ReAct Loop | Claude Code Intel | Multi-turn LLM execution per task |
| +Tool Orchestration (Read-Parallel/Write-Serial) | Claude Code Intel | Concurrency-safe tool execution |
| +9-Section Pheromone Compaction | Claude Code Intel | Structured summarization, not truncation |
| +str_replace Edit Algorithm + Conflict Detection | Claude Code Intel | Battle-tested file editing |
| +Agent Tool System (typed tool profiles) | Claude Code Intel | Per-agent-type tool restrictions |
| +Structured Prompt Engineering (modular assembly) | Claude Code Intel | Static+dynamic prompt boundary |
| +MCP-Compatible Protocol | Claude Code Intel | Ecosystem interoperability |
| +Codebase Index via Pheromones | Claude Code Intel | Auto-deposited file discovery knowledge |
| +CLAUDE.md Compatibility | Claude Code Intel | Read existing project configs |
| +Battle-Tested Constants (30+) | Claude Code Intel | Production-refined defaults |
| +PheromBench (New Benchmark Standard) | Research | 5-category multi-agent benchmark |

**Total: 26 gaps resolved. 16 theoretical concepts. 5 novel contributions. 14 Claude Code intelligence integrations. 0 known remaining gaps.**

---

## TABLE OF CONTENTS

### FOUNDATION
1. System identity & positioning
2. Complete theoretical inventory (16 concepts, 10 fields)
3. Constants reference (30+ battle-tested defaults)

### CORE ARCHITECTURE
4. Core data models
5. Pheromone environment (MAX-MIN, compaction, auto-indexing)
6. Agent model (ReAct loop, thresholds, tool profiles, prompt engineering)
7. Agent tool system
8. Hierarchical task decomposition + specification tracking
9. Shared workspace (str_replace, leasing, conventions)
10. Stigmergic task allocation (ACO + Lévy flights + tool orchestration)
11. Execution engine (with iterative refinement cycles)
12. Architectural Decision Records
13. Integration verification layer
14. Evolution engine (Stigmergic RL)
15. Quality control (Quorum Sensing + Bayesian Trust)

### INFRASTRUCTURE
16. Fault tolerance & resilience
17. Concurrency model
18. Cost management
19. Context window management (Information Foraging + dual token counting)
20. Security model
21. Observability (structured logging + ring buffers)
22. Tool integration
23. Long-running task support
24. Human-in-the-loop (3-way permission model)
25. Multi-colony federation
26. CLAUDE.md compatibility layer
27. Integration protocol specification (PPS + MCP)
28. Deployment architecture

### DELIVERY
29. Project structure
30. Public API reference
31. Benchmarking strategy (PheromBench + established benchmarks)
32. 12-week build roadmap (5 phases)
33. Research plan
34. Implementation risk register (26 risks)
35. Quality standards (per-component)
36. Gap coverage matrix

---

## 1. SYSTEM IDENTITY & POSITIONING

### What Pheromone IS
An open-source Python framework enabling groups of AI agents to coordinate, share knowledge, and solve complex problems through bio-inspired stigmergic communication — without any central orchestrator. Designed to handle real-world complexity: multi-file codebases, iterative review cycles, cross-cutting architectural decisions, and production-grade output quality.

### What Pheromone IS NOT
- Not an agent framework (doesn't replace LangGraph, CrewAI, OpenClaw)
- Not an LLM wrapper (doesn't compete with LiteLLM, OpenRouter)
- Not a workflow engine (doesn't replace Temporal, Prefect)

### Competitive Differentiation

| Feature | CrewAI | LangGraph | AutoGen | Claude Code | **Pheromone** |
|---------|--------|-----------|---------|-------------|---------------|
| Coordination | Hierarchical | Graph/FSM | Conversation | Subagent spawn | **Stigmergic (ACO)** |
| Knowledge sharing | Shared dict | State in graph | Chat history | CLAUDE.md + context | **Pheromone env (decay+reinforce)** |
| Task allocation | Static roles | Pre-defined | Round-robin | LLM decides | **ACO self-organization** |
| Review cycles | None | Manual graph | None | Verification subagent | **Built-in test→review→fix loops** |
| Shared codebase | None | None | None | Single-agent filesystem | **Workspace w/ leasing+contracts** |
| Learning over time | None | None | None | Session memory | **Stigmergic RL meta-learning** |
| Specialization | Static roles | Static nodes | Static | 6 subagent types | **Emergent (Response Thresholds)** |
| Codebase index | None | None | None | None (dynamic grep) | **Auto-deposited file pheromones** |
| Framework lock-in | Yes | Yes | Yes | Yes | **Framework-agnostic (MCP)** |

---

## 2. COMPLETE THEORETICAL INVENTORY

### 16 Concepts from 10 Academic Fields

| # | Concept | Field | Role in Pheromone | Phase |
|---|---------|-------|-------------------|-------|
| 1 | Ant Colony Optimization (Dorigo 1991) | Swarm Intelligence | Task allocation core formula | 1 |
| 2 | Stigmergy (Grassé 1959) | Entomology | Core coordination principle | 1 |
| 3 | MAX-MIN Ant System (Stützle & Dorigo 2002) | Metaheuristics | Pheromone convergence bounds | 1 |
| 4 | Lévy Flight Exploration (Viswanathan 1999) | Optimal Foraging Theory | Replaces ε-greedy exploration | 1 |
| 5 | Bayesian Trust — Beta-Binomial | Bayesian Statistics | Agent reliability scoring | 1 |
| 6 | DAG Scheduling — Kahn's Algorithm | Graph Theory | Task dependency resolution | 1 |
| 7 | Circuit Breaker (Nygard) | Distributed Systems | Per-agent fault tolerance | 2 |
| 8 | Response Threshold Model (Bonabeau 1996) | Swarm Intelligence | Emergent agent specialization | 1 |
| 9 | Quorum Sensing | Microbiology | Collective decision validation | 2 |
| 10 | Information Foraging Theory (Pirolli & Card 1999) | HCI / Cognitive Science | Sensing system formalization | 1 |
| 11 | Stigmergic Reinforcement Learning | **Novel contribution** | Colony self-optimizes parameters | 3 |
| 12 | Positive-Negative Feedback | Complex Systems | Self-organization dynamics | 1 |
| 13 | Eventual Consistency | Distributed Databases | Pheromone store semantics | 1 |
| 14 | Semantic Similarity Search | NLP / Info Retrieval | Pheromone sensing mechanism | 1 |
| 15 | Optimistic Concurrency Control | Database Theory (MVCC) | Task claim conflict resolution | 1 |
| 16 | Adaptive Colony Composition | **Novel contribution** | Colony self-assembles agent team | 2 |

### 5 Novel Contributions (Publishable)
1. **Stigmergic coordination for LLM agents** — First formal ACO adaptation for LLM multi-agent task allocation with convergence guarantees
2. **Response Threshold Model for AI agent specialization** — First application of Bonabeau's threshold dynamics to LLM agent role emergence
3. **Stigmergic Reinforcement Learning** — Colony learns to optimize its own coordination parameters via policy gradient from outcome rewards
4. **Adaptive Colony Composition** — Colony analyzes goals and self-assembles optimal agent teams
5. **PheromBench** — First standardized benchmark for multi-agent coordination quality


---

## 3. CONSTANTS REFERENCE

All battle-tested defaults centralized in `pheromone/constants.py`. Sources: Claude Code production values (CC:), Pheromone-specific (PH:), academic literature (LIT:).

```python
# ═══════════════════════════════════════════
# EXECUTION LIMITS
# ═══════════════════════════════════════════
AGENT_TASK_TIMEOUT_SECONDS = 300          # CC: MAX_EXECUTION_MS (5 min per task)
AGENT_MAX_TURNS_PER_TASK = 25             # PH: ReAct loop iteration cap
TOOL_DEFAULT_TIMEOUT_SECONDS = 120        # CC: BASH_DEFAULT_TIMEOUT
TOOL_MAX_TIMEOUT_SECONDS = 600            # CC: BASH_MAX_TIMEOUT (10 min)
MAX_TOOL_CONCURRENCY = 10                 # CC: MAX_TOOL_USE_CONCURRENCY

# ═══════════════════════════════════════════
# RESULT SIZE LIMITS
# ═══════════════════════════════════════════
MAX_RESULT_SIZE_CHARS = 50_000            # CC: DEFAULT_MAX_RESULT_SIZE_CHARS
MAX_RESULTS_PER_MESSAGE_CHARS = 200_000   # CC: MAX_TOOL_RESULTS_PER_MESSAGE_CHARS
MAX_RESULT_TOKENS = 100_000              # CC: MAX_TOOL_RESULT_TOKENS
MAX_FILE_READ_SIZE_BYTES = 1_073_741_824  # CC: 1 GiB max file read
DEFAULT_FILE_READ_LINES = 2_000           # CC: FILE_READ_DEFAULT_LINES
GREP_MAX_RESULTS = 250                    # CC: GREP_DEFAULT_HEAD_LIMIT

# ═══════════════════════════════════════════
# API RETRY STRATEGY
# ═══════════════════════════════════════════
API_MAX_RETRIES = 10                      # CC: DEFAULT_MAX_RETRIES
API_MAX_OVERLOAD_RETRIES = 3              # CC: MAX_529_RETRIES
API_BASE_DELAY_MS = 500                   # CC: BASE_DELAY_MS
API_MAX_BACKOFF_MS = 300_000              # CC: 5 min max backoff

# ═══════════════════════════════════════════
# CONTEXT & TOKEN MANAGEMENT
# ═══════════════════════════════════════════
CONTEXT_COMPACTION_THRESHOLD = 0.90       # CC: Compact at 90% capacity
COMPACTION_STOP_DELTA_TOKENS = 500        # CC: Stop if <500 token savings
TOKEN_ESTIMATION_DIVISOR = 4              # CC: chars/4 ≈ tokens heuristic
TOKEN_SAFETY_MARGIN = 0.10               # CC: 10% reserved
THINKING_BUDGET_FOR_COUNTING = 1024       # CC: THINKING_BUDGET_FOR_COUNTING

# ═══════════════════════════════════════════
# PHEROMONE SYSTEM
# ═══════════════════════════════════════════
TAU_MIN = 0.01                            # LIT: MAX-MIN lower bound (Stützle 2002)
TAU_MAX = 5.0                             # LIT: MAX-MIN upper bound
PHEROMONE_COMPACTION_THRESHOLD = 50       # PH: Per type before summarization
PHEROMONE_PRESERVATION_WINDOW = 10        # PH: Recent kept verbatim during compaction
ACO_ALPHA = 2.0                           # LIT: Capability pheromone weight
ACO_BETA = 1.0                            # LIT: Urgency heuristic weight
ACO_GAMMA = 1.5                           # PH: Historical success weight
LEVY_MU = 1.5                             # LIT: Lévy exponent (Viswanathan 1999)
EPSILON_INITIAL = 0.3                     # PH: Initial exploration rate
EPSILON_MIN = 0.05                        # PH: Minimum exploration rate
EPSILON_DECAY = 0.95                      # PH: Per-round decay multiplier

# ═══════════════════════════════════════════
# AGENT THRESHOLDS (Response Threshold Model)
# ═══════════════════════════════════════════
THRESHOLD_MIN = 0.05                      # LIT: θ_min (Bonabeau 1996)
THRESHOLD_MAX = 0.95                      # LIT: θ_max
THRESHOLD_INITIAL = 0.5                   # PH: Neutral starting point
THRESHOLD_SUCCESS_DELTA = 0.05            # PH: Decrease on success (specialize)
THRESHOLD_FAILURE_DELTA = 0.08            # PH: Increase on failure (back off)
THRESHOLD_IDLE_DELTA = 0.01              # PH: Increase per idle cycle (drift)

# ═══════════════════════════════════════════
# WORKSPACE & FILE OPERATIONS
# ═══════════════════════════════════════════
FILE_LEASE_TTL_SECONDS = 60               # PH: Auto-release after timeout
HEARTBEAT_INTERVAL_SECONDS = 30           # PH: Agent liveness signal
DEAD_AGENT_MULTIPLIER = 3                 # PH: Dead if no heartbeat for 3× interval
GIT_STATUS_MAX_CHARS = 2_000              # CC: Status truncation

# ═══════════════════════════════════════════
# QUALITY CONTROL
# ═══════════════════════════════════════════
QUORUM_DECOMPOSITION = 0.60              # PH: 60% must approve decomposition
QUORUM_RESULT = 0.50                     # PH: 50% must approve high-stakes results
QUORUM_ADR = 0.50                        # PH: 50% must ratify ADR
QUORUM_TIMEOUT_SECONDS = 30              # PH: Max wait for votes
MAX_REVISIONS = 3                        # PH: Max review-fix cycles per task
REVIEW_TIMEOUT_SECONDS = 120             # PH: Max wait for reviewer

# ═══════════════════════════════════════════
# MONITORING
# ═══════════════════════════════════════════
RING_BUFFER_ACTIVITIES = 10               # CC: MAX_ACTIVITIES
RING_BUFFER_ERRORS = 100                  # CC: MAX_ERRORS
SLOW_OP_LOG_THRESHOLD_MS = 2_000          # CC: SLOW_OP_LOG_THRESHOLD
DENIAL_THRESHOLD = 3                      # CC: Denials before auto-deny
DENIAL_WINDOW_SECONDS = 60                # CC: Tracking window

# ═══════════════════════════════════════════
# STIGMERGIC RL
# ═══════════════════════════════════════════
SRL_LEARNING_RATE = 0.01                  # PH: Slow meta-learning
SRL_EMA_ALPHA = 0.1                       # PH: Running average decay
SRL_REWARD_QUALITY_WEIGHT = 0.4           # PH: Quality component
SRL_REWARD_COMPLETION_WEIGHT = 0.3        # PH: Task completion component
SRL_REWARD_COST_WEIGHT = 0.2             # PH: Cost efficiency component
SRL_REWARD_TIME_WEIGHT = 0.1             # PH: Time efficiency component
```

---

## 4. CORE DATA MODELS

### 4.1 Pheromone Types (8 total)

```
KNOWLEDGE       — Facts, findings, insights discovered during work
CAPABILITY      — Agent skills (auto-calibrated from outcomes)
COORDINATION    — Work status signals (CLAIMED, IN_PROGRESS, HEARTBEAT, etc.)
RESULT          — Completed work products (code, text, analysis)
WARNING         — Failure signals, risks, concerns
GOAL            — Top-level goals submitted to colony
META            — Summarized/aggregated pheromones + colony meta-parameters
ADR             — Architectural Decision Records (binding cross-cutting constraints)
```

### 4.2 Pheromone Base Model

```python
class Pheromone(BaseModel):
    id: str = Field(default_factory=uuid4_str)
    type: PheromoneType
    content: dict                           # Type-specific payload (validated per type)
    strength: float = Field(default=1.0)    # Clamped to [TAU_MIN, TAU_MAX] by environment
    decay_rate: float = Field(default=0.05, ge=0.0, le=1.0)
    depositor_id: str
    depositor_trust: float = Field(default=0.5, ge=0.0, le=1.0)
    task_context: str | None = None
    scope: PheromoneScope = PheromoneScope.COLONY
    tags: list[str] = Field(default_factory=list)
    embedding: list[float] | None = None    # Computed at deposit time
    schema_version: int = 1
    contradicts: list[str] = []             # IDs of contradicting pheromones
    
    created_at: datetime
    last_reinforced: datetime | None = None
    reinforcement_count: int = 0
    content_hash: str | None = None         # SHA-256 integrity
    
    @property
    def effective_strength(self) -> float:
        return self.strength * self.depositor_trust

class PheromoneScope(str, Enum):
    PRIVATE = "private"       # Only depositor can sense
    TEAM = "team"             # Only matching team_id
    COLONY = "colony"         # All agents (default)
    FEDERATED = "federated"   # Shared across federated colonies
```

### 4.3 Hierarchical Task Model

```python
class TaskLevel(str, Enum):
    EPIC = "epic"
    FEATURE = "feature"
    TASK = "task"
    SUBTASK = "subtask"

class TaskStatus(str, Enum):
    PENDING = "PENDING"
    AVAILABLE = "AVAILABLE"
    CLAIMED = "CLAIMED"
    IN_PROGRESS = "IN_PROGRESS"
    TESTING = "TESTING"
    FIX_NEEDED = "FIX_NEEDED"
    REVIEW_PENDING = "REVIEW_PENDING"
    REVISION_NEEDED = "REVISION_NEEDED"
    INTEGRATION_CHECK = "INTEGRATION_CHECK"
    COMPLETED = "COMPLETED"
    FAILED = "FAILED"
    ABANDONED = "ABANDONED"

class TaskNode(BaseModel):
    id: str = Field(default_factory=uuid4_str)
    level: TaskLevel
    description: str
    acceptance_criteria: list[str] = []
    required_skills: list[str] = []
    dependencies: list[str] = []
    children: list[str] = []
    parent_id: str | None = None
    
    estimated_complexity: str = "medium"
    max_retries: int = 3
    timeout_seconds: int = AGENT_TASK_TIMEOUT_SECONDS
    requires_review: bool = True
    requires_integration_check: bool = False
    
    status: TaskStatus = TaskStatus.PENDING
    assigned_agent: str | None = None
    result_pheromone_id: str | None = None
    review_history: list[ReviewRecord] = []
    revision_count: int = 0
    max_revisions: int = MAX_REVISIONS
    
    prd_requirements: list[str] = []
    coverage_verified: bool = False

class ReviewRecord(BaseModel):
    reviewer_id: str
    verdict: str          # "approved" | "revision_needed"
    feedback: str
    timestamp: datetime
    revision_number: int

class HierarchicalTaskGraph(BaseModel):
    goal_id: str
    goal_text: str
    specification: SpecificationModel | None = None
    nodes: dict[str, TaskNode]
    edges: list[tuple[str, str]]
    
    def get_leaf_tasks(self) -> list[TaskNode]:
        return [n for n in self.nodes.values() if not n.children]
    
    def get_available_leaves(self) -> list[TaskNode]:
        completed_ids = {nid for nid, n in self.nodes.items() 
                        if n.status == TaskStatus.COMPLETED}
        return [n for n in self.get_leaf_tasks() 
                if n.status == TaskStatus.AVAILABLE 
                and all(d in completed_ids for d in n.dependencies)]
    
    def get_execution_waves(self) -> list[list[str]]:
        """Kahn's algorithm: topological sort into parallelizable waves."""
        leaves = {n.id: n for n in self.get_leaf_tasks()}
        in_degree = {nid: 0 for nid in leaves}
        adj = {nid: [] for nid in leaves}
        for src, dst in self.edges:
            if src in leaves and dst in leaves:
                adj[src].append(dst)
                in_degree[dst] += 1
        waves, queue = [], [nid for nid, deg in in_degree.items() if deg == 0]
        while queue:
            waves.append(list(queue))
            next_q = []
            for node in queue:
                for nb in adj.get(node, []):
                    in_degree[nb] -= 1
                    if in_degree[nb] == 0:
                        next_q.append(nb)
            queue = next_q
        return waves
    
    def validate_dag(self) -> bool:
        waves = self.get_execution_waves()
        return sum(len(w) for w in waves) == len(self.get_leaf_tasks())
    
    def get_specification_coverage(self) -> dict:
        if not self.specification:
            return {"covered": set(), "uncovered": set(), "coverage_pct": 100.0}
        all_reqs = set(self.specification.requirement_ids)
        covered = set()
        for n in self.nodes.values():
            if n.status == TaskStatus.COMPLETED:
                covered.update(n.prd_requirements)
        uncovered = all_reqs - covered
        return {"covered": covered, "uncovered": uncovered,
                "coverage_pct": len(covered) / max(1, len(all_reqs)) * 100}

class SpecificationModel(BaseModel):
    raw_text: str
    requirements: list[Requirement]
    requirement_ids: list[str] = []

class Requirement(BaseModel):
    id: str
    description: str
    priority: str = "must"        # MoSCoW: must|should|could|wont
    category: str = "functional"
    acceptance_criteria: list[str] = []
    verified: bool = False
```

### 4.4 Shared Workspace Model

```python
class SharedWorkspace(BaseModel):
    project_root: str
    file_tree: dict[str, FileInfo] = {}
    conventions: list[str] = []
    api_contracts: dict[str, APIContract] = {}
    active_adrs: list[str] = []
    dependency_graph: dict[str, list[str]] = {}
    test_results: TestResults | None = None

class FileInfo(BaseModel):
    path: str
    content_hash: str
    last_modified_by: str
    last_modified_at: datetime
    language: str | None = None
    size_bytes: int = 0

class APIContract(BaseModel):
    module_name: str
    exports: list[str]
    expected_inputs: dict[str, str]
    expected_outputs: dict[str, str]
    defined_by_agent: str
    consumed_by_agents: list[str] = []

class FileLease(BaseModel):
    path: str
    holder_agent_id: str
    acquired_at: datetime
    ttl_seconds: int = FILE_LEASE_TTL_SECONDS
    content_hash_at_acquire: str

class ADRPayload(BaseModel):
    decision: str
    rationale: str
    scope: str
    binding: bool = True
    alternatives_rejected: list[str] = []
    decided_by: str
    approved_by: list[str] = []
    affects_skills: list[str] = []
    supersedes: str | None = None
```


---

## 5. PHEROMONE ENVIRONMENT

### 5.1 Store Interface
```
deposit(pheromone) → str           # Atomic. Validates. Hashes. Embeds. Bounds. Audits.
get(id) → Pheromone | None
sense(query) → SenseResult         # Info Foraging: ranked by scent, within budget
update_strength(id, new) → bool    # Atomic. Enforces MAX-MIN.
bulk_decay(rate) → int             # Atomic. Returns evaporated count.
count(type?) → int
get_audit_log(since?) → list
```

### 5.2 MAX-MIN Bounds (Stützle & Dorigo 2002)
```
On every deposit/reinforce: strength = clamp(strength, TAU_MIN, TAU_MAX)
On every decay: if strength < TAU_MIN → evaporate (delete pheromone)
Convergence: Under these bounds with P(explore) > 0, system converges 
to within factor (1+δ) of optimal as iterations increase (Gutjahr 2002).
```

### 5.3 Pheromone Update Rules
```
Evaporation (every cycle):    τ(t+1) = (1 - ρ) × τ(t)
Reinforcement (on success):   τ(t+1) = min(TAU_MAX, τ(t) + Δτ)
Penalty (on failure):         τ(t+1) = max(TAU_MIN, τ(t) × 0.8)
```

### 5.4 Sensing System (Information Foraging Theory)

```
scent(p, a, t) = relevance(p,t) × strength(p) × trust(p.depositor) × freshness(p)

where:
  relevance = cosine_similarity(p.embedding, t.embedding)
  strength = p.effective_strength (bounded by MAX-MIN)
  trust = depositor's Bayesian trust score
  freshness = 1 / (1 + age_hours × decay_weight)

Patch-leaving: stop sensing a type when marginal_scent < 0.1 × best_scent

Token budget allocation (per agent per sense operation):
  ADRs (binding):         15% — ALWAYS injected for affected tasks
  Dependency results:     40% — Outputs from predecessor tasks
  Knowledge:              30% — Facts discovered by other agents
  Warnings:               10% — Failure signals
  Coordination:            5% — Status updates
```

### 5.5 Pheromone Compaction (9-Section Summarization)

Adapted from Claude Code's conversation compaction algorithm. Uses summarization, NOT truncation.

```python
class PheromoneCompactor:
    """
    When pheromone count exceeds PHEROMONE_COMPACTION_THRESHOLD per type,
    generate a META pheromone summarizing the old ones.
    """
    SECTIONS = [
        "goal_context",           # Original goal + current understanding
        "knowledge_discovered",   # Merged KNOWLEDGE pheromones
        "decisions_made",         # Merged ADR pheromones
        "files_modified",         # Files created/changed + state
        "errors_encountered",     # Merged WARNING pheromones
        "agent_capabilities",     # Agent specialization state
        "pending_work",           # Incomplete tasks
        "coordination_state",     # Current agent assignments
        "colony_metrics",         # Quality, cost, tokens
    ]
    
    async def compact(self, env: PheromoneEnvironment, pheromone_type: PheromoneType):
        pheromones = await env.sense(SenseQuery(type=pheromone_type, limit=1000))
        
        # Keep PHEROMONE_PRESERVATION_WINDOW most recent verbatim
        recent = pheromones[-PHEROMONE_PRESERVATION_WINDOW:]
        old = pheromones[:-PHEROMONE_PRESERVATION_WINDOW]
        
        if len(old) < PHEROMONE_COMPACTION_THRESHOLD:
            return  # Not enough to compact
        
        # Generate structured summary via LLM
        summary = await self.summarize(old, self.SECTIONS)
        
        # Deposit META pheromone
        await env.deposit(Pheromone(
            type=PheromoneType.META,
            content={"summary": summary, "compacted_count": len(old),
                     "compacted_ids": [p.id for p in old]},
            strength=TAU_MAX * 0.8,   # Strong but not maximum
            decay_rate=0.005,          # Very slow decay
            depositor_id="compactor",
            depositor_trust=1.0,
        ))
        
        # Archive originals (don't delete — audit trail)
        for p in old:
            await env.update_strength(p.id, TAU_MIN)  # Will evaporate on next cycle
```

### 5.6 Codebase Index via Auto-Deposited Pheromones

When any agent reads or modifies a file, the system auto-deposits a KNOWLEDGE pheromone capturing the discovery. Over time, the pheromone environment becomes a rich project index — the structural advantage single-agent tools like Claude Code don't have.

```python
class CodebaseIndexer:
    async def on_file_read(self, path: str, content: str, agent_id: str, env: PheromoneEnvironment):
        """Auto-deposit on every FileRead tool call."""
        exports = self.extract_exports(content, path)
        await env.deposit(Pheromone(
            type=PheromoneType.KNOWLEDGE,
            content={
                "claim": f"File {path} exists and contains: {', '.join(exports[:10])}",
                "evidence": f"Language: {detect_language(path)}, Lines: {content.count(chr(10))+1}",
                "file_path": path,
                "exports": exports,
            },
            tags=["file_index", detect_language(path)] + path.split("/")[:-1],
            decay_rate=0.005,      # Very slow — file structure rarely changes
            depositor_id=agent_id,
            scope=PheromoneScope.COLONY,
        ))
    
    async def on_file_write(self, path: str, change_summary: str, agent_id: str, env: PheromoneEnvironment):
        """Auto-deposit on every FileWrite/FileEdit tool call."""
        await env.deposit(Pheromone(
            type=PheromoneType.KNOWLEDGE,
            content={
                "claim": f"{path} was modified: {change_summary}",
                "modified_by": agent_id,
                "file_path": path,
            },
            tags=["file_mutation", detect_language(path)],
            decay_rate=0.02,      # Slightly faster — changes get superseded
            depositor_id=agent_id,
        ))
```

### 5.7 Scope Enforcement
```
PRIVATE:   Only depositor can sense (agent working notes)
TEAM:      Only agents with matching team_id
COLONY:    All agents in colony (default)
FEDERATED: Shared across federated colonies (strength × 0.5 on propagation)
```

### 5.8 Pheromone Validation Rules

| Type | Required Fields | Reject If |
|------|----------------|-----------|
| KNOWLEDGE | claim, evidence | Empty claim, confidence=1.0 |
| CAPABILITY | agent_id, skill, proficiency | Unknown agent_id |
| COORDINATION | task_id, status | Invalid state transition |
| RESULT | task_id, output | Empty output |
| WARNING | subject_id, description | Non-existent subject |
| ADR | decision, rationale, scope | Empty decision |
| META | summary, compacted_count | Empty summary |
| GOAL | goal_text | Empty text |

---

## 6. AGENT MODEL

### 6.1 Agent Configuration

```python
class AgentConfig(BaseModel):
    name: str
    skills: list[str]
    agent_type: str = "developer"            # Maps to tool profile (§7)
    model: str = "claude-sonnet-4-6"         # LiteLLM model string
    tools: list[str] = []                     # Override tool set (empty = use type default)
    system_prompt_overrides: dict = {}
    team_id: str | None = None
    max_context_tokens: int = 100_000
    pheromone_budget_tokens: int = 10_000
    temperature: float = 0.3
    max_turns_per_task: int = AGENT_MAX_TURNS_PER_TASK
    heartbeat_interval: int = HEARTBEAT_INTERVAL_SECONDS
    task_timeout: int = AGENT_TASK_TIMEOUT_SECONDS
```

### 6.2 Agent Lifecycle (High-Level Phases)
```
IDLE → SENSING → DECIDING → EXECUTING (ReAct loop) → DEPOSITING → IDLE
```

### 6.3 Agent Internal ReAct Loop

The EXECUTING phase internally runs a multi-turn LLM loop with tool use. This is what happens INSIDE a single task execution — not the colony loop. Adapted from Claude Code's ReAct architecture.

```python
class AgentReActLoop:
    async def execute(self, task: TaskNode, context: SenseResult,
                      workspace: SharedWorkspace, agent: AgentConfig) -> TaskOutput:
        
        messages = self.build_initial_context(task, context, workspace, agent)
        
        for turn in range(agent.max_turns_per_task):
            # 1. SAMPLE LLM
            response = await self.llm.create(
                messages=messages,
                model=agent.model,
                tools=self.get_tool_definitions(agent.agent_type),
                temperature=agent.temperature,
                max_tokens=3000,
            )
            
            # 2. CHECK TERMINATION
            if not response.has_tool_calls:
                return self.extract_output(response, task)
            
            if response.stop_reason == "end_turn":
                return self.extract_output(response, task)
            
            # 3. PARSE + EXECUTE TOOLS (read-parallel, write-serial)
            tool_results = await self.tool_orchestrator.execute_tools(
                response.tool_calls, workspace, agent.agent_id
            )
            
            # 4. AUTO-DEPOSIT: file reads/writes trigger codebase index pheromones
            await self.codebase_indexer.process_tool_results(tool_results, agent, self.env)
            
            # 5. APPEND to message history
            messages.append(response.as_assistant_message())
            messages.extend(tool_results.as_tool_result_messages())
            
            # 6. CONTEXT BUDGET CHECK
            token_count = TokenCounter.estimate_fast(str(messages))
            if token_count > agent.max_context_tokens * CONTEXT_COMPACTION_THRESHOLD:
                messages = await self.compact_messages(messages)
        
        # Max turns exhausted
        return TaskOutput(status="incomplete", partial_output=self.extract_partial(messages))
    
    def build_initial_context(self, task, sense_result, workspace, agent) -> list[Message]:
        """Assemble the initial prompt for this task."""
        return [
            SystemMessage(content=AgentPromptBuilder.build(agent, task, workspace, 
                                                           sense_result.adrs)),
            UserMessage(content=self.format_task_prompt(task, sense_result, workspace)),
        ]
```

### 6.4 Tool Orchestration (Per-Agent, Read-Parallel/Write-Serial)

Adapted from Claude Code's `toolOrchestration.ts`:

```python
class ToolOrchestrator:
    async def execute_tools(self, tool_calls: list[ToolCall], 
                            workspace: SharedWorkspace, agent_id: str) -> list[ToolResult]:
        reads = [tc for tc in tool_calls if tc.tool.is_read_only]
        writes = [tc for tc in tool_calls if not tc.tool.is_read_only]
        results = []
        
        # Reads: parallel (bounded concurrency)
        if reads:
            read_coros = [self.run_tool(tc, workspace, agent_id) for tc in reads]
            read_results = await asyncio.gather(
                *read_coros[:MAX_TOOL_CONCURRENCY], return_exceptions=True
            )
            results.extend(self.handle_exceptions(read_results, reads))
        
        # Writes: serial (one at a time, with lease acquisition)
        for tc in writes:
            if tc.tool.requires_lease:
                lease = await workspace.lease_manager.acquire(tc.input.get("file_path"), agent_id)
                if not lease:
                    results.append(ToolResult(error="File locked by another agent", is_error=True))
                    continue
            result = await self.run_tool(tc, workspace, agent_id)
            results.append(result)
            if tc.tool.requires_lease:
                await workspace.lease_manager.release(tc.input.get("file_path"), agent_id)
        
        return results
    
    async def run_tool(self, tc: ToolCall, workspace: SharedWorkspace, agent_id: str) -> ToolResult:
        try:
            result = await asyncio.wait_for(
                tc.tool.execute(tc.input, workspace, agent_id),
                timeout=tc.tool.timeout or TOOL_DEFAULT_TIMEOUT_SECONDS
            )
            return self.cap_result_size(result, MAX_RESULT_SIZE_CHARS)
        except asyncio.TimeoutError:
            return ToolResult(error=f"{tc.tool.name} timed out after {tc.tool.timeout}s", is_error=True)
        except Exception as e:
            return ToolResult(error=str(e), is_error=True)
```

### 6.5 Structured Prompt Engineering (Modular Assembly)

Adapted from Claude Code's `prompts.ts` modular system with static/dynamic boundary:

```python
class AgentPromptBuilder:
    @staticmethod
    def build(agent: AgentConfig, task: TaskNode, 
              workspace: SharedWorkspace, adrs: list[ADRPayload]) -> str:
        sections = []
        
        # ═══ STATIC SECTIONS (cacheable across tasks) ═══
        sections.append(IDENTITY_SECTION.format(name=agent.name, type=agent.agent_type))
        sections.append(ROLE_SECTIONS[agent.agent_type])
        sections.append(COLONY_RULES_SECTION)
        sections.append(TOOL_USAGE_SECTION)
        sections.append(QUALITY_SECTION)
        sections.append(SAFETY_SECTION)
        sections.append(OUTPUT_EFFICIENCY_SECTION)
        
        # ═══ DYNAMIC BOUNDARY ═══
        sections.append("__PHEROMONE_PROMPT_DYNAMIC_BOUNDARY__")
        
        # ═══ DYNAMIC SECTIONS (per-task) ═══
        sections.append(task_context(task))
        sections.append(workspace_context(workspace))
        sections.append(active_adrs(adrs))
        sections.append(conventions(workspace.conventions))
        sections.append(specialization_state(agent))
        
        return "\n\n".join(s for s in sections if s)

# Key prompt sections (adapted from Claude Code):
COLONY_RULES_SECTION = """
# Colony coordination rules
- You are one agent in a colony. Other agents work on related tasks simultaneously.
- Do NOT propose changes to code you haven't read via FileRead.
- Do NOT create files unless absolutely necessary for your task.
- If an approach fails, diagnose why before switching tactics.
- Do NOT add features, refactoring, or improvements beyond your task scope.
- Do NOT add error handling for scenarios that cannot happen. Trust internal code.
- Three similar lines of code is better than a premature abstraction.
- Check active ADRs before making architectural choices — follow binding decisions.
- Deposit KNOWLEDGE pheromones when you discover facts other agents need.
- Deposit WARNING pheromones when something fails or seems risky.
- Deposit ADR pheromones when you make decisions affecting other agents.
- The cost of pausing to verify is low. The cost of breaking another agent's work is high.
- Call multiple tools in parallel if no dependencies between them.
- Use dedicated tools (FileRead not cat, FileEdit not sed, GlobTool not find, GrepTool not grep).
"""

OUTPUT_EFFICIENCY_SECTION = """
# Output efficiency
Go straight to the point. Try the simplest approach first without going in circles.
Keep text output brief and direct. Lead with the action, not the reasoning.
Focus on: decisions needing input, status at milestones, errors changing the plan.
If you can say it in one sentence, don't use three.
"""
```

### 6.6 Response Threshold Model (Bonabeau 1996)

Each agent maintains private internal thresholds per skill — NOT pheromones:

```
θ(agent_a, skill_s) ∈ [THRESHOLD_MIN, THRESHOLD_MAX]

Initial: θ = THRESHOLD_INITIAL (0.5) for all skills

After SUCCESS on task requiring skill s:
    θ(a,s) = max(THRESHOLD_MIN, θ(a,s) - THRESHOLD_SUCCESS_DELTA)    # Specialize
After FAILURE:
    θ(a,s) = min(THRESHOLD_MAX, θ(a,s) + THRESHOLD_FAILURE_DELTA)    # Back off
After INACTIVITY (N cycles without using skill s):
    θ(a,s) = min(THRESHOLD_MAX, θ(a,s) + THRESHOLD_IDLE_DELTA × N)   # Drift

Eligibility gate (pre-ACO filter):
    stimulus(t) > θ(a, required_skill(t))
    stimulus(t) = urgency × priority × (1 + retry_count × 0.2)
```

### 6.7 Bayesian Trust Score (Beta-Binomial)
```
trust(a) = (successes + 1) / (successes + failures + 2)
Initial: 0.5. Floor: 0.1. Cap: 1.0.
All pheromone effective_strength = raw_strength × depositor_trust
```

### 6.8 Adaptive Colony Composition (3 Modes)

**Manual:** `colony.register(Agent(name="backend", skills=["python", "fastapi"]))`.
**Template:** `Colony("dev", template=SoftwareDevTeam())` — auto-registers architect, backend, frontend, qa, devops.
**Adaptive:** `Colony("adaptive", composition="adaptive")` — GoalAnalyzer parses goal, identifies required skills, spawns agents from templates.

Built-in templates: SoftwareDevTeam, ResearchTeam, ContentTeam, DataScienceTeam, ConsultingTeam, LegalTeam, MarketingTeam, GeneralPurpose.

### 6.9 Heartbeat Protocol
```
Every HEARTBEAT_INTERVAL_SECONDS: deposit COORDINATION pheromone (status=HEARTBEAT)
Decay rate: 0.5 (fast). Dead detection: no heartbeat for DEAD_AGENT_MULTIPLIER × interval.
On death: release all leases, release claimed tasks back to AVAILABLE, deposit WARNING.
```


---

## 7. AGENT TOOL SYSTEM

### 7.1 Tool Definition Format

```python
class ToolDefinition(BaseModel):
    name: str
    description: str                       # Shown to LLM — must be precise
    input_schema: dict                     # JSON Schema (validated with Pydantic)
    is_read_only: bool = False
    requires_lease: bool = False
    requires_approval: bool = False
    timeout_seconds: int = TOOL_DEFAULT_TIMEOUT_SECONDS
    
    async def execute(self, input: dict, workspace: SharedWorkspace, 
                      agent_id: str) -> ToolResult

class ToolResult(BaseModel):
    content: str
    is_error: bool = False
    metadata: dict = {}
```

### 7.2 Complete Tool Inventory

```python
# ═══ CORE TOOLS (filesystem + shell + web) ═══
CORE_TOOLS = {
    "FileRead":    ToolDef(read_only=True,  desc="Read file content with line numbers. Default 2000 lines."),
    "FileWrite":   ToolDef(read_only=False, requires_lease=True, desc="Create or overwrite a file."),
    "FileEdit":    ToolDef(read_only=False, requires_lease=True, desc="str_replace editing. Must read before editing."),
    "BashTool":    ToolDef(read_only=False, requires_approval=True, desc="Execute shell commands."),
    "GlobTool":    ToolDef(read_only=True,  desc="Find files matching glob pattern."),
    "GrepTool":    ToolDef(read_only=True,  desc="Search file contents. Max 250 results."),
    "WebSearch":   ToolDef(read_only=True,  desc="Search the web."),
    "WebFetch":    ToolDef(read_only=True,  desc="Fetch and summarize URL content."),
}

# ═══ PHEROMONE TOOLS (colony coordination) ═══
PHEROMONE_TOOLS = {
    "SenseTool":             ToolDef(read_only=True, desc="Query pheromone environment for relevant knowledge."),
    "DepositKnowledge":      ToolDef(read_only=False, desc="Share discovered facts with the colony."),
    "DepositADR":            ToolDef(read_only=False, desc="Record binding architectural decision."),
    "DepositWarning":        ToolDef(read_only=False, desc="Signal failure, risk, or concern."),
    "RequestReview":         ToolDef(read_only=False, desc="Submit output for peer review."),
    "CheckConventions":      ToolDef(read_only=True,  desc="Verify output against active ADRs."),
}

# ═══ WORKSPACE TOOLS (shared state) ═══
WORKSPACE_TOOLS = {
    "AcquireLease":          ToolDef(read_only=False, desc="Get exclusive write access to a file."),
    "ReleaseLease":          ToolDef(read_only=False, desc="Release file write access."),
    "GetProjectContext":     ToolDef(read_only=True,  desc="Get workspace state: file tree, conventions, contracts."),
    "UpdateAPIContract":     ToolDef(read_only=False, desc="Declare a module's interface for other agents."),
    "RunTests":              ToolDef(read_only=True,  desc="Execute tests in workspace."),
}
```

### 7.3 Tool Profiles Per Agent Type

Not all agents need all tools. Restricting tools reduces noise and cost:

| Agent Type | Core Tools | Pheromone Tools | Workspace Tools | Write Access | Default Model |
|-----------|-----------|----------------|-----------------|-------------|--------------|
| researcher | FileRead, Glob, Grep, WebSearch, WebFetch | Sense, DepositKnowledge | GetProjectContext | No | haiku-4.5 |
| architect | FileRead, Glob, Grep, WebSearch | Sense, DepositKnowledge, DepositADR | GetProjectContext | No | sonnet-4.6 |
| developer | ALL core | ALL pheromone | ALL workspace | Yes | sonnet-4.6 |
| reviewer | FileRead, Glob, Grep, Bash, RunTests | Sense, DepositWarning, RequestReview | GetProjectContext | No | sonnet-4.6 |
| tester | FileRead, FileWrite, FileEdit, Bash, Glob, Grep | Sense, DepositKnowledge | GetProjectContext, RunTests | Yes (test files) | haiku-4.5 |

---

## 8. HIERARCHICAL TASK DECOMPOSITION + SPECIFICATION TRACKING

### 8.1 Multi-Level Decomposition

```
Phase 1 — Specification parsing (if PRD provided):
    Parse into structured Requirements with IDs and acceptance criteria

Phase 2 — Epic decomposition: Goal → 3-8 Epics

Phase 3 — Feature decomposition: Epic → 2-5 Features per epic

Phase 4 — Task decomposition: Feature → 1-4 atomic Tasks per feature

Phase 5 — DAG validation: Kahn's algorithm confirms acyclicity, identifies waves

Phase 6 — Coverage check: every requirement mapped to at least one task

For simple goals: skip to Phase 4 (flat task list, like single-agent tools do)
```

### 8.2 Quorum Sensing for Decomposition Validation

```
1. Proposed TaskGraph deposited as PROPOSAL pheromone
2. Each agent evaluates: "Does this decomposition make sense for my skills?"
3. Agents deposit VOTE pheromones (agree / disagree / suggest_change)
4. Accepted when: agreement_count >= ceil(num_agents × QUORUM_DECOMPOSITION)
5. If quorum fails: re-decompose with feedback. Fails twice → accept with WARNING.
6. Timeout: QUORUM_TIMEOUT_SECONDS
```

### 8.3 Specification Coverage Tracking

Throughout execution, each task completion checks off its `prd_requirements`. On completion, if coverage < 90%, generate additional tasks for uncovered requirements.

---

## 9. SHARED WORKSPACE / CODEBASE AWARENESS

### 9.1 WorkspaceManager

```python
class WorkspaceManager:
    async def write_file(self, path, content, agent_id) -> None
    async def read_file(self, path) -> str
    async def edit_file(self, path, old_string, new_string, agent_id, expected_hash) -> EditResult
    async def get_project_context(self, task: TaskNode) -> ProjectContext
    async def check_conventions(self, path, content) -> list[Violation]
    async def update_api_contract(self, module, contract) -> None
    async def check_api_compatibility(self, module_a, module_b) -> list[Issue]
```

### 9.2 File Edit Algorithm (str_replace with Conflict Detection)

Adopted from Claude Code's `FileEditTool/utils.ts`, extended with multi-agent safety:

```python
async def edit_file(self, path: str, old_string: str, new_string: str,
                    agent_id: str, expected_hash: str | None = None) -> EditResult:
    current_content = await self.read_file(path)
    current_hash = sha256(current_content)
    
    # CONFLICT DETECTION
    if expected_hash and current_hash != expected_hash:
        return EditResult(success=False, 
            error="CONFLICT: File modified by another agent since you read it. Re-read and retry.",
            current_hash=current_hash)
    
    # STEP 1: Exact match
    if old_string in current_content:
        new_content = current_content.replace(old_string, new_string, 1)
    # STEP 2: Quote normalization fallback (curly ↔ straight)
    elif self.normalize_quotes(old_string) in current_content:
        normalized = self.normalize_quotes(old_string)
        new_content = current_content.replace(normalized, new_string, 1)
    else:
        return EditResult(success=False, error="String not found in file")
    
    # STEP 3: Sequential edit guard — reject if old_string is substring of previous edit
    # (prevents editing content you just inserted in the same batch)
    
    new_hash = sha256(new_content)
    await self.write_file(path, new_content, agent_id)
    return EditResult(success=True, new_hash=new_hash)
```

### 9.3 File Leasing

```python
class WorkspaceLeaseManager:
    async def acquire(self, path: str, agent_id: str) -> FileLease | None:
        """Try to acquire. If held by another agent, return None."""
    async def release(self, path: str, agent_id: str) -> None
    async def force_release_expired(self) -> int:
        """Release leases past FILE_LEASE_TTL_SECONDS. Returns count."""
```

### 9.4 Convention Enforcement

When an agent deposits a RESULT pheromone, the execution engine checks against active ADRs and workspace conventions. Violations are flagged and the agent revises before the result is accepted.

---

## 10. STIGMERGIC TASK ALLOCATION (ACO + Lévy Flights)

### 10.1 ACO Selection Formula
```
attraction(a, t) = [τ_cap(a,t)]^α × [η_urg(t)]^β × [ρ_hist(a,t)]^γ

τ_cap = capability pheromone strength (skill match)
η_urg = urgency heuristic (priority × deps × retries × complexity)
ρ_hist = historical success rate on similar tasks

Defaults: α=ACO_ALPHA, β=ACO_BETA, γ=ACO_GAMMA (learnable via Stigmergic RL)
```

### 10.2 Pre-Filter: Response Threshold Gate
```
Before ACO: filter eligible agents where stimulus(t) > θ(a, skill) for required skills.
Only eligible agents enter the probability calculation.
```

### 10.3 Lévy Flight Exploration (replaces ε-greedy)
```
P(explore) = max(EPSILON_MIN, EPSILON_INITIAL × EPSILON_DECAY^round)

When exploration triggers:
  step_size ~ Lévy(μ=LEVY_MU) via Mantegna's algorithm
  Small step → explore nearby skills. Large step → explore distant skills.
  Select task whose skill_distance ≈ step_size.
```

### 10.4 Probabilistic Selection + Optimistic Locking
```
P(task_j) = attraction(a, task_j) / Σ_k attraction(a, task_k)
Conflicts: highest attraction score wins. Loser re-evaluates next round.
```

---

## 11. EXECUTION ENGINE (with Iterative Refinement)

### 11.1 Main Loop

```python
async def run(self, goal, colony, strategy):
    # Phase 0: Adaptive composition (if enabled)
    # Phase 1: Parse specification (if provided)
    # Phase 2: Hierarchical decomposition
    # Phase 3: Quorum validation
    # Phase 4: Execution loop
    while not all_terminal(task_graph) and within_budget(colony):
        await check_agent_health(colony)
        available = task_graph.get_available_leaves()
        claims = await colony.allocator.allocate_round(available, colony.agents, colony.environment)
        tasks_coros = [execute_with_review(tid, aid, colony, task_graph) for tid, aid in claims.items()]
        await asyncio.gather(*tasks_coros, return_exceptions=True)
        await colony.evolution.cycle(colony.environment)
        propagate_completion(task_graph)
        await check_integration(task_graph, colony)
    # Phase 5: Specification coverage check
    # Phase 6: Assemble result
```

### 11.2 Task Execution with Review Loop

```
1. SENSE: Agent reads pheromone environment (dependency results, knowledge, ADRs, warnings)
2. EXECUTE: Agent runs ReAct loop (§6.3) with tool use against shared workspace
3. TEST: Run relevant tests. Fail → FIX_NEEDED → loop to step 2 (max 3 fix attempts)
4. CONVENTION CHECK: Verify against active ADRs. Violations → fix before proceeding
5. REVIEW: Different agent reviews. Approved → COMPLETED. Revision needed → loop (max MAX_REVISIONS)
6. DEPOSIT: Result pheromone + trust update + capability reinforcement + threshold adjustment
```

### 11.3 Task State Machine (12 States)

```
PENDING ──(deps met)──→ AVAILABLE ──(claimed)──→ CLAIMED ──(started)──→ IN_PROGRESS
                                                                            │
                              ┌──────────────────────────────────────────────┤
                              ▼                                              ▼
                         TESTING ──(pass)──→ REVIEW_PENDING           (timeout/error)
                              │                    │                         │
                         (fail)│              (approved)                     ▼
                              ▼                    │                      FAILED
                        FIX_NEEDED                 ▼                    (retry→AVAILABLE)
                              │          INTEGRATION_CHECK              (exhausted→ABANDONED)
                              ▼              │         │
                        IN_PROGRESS    (pass)▼    (fail)▼
                                        COMPLETED   fix tasks
                         REVIEW_PENDING
                              │
                       (revision_needed, count < MAX_REVISIONS)
                              ▼
                       REVISION_NEEDED → IN_PROGRESS
```

---

## 12. ARCHITECTURAL DECISION RECORDS (ADRs)

**When created:** Agent chooses a framework, establishes a pattern, creates a shared interface, or selects infrastructure.

**Lifecycle:** Agent deposits ADR → quorum validates (QUORUM_ADR fraction) → if approved, becomes active → injected into all agents' context for affected tasks → can be superseded by newer ADR.

**Binding enforcement:** Before accepting RESULT pheromones, check output against active binding ADRs. Non-compliant results sent back for revision.

---

## 13. INTEGRATION VERIFICATION LAYER

After all tasks under a FEATURE complete:
1. API contract verification (do interfaces match?)
2. Dependency resolution (do imports resolve?)
3. Integration test generation + execution
4. Cross-module consistency check

Failures generate specific FIX tasks targeting incompatibilities, assigned to the agents who built the conflicting modules.

---

## 14. EVOLUTION ENGINE (with Stigmergic RL)

### Four Mechanisms

**1. Decay** — Per-type rates:
```
knowledge: 0.02, capability: 0.01, coordination: 0.30, result: 0.02,
warning: 0.10, ADR: 0.005, meta: 0.005, goal: 0.01
```

**2. Reinforcement** — On success: capability +0.2, used knowledge +0.1, followed ADRs +0.05.

**3. Capability Calibration** — Proficiency, avg_completion_time, avg_quality as EMAs.

**4. Stigmergic RL (Novel)** — After each colony.solve():
```
Reward = SRL_REWARD_QUALITY_WEIGHT × quality
       + SRL_REWARD_COMPLETION_WEIGHT × (completed/total)
       + SRL_REWARD_COST_WEIGHT × (1 - cost/budget)
       + SRL_REWARD_TIME_WEIGHT × (1 - time/timeout)

Update θ_colony = {α, β, γ, ρ, ε} via REINFORCE with SRL_LEARNING_RATE.
Running average updated with SRL_EMA_ALPHA.
Stored as META pheromones (decay 0.005) — persist across colony runs.
```

---

## 15. QUALITY CONTROL (Quorum Sensing + Trust)

### Quorum Applications
- Decomposition validation: QUORUM_DECOMPOSITION (0.6)
- High-stakes result validation: QUORUM_RESULT (0.5)
- ADR ratification: QUORUM_ADR (0.5)
- Timeout: QUORUM_TIMEOUT_SECONDS. Fallback: accept with WARNING.

### Knowledge Conflict Resolution
When KNOWLEDGE pheromone contradicts existing (embedding similarity > 0.8 + semantic negation): both flagged, RESOLUTION task created, resolver deposits VERDICT, winner reinforced, loser weakened.


---

## 16. FAULT TOLERANCE & RESILIENCE

| Failure Mode | Detection | Recovery |
|-------------|-----------|----------|
| Agent crash | No heartbeat 3× interval | Release leases+tasks, mark DEAD, reassign |
| LLM API timeout | asyncio.wait_for | Retry (API_MAX_RETRIES) → different model |
| LLM rate limit | 429 response | Parse Retry-After, exponential backoff |
| LLM overloaded | 529 response | Max API_MAX_OVERLOAD_RETRIES, then fail |
| Task timeout | AGENT_TASK_TIMEOUT_SECONDS | Kill, FAILED, retry with WARNING |
| Circular deps | Kahn's validation | Re-decompose with acyclicity constraint |
| Livelock | Claim-release count >3 | Force-assign to highest-trust agent |
| Budget exhausted | Budget.is_exhausted() | Graceful stop, return best results |
| Review deadlock | REVIEW_TIMEOUT_SECONDS | Auto-approve with quality_warning |
| Integration failure | IntegrationVerifier | Generate fix tasks, re-verify |
| Convention violation | Workspace check | Agent revises before result accepted |
| File edit conflict | Content hash mismatch | Agent re-reads file, retries edit |
| Store failure | Connection error | Fallback to InMemoryStore, log warning |
| Prompt too long | Token count > limit | Compact context, retry |
| Malformed LLM output | Parse failure | Error returned to LLM, max 3 retries |

### Circuit Breaker (per agent)
```
CLOSED → (3 consecutive failures) → OPEN → (60s) → HALF_OPEN → test
Success → CLOSED. Failure → OPEN. Agent in OPEN excluded from allocation.
```

---

## 17. CONCURRENCY MODEL

```
Agent phases NEVER overlap within one agent: IDLE → SENSING → DECIDING → EXECUTING → DEPOSITING → IDLE
Within EXECUTING: ReAct loop with read-parallel/write-serial tool orchestration.
Colony level: multiple agents execute different tasks concurrently.
```

**Guarantees:**
1. Pheromone reads: non-blocking snapshots
2. Pheromone writes: per-pheromone atomic (no global lock)
3. Task claims: optimistic locking (highest attraction wins)
4. Decay: bulk-atomic (all-or-nothing per cycle)
5. Workspace writes: file-level leasing (two agents can't write same file)
6. No global locks anywhere in the system

---

## 18. COST MANAGEMENT

```python
class Budget(BaseModel):
    max_dollars: float = 5.0
    max_tokens: int = 2_000_000
    spent_dollars: float = 0.0
    spent_tokens: int = 0
```

When utilization > 50%: `attraction *= 1.0 / (agent.avg_cost_per_task + 0.01)` naturally shifts to cheaper agents.

Deduplication: before LLM call, check knowledge pheromones. If relevant knowledge exists (strength > 0.5, trust > 0.6), use it instead of API call. Codebase index pheromones (§5.6) prevent redundant file reads.

---

## 19. CONTEXT WINDOW MANAGEMENT

### Dual Token Counting (from Claude Code)
```python
class TokenCounter:
    @staticmethod
    def estimate_fast(text: str) -> int:
        return len(text) // TOKEN_ESTIMATION_DIVISOR   # chars/4, ~10-15% overestimate
    
    @staticmethod
    async def count_accurate(text: str, model: str) -> int:
        return await anthropic.count_tokens(text, model=model)  # API-based, ±1%
```

### Context Budget Allocation (per agent)
```
System prompt:          ~2,000 tokens
Task description:       ~500 tokens
Workspace context:      ~5,000 tokens (file tree, conventions, API contracts)
Pheromone context:      ~10,000 tokens (allocated per §5.4 priorities)
Agent response:         ~remaining
Safety margin:          TOKEN_SAFETY_MARGIN (10%)
```

### Compaction Trigger
At CONTEXT_COMPACTION_THRESHOLD (90%) of budget → compact via 9-section summarization (§5.5).
Stop compaction when delta < COMPACTION_STOP_DELTA_TOKENS (500).

---

## 20. SECURITY MODEL

| Threat | Mitigation |
|--------|-----------|
| Pheromone poisoning | Trust scoring + validation + rate limits (50 deposits/agent/min) |
| Agent impersonation | Colony-issued UUID tokens |
| Content tampering | SHA-256 hash verified on read |
| Cross-colony leakage | Namespace isolation (colony_id prefix) |
| Workspace sabotage | File leasing + convention enforcement |
| Cost attack | Budget manager with colony-level cap |
| Replay attacks | Reject future timestamps |
| Sensitive data in env | Sanitize: ANTHROPIC_API_KEY, AWS_SECRET_*, JWT_SECRET etc. |

---

## 21. OBSERVABILITY

### Structured Logging
Every operation: timestamp, colony_id, component, event, agent_id, task_id, correlation_id, details (JSON).

### Ring Buffers (from Claude Code)
```python
activity_buffer = RingBuffer(RING_BUFFER_ACTIVITIES)   # Last 10 activities
error_buffer = RingBuffer(RING_BUFFER_ERRORS)           # Last 100 errors
slow_ops_buffer = RingBuffer(50)                        # Operations > SLOW_OP_LOG_THRESHOLD_MS
```

### Prometheus Metrics
```
pheromone_tasks_total{colony,status}
pheromone_cost_dollars{colony}
pheromone_count{colony,type}
pheromone_agent_trust{colony,agent}
pheromone_agent_threshold{colony,agent,skill}
pheromone_meta_params{colony,param}
pheromone_execution_seconds{colony,agent}
pheromone_review_cycles{colony}
pheromone_spec_coverage{colony}
```

### Colony Replay
Full audit trail enables deterministic step-through of past executions.

---

## 22. TOOL INTEGRATION

When agents use tools, results shared as pheromones to prevent duplication:

```python
class ToolPheromone(BaseModel):
    tool_name: str
    tool_input: str
    tool_output_summary: str    # Summarized, not raw
    success: bool
    latency_ms: float
    cost_usd: float
```

---

## 23. LONG-RUNNING TASK SUPPORT

```python
class CheckpointPheromone(BaseModel):
    task_id: str
    agent_id: str
    checkpoint_data: dict
    progress: float
    resumable: bool
    expires_at: datetime
```
Agent crashes → another resumes from latest checkpoint.

---

## 24. HUMAN-IN-THE-LOOP (3-Way Permission Model)

Adopted from Claude Code's full permission architecture:

```python
class PermissionDecision(BaseModel):
    behavior: Literal["allow", "ask", "deny"]
    message: str | None = None
    reason: PermissionReason

class PermissionReason(str, Enum):
    RULE = "rule"
    MODE = "mode"
    CLASSIFIER = "classifier"
    QUORUM = "quorum"
    HUMAN = "human"
    SAFETY = "safety"
    CONVENTION = "convention"
    BUDGET = "budget"

class DenialTracker:
    """Stop asking after DENIAL_THRESHOLD denials in DENIAL_WINDOW_SECONDS."""

class ColonyPermissionSync:
    """Human approves for one agent → propagates to all agents in colony."""
```

---

## 25. MULTI-COLONY FEDERATION

```python
class Federation:
    def federate(self, colony_a, colony_b, share_knowledge=True, share_meta=False):
        """Link colonies. Only knowledge + meta shared; coordination stays local."""
    def propagate(self, pheromone, from_colony, to_colony):
        """Strength reduced by 0.5× on federation boundary."""
```

---

## 26. CLAUDE.MD COMPATIBILITY LAYER

Bridge existing Claude Code project configurations into the pheromone environment:

```python
class CLAUDEMDLoader:
    SEARCH_PATHS = [
        "./CLAUDE.md", "./.claude/CLAUDE.md", "./.claude/memory/*.md",
        "~/.claude/CLAUDE.md", "~/.claude/memory/*.md",
    ]
    
    async def load_into_environment(self, env: PheromoneEnvironment) -> int:
        """Read CLAUDE.md files, deposit as high-strength binding ADR pheromones."""
        for path in self.find_files():
            content = await self.read_file(path)
            await env.deposit(Pheromone(
                type=PheromoneType.ADR,
                content={"decision": f"Project directive from {path}",
                         "rationale": "Pre-existing project configuration",
                         "scope": "global", "binding": True, "raw_text": content},
                strength=TAU_MAX,
                decay_rate=0.001,
                depositor_id="system",
                depositor_trust=1.0,
            ))
```

---

## 27. INTEGRATION PROTOCOL (PPS + MCP)

### REST API
```
POST /api/v1/colony/{id}/solve
POST /api/v1/colony/{id}/deposit
POST /api/v1/colony/{id}/sense
GET  /api/v1/colony/{id}/state
GET  /api/v1/colony/{id}/workspace
WS   /api/v1/colony/{id}/stream
```

### MCP Compatibility

Colony exposed as MCP server for ecosystem interoperability:
```python
class PheromonesMCPServer:
    server_name = "pheromone/colony"
    tools = ["pheromone_sense", "pheromone_deposit", "pheromone_claim_task",
             "pheromone_submit_result", "workspace_read", "workspace_write", "colony_status"]
```
Any MCP-compatible tool (Claude Code, Cursor, etc.) can join a Pheromone colony as an agent.

### Python SDK
```python
client = PheromoneClient(url, colony_id)
await client.sense(query, types)
await client.deposit_knowledge(claim, evidence, confidence)
```

---

## 28. DEPLOYMENT ARCHITECTURE

**Local:** Single Python process (dev/testing)
**Docker:** Colony server (FastAPI + Redis) + agent containers via docker-compose.yml
**Cloud:** Colony on Railway/Fly.io, Redis on Upstash, agents anywhere via REST/MCP


---

## 29. PROJECT STRUCTURE

```
pheromone/
├── pyproject.toml, README.md, LICENSE (Apache 2.0), CONTRIBUTING.md
├── docker-compose.yml, Dockerfile
│
├── pheromone/
│   ├── __init__.py
│   ├── colony.py                           # Colony class (entry point)
│   ├── constants.py                        # ALL constants (§3)
│   │
│   ├── models/
│   │   ├── pheromones.py                   # Pheromone types + payloads
│   │   ├── tasks.py                        # HierarchicalTaskGraph, TaskNode, TaskStatus
│   │   ├── workspace.py                    # SharedWorkspace, FileInfo, APIContract, FileLease
│   │   ├── config.py                       # Strategy, Budget, QuorumConfig, ApprovalConfig
│   │   ├── results.py                      # ColonyResult, AuditEntry
│   │   └── specifications.py              # SpecificationModel, Requirement
│   │
│   ├── agents/
│   │   ├── proxy.py                        # AgentProxy (ReAct loop, §6.3)
│   │   ├── react_loop.py                   # AgentReActLoop implementation
│   │   ├── tool_orchestrator.py            # Read-parallel/write-serial (§6.4)
│   │   ├── prompt_builder.py               # Modular prompt assembly (§6.5)
│   │   ├── thresholds.py                   # Response Threshold Model (§6.6)
│   │   ├── composer.py                     # GoalAnalyzer + Adaptive Composition
│   │   └── templates.py                    # 8 built-in colony templates
│   │
│   ├── engine/
│   │   ├── execution.py                    # ExecutionEngine main loop (§11)
│   │   ├── decomposer.py                   # Hierarchical decomposition (§8)
│   │   ├── allocator.py                    # StigmergicAllocator (§10)
│   │   ├── reviewer.py                     # Review cycle management
│   │   ├── integrator.py                   # Integration verification (§13)
│   │   └── evolution.py                    # EvolutionEngine + Stigmergic RL (§14)
│   │
│   ├── environment/
│   │   ├── environment.py                  # PheromoneEnvironment (§5)
│   │   ├── sensing.py                      # Information Foraging sensing (§5.4)
│   │   ├── compactor.py                    # 9-section compaction (§5.5)
│   │   ├── indexer.py                      # Codebase auto-indexing (§5.6)
│   │   ├── embeddings.py                   # Sentence-transformer integration
│   │   ├── quorum.py                       # Quorum Sensing protocol
│   │   └── conflicts.py                    # Knowledge conflict resolution
│   │
│   ├── workspace/
│   │   ├── manager.py                      # WorkspaceManager (§9.1)
│   │   ├── editor.py                       # FileEditor with str_replace (§9.2)
│   │   ├── leasing.py                      # File lease management (§9.3)
│   │   ├── conventions.py                  # Convention enforcement (§9.4)
│   │   └── contracts.py                    # API contract management
│   │
│   ├── tools/
│   │   ├── base.py                         # ToolDefinition, ToolResult
│   │   ├── core/                           # FileRead, FileWrite, FileEdit, Bash, Glob, Grep, Web*
│   │   ├── pheromone/                      # Sense, DepositKnowledge, DepositADR, DepositWarning
│   │   ├── workspace/                      # AcquireLease, ReleaseLease, GetContext, RunTests
│   │   └── registry.py                     # Tool registration + type profiles (§7.3)
│   │
│   ├── stores/
│   │   ├── base.py                         # PheromoneStore ABC
│   │   ├── memory.py                       # InMemoryStore
│   │   └── redis_store.py                  # RedisStore
│   │
│   ├── resilience/
│   │   ├── circuit_breaker.py
│   │   ├── health.py                       # Heartbeat + ring buffers
│   │   ├── recovery.py                     # Retry + checkpoint resume
│   │   └── permissions.py                  # 3-way permission + denial tracking (§24)
│   │
│   ├── security/
│   │   ├── auth.py, validation.py, integrity.py
│   │
│   ├── observability/
│   │   ├── logging.py                      # Structured JSON + ring buffers
│   │   ├── metrics.py                      # Prometheus exports
│   │   └── replay.py                       # Colony execution replay
│   │
│   ├── compat/
│   │   └── claude_md.py                    # CLAUDE.md loader (§26)
│   │
│   ├── integrations/
│   │   ├── mcp_server.py                   # MCP compatibility (§27)
│   │   ├── openclaw_skill/
│   │   ├── langgraph_node.py
│   │   └── rest_client.py
│   │
│   └── api/
│       └── server.py                       # FastAPI REST + WebSocket
│
├── viz/
│   └── dashboard.py                        # Streamlit dashboard
│
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── e2e/
│   └── benchmarks/
│
├── templates/                              # Colony YAML templates
├── examples/
│   ├── 01_basic_colony.py
│   ├── 02_software_dev.py
│   ├── 03_complex_saas.py
│   ├── 04_research_team.py
│   ├── 05_learning_colony.py
│   ├── 06_adaptive_composition.py
│   └── 07_federation.py
│
└── docs/
    ├── architecture.md                     # This document
    ├── algorithms.md
    ├── api_reference.md
    └── research/
```

---

## 30. PUBLIC API REFERENCE

```python
from pheromone import Colony, Agent, Budget, Strategy
from pheromone.templates import SoftwareDevTeam

# Simple usage
colony = Colony("my-project", template=SoftwareDevTeam())
result = await colony.solve("Build a weather API with tests and docs")

# Complex usage with PRD
colony = Colony("saas-build", composition="adaptive", budget=Budget(max_dollars=5.0))
result = await colony.solve(
    goal="Build a project management SaaS",
    specification=open("prd.md").read(),
    strategy=Strategy(
        decomposition="hierarchical",
        require_quorum=True,
        review=ReviewConfig(require_review=True, max_revisions=MAX_REVISIONS),
        integration=IntegrationConfig(verify_features=True),
        approval=ApprovalConfig(require_approval_for=["external_api"]),
        min_coverage=0.90,
    )
)

# Inspect results
result.output                    # Final assembled deliverable
result.task_graph.summary()      # Task tree with statuses
result.specification_coverage    # {covered: set, uncovered: set, pct: float}
result.quality_report            # Review scores, test results
result.integration_report        # Cross-module verification
result.cost_summary              # Per-agent and total
result.pheromone_trail           # Full audit trail
result.workspace.file_tree       # All files produced
result.learning_summary          # Meta-parameter changes for next run
```

---

## 31. BENCHMARKING STRATEGY

### Prong 1 — Beat Established Benchmarks

| Benchmark | Current SOTA | Pheromone Advantage | Target |
|-----------|-------------|-------------------|--------|
| SWE-bench Verified | 76.1% (Verdent) | Knowledge sharing + review cycles | 80%+ |
| GAIA Level 3 | 61% (Action Agent) | Parallel tool use + shared knowledge | 65%+ |
| DPAI Arena | New (JetBrains) | Full lifecycle coverage | Top 3 |
| CUB | 10.4% | Cross-agent learning + workspace | 15%+ |
| The Agent Company | ~25% | Multi-agent coordination | 35%+ |

### Prong 2 — PheromBench (New Standard)

5 categories, 10 tasks each, 5 baselines, 10 runs per config. Total: 2,500 runs.
Categories: Parallel Efficiency, Knowledge Transfer, Iterative Refinement, Fault Recovery, Colony Learning.
Statistical rigor: mean ± std, paired t-tests, p < 0.05.

---

## 32. 12-WEEK BUILD ROADMAP

### Phase 1: Foundation (Week 1) — Working prototype

| Day | Deliverable |
|-----|-------------|
| 1 | Data models + InMemoryStore + MAX-MIN + constants + 20 tests |
| 2 | AgentProxy + ReAct loop + thresholds + sensing + embeddings + 15 tests |
| 3 | Hierarchical decomposer + DAG validation + Workspace + FileEditor + leasing + 15 tests |
| 4 | StigmergicAllocator (ACO + Lévy) + tool definitions + tool orchestrator + 15 tests |
| 5 | ExecutionEngine + knowledge sharing + codebase indexer + basic review + 15 tests |
| 6 | Colony integration + CLAUDE.md loader + evolution (basic) + prompts + Streamlit + fix all |
| 7 | README + 2 examples + structured logging + GitHub + HuggingFace Spaces |

### Phase 2: Robustness (Week 2-4)
Quorum Sensing, full workspace conventions, complete review loop, ADR system, integration verification, circuit breaker, Redis store, budget manager, spec tracking, 8 templates, human-in-the-loop, comprehensive tests.

### Phase 3: Intelligence (Week 5-7)
Stigmergic RL meta-learner, adaptive composition, pheromone compaction (9-section), knowledge conflict resolution, colony learning benchmarks, tool pheromones, checkpoint pheromones.

### Phase 4: Ecosystem (Week 8-10)
FastAPI server, WebSocket stream, MCP server, OpenClaw skill, LangGraph adapter, Docker, security, federation, schema versioning, pheromone scoping.

### Phase 5: Publication (Week 11-12)
PheromBench, established benchmark runs, arXiv paper, LinkedIn series, HuggingFace demo, GitHub launch, PyPI release.

---

## 33. RESEARCH PLAN

**Paper 1:** "Stigmergic Coordination for LLM-Based Multi-Agent Systems" — Core: ACO + Response Thresholds + Stigmergic RL. Empirical: PheromBench + SWE-bench. Target: NeurIPS 2026 Workshop / AAMAS 2027.

**Paper 2:** "PheromBench: A Benchmark for Multi-Agent Coordination Quality" — Benchmark spec + baselines. Target: EMNLP 2027 / arXiv.

**Blog Series:** (1) Why stigmergy for AI agents (2) No orchestrator needed (3) 16 concepts from 10 fields (4) Benchmark results.

---

## 34. IMPLEMENTATION RISK REGISTER (26 Risks)

| # | Risk | Sev | Likelihood | Mitigation | Phase |
|---|------|-----|-----------|-----------|-------|
| R1 | API rate limits under parallel calls | HIGH | HIGH | Shared rate limiter, queue, backoff | 1 |
| R2 | File edit conflicts between agents | HIGH | HIGH | File leasing + content hash | 1 |
| R3 | Pheromone env too large to sense | MED | MED | Compaction at 50/type + budget caps | 1 |
| R4 | ReAct loop stuck (infinite cycles) | HIGH | MED | Max turns (25) + circuit breaker | 1 |
| R5 | Wrong decomposition granularity | MED | HIGH | Quorum validation + re-decompose | 2 |
| R6 | Incorrect knowledge pheromones | MED | MED | Trust scoring + quorum + conflicts | 2 |
| R7 | Review loops add too much latency | MED | LOW | Max 3 revisions + timeout 120s | 2 |
| R8 | ADR conflicts between agents | MED | MED | Quorum + first-deposited wins | 2 |
| R9 | Stigmergic RL diverges | LOW | MED | LR=0.01 + clamping + fallback | 3 |
| R10 | Adaptive composition wrong agents | MED | MED | Template matching + fallback | 3 |
| R11 | Token costs explode | HIGH | MED | Budget cap + cost-aware allocation + dedup | 1 |
| R12 | Integration tests fail post-completion | MED | HIGH | Integration Verification Layer | 2 |
| R13 | Colony startup too slow | LOW | MED | Lazy init + agent pool | 1 |
| R14 | Embedding latency per deposit/sense | MED | HIGH | Batch + cache + lightweight model | 1 |
| R15 | Redis unavailable | MED | LOW | Fallback to InMemory + warning | 2 |
| R16 | Agents ignore conventions | MED | HIGH | Convention check before result accept | 2 |
| R17 | PheromBench not significant | LOW | MED | 10 runs + paired t-tests + CI | 5 |
| R18 | Workspace context too large | MED | MED | File tree summarization + 5K cap | 1 |
| R19 | Over-specialization | LOW | LOW | Lévy jumps + idle drift + θ_min | 1 |
| R20 | Quorum voting too slow | MED | MED | 30s timeout + async voting | 2 |
| R21 | Federation inconsistency | LOW | LOW | Decay on boundary + conflict protocol | 4 |
| R22 | Schema migration breaks store | MED | LOW | Version field + lazy migration | 4 |
| R23 | Benchmark eval too expensive | MED | HIGH | Haiku baselines + cache + budget | 5 |
| R24 | Security vulnerabilities | MED | MED | SHA-256 + isolation + rate limit | 4 |
| R25 | Context fills before task done | HIGH | MED | Per-turn tracking + compact at 90% | 1 |
| R26 | Malformed LLM tool calls | MED | MED | Pydantic validation + error to LLM | 1 |

---

## 35. QUALITY STANDARDS (Per-Component)

| Component | Quality Bar | Unacceptable |
|-----------|------------|-------------|
| Data Models | Every field typed+documented. Pydantic validation on all inputs. | Untyped field. Model accepts invalid data. |
| Pheromone Store | Atomic ops. No data loss on crash (Redis). <10ms read p99. | Lost writes. Corrupt state. >100ms p99. |
| Agent ReAct Loop | Terminates in finite time for any input. Partial output on timeout. | Infinite loop. Crash on malformed LLM. Silent failure. |
| Allocator | Converges within 5 rounds. Cost within 2× of optimal. | Starvation. Thrashing. |
| Decomposer | Valid DAG for any well-formed goal. Handles 1-50 subtasks. | Cyclic graph. >60s decomposition. |
| Workspace | No file corruption. Leasing prevents conflicts. Convention check <500ms. | Corrupted files. Lease deadlock. |
| Review Loop | Measurable quality improvement. Completes within MAX_REVISIONS. | Quality regression. Infinite review. |
| Evolution | Quality improves over 5+ colony runs on same task family. | Quality degrades. Parameters diverge. |
| Sensing | Returns relevant pheromones within budget. <100ms for 500 pheromones. | Irrelevant top results. Budget overflow. >500ms. |
| Budget Manager | Never exceeds budget. Graceful degradation at 80%+. | Budget exceeded >10%. Crash on exhaustion. |
| Error Handling | Every error type has handler. No unhandled exceptions. | Unhandled exception. Silent error. |
| Tests | >80% line coverage core. All critical paths have integration tests. | <60% coverage. Flaky tests. |
| Documentation | pip install + run in <5 min. Architecture doc matches code. | Broken install. Outdated docs. |

---

## 36. GAP COVERAGE MATRIX (FINAL)

| # | Gap | Category | Status | Section |
|---|-----|----------|--------|---------|
| 1 | No convergence model | Critical | FIXED | §5.2 |
| 2 | No fault tolerance | Critical | FIXED | §16 |
| 3 | No concurrency control | Critical | FIXED | §17 |
| 4 | No pheromone quality control | Critical | FIXED | §15 |
| 5 | No context window management | Critical | FIXED | §19 |
| 6 | No cost management | Critical | FIXED | §18 |
| 7 | No deadlock/livelock detection | Important | FIXED | §16 |
| 8 | No formal comparison | Important | FIXED | §31 |
| 9 | No security model | Important | FIXED | §20 |
| 10 | No observability | Important | FIXED | §21 |
| 11 | No edge case handling | Important | FIXED | §11, §16 |
| 12 | No integration protocol | Design | FIXED | §27 |
| 13 | No deployment architecture | Design | FIXED | §28 |
| 14 | No UX design | Design | FIXED | §30 |
| 15 | No tool integration | Infra | FIXED | §22 |
| 16 | No long-running tasks | Infra | FIXED | §23 |
| 17 | No human-in-the-loop | Infra | FIXED | §24 |
| 18 | No multi-colony | Infra | FIXED | §25 |
| 19 | No pheromone privacy | Infra | FIXED | §5.7 |
| 20 | No contradiction resolution | Intel | FIXED | §15 |
| 21 | No schema versioning | Infra | FIXED | §4.2 |
| 22 | No hierarchical decomposition | Enterprise | FIXED | §8 |
| 23 | No shared codebase awareness | Enterprise | FIXED | §9 |
| 24 | No iterative refinement | Enterprise | FIXED | §11.2 |
| 25 | No cross-cutting consistency | Enterprise | FIXED | §12 |
| 26 | No integration verification | Enterprise | FIXED | §13 |

**26 gaps identified. 26 gaps resolved. Zero remaining.**

---

**This document is the single source of truth for building Pheromone.**

**16 theoretical concepts** from 10 academic fields. **5 novel research contributions.** **14 Claude Code intelligence integrations.** **26 architectural gaps** identified and resolved. **26 implementation risks** registered with mitigations. **13 quality standards** with measurable bars. **30+ battle-tested constants** from production systems. **12-week roadmap** with day-by-day Week 1 plan.

**No code is written that isn't specified here. Ready to build.**

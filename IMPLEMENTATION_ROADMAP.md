# PHEROMONE — Implementation Roadmap

**Purpose:** Exact file-by-file build order for Week 1, plus weekly milestones for Weeks 2-12.
**Goal:** `colony.solve("Build a weather API")` working E2E with MockLLM by Day 5. Real LLM by Day 7.
**Last Updated:** April 8, 2026

---

## CRITICAL PATH ANALYSIS

The dependency chain to a working `colony.solve()`:

```
errors.py → constants.py → models/* → stores/memory.py → llm/* → environment/* → workspace/* → agents/* → tools/* → engine/* → colony.py → cli/main.py
```

Every file depends on something to its left. Nothing to its right. Build left to right.

---

## DAY 1: Foundation Models + Store (Target: 35 tests green)

**Theme:** All data models compile. InMemoryStore works. Constants exist. Error hierarchy exists.

### Morning (Files 1-5)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 1 | `pheromone/errors.py` | ~150 | None | Full error taxonomy (Gap 12). PheromoneError base → 6 branches, 25 subclasses. severity/retryable/user_hint fields. |
| 2 | `pheromone/constants.py` | ~80 | None | All 50+ constants from architecture §3. Copy verbatim. |
| 3 | `pheromone/models/__init__.py` | ~5 | None | Empty init. |
| 4 | `pheromone/models/pheromones.py` | ~200 | errors, constants | Pheromone, PheromoneType (8 types), PheromoneScope (4 scopes), SenseResult (from cross-spec audit), pheromone validation rules (§5.8). |
| 5 | `pheromone/models/tasks.py` | ~200 | constants | TaskNode, TaskLevel, TaskStatus (12 states), ReviewRecord, HierarchicalTaskGraph (with get_available_leaves, get_execution_waves via Kahn's, validate_dag), SpecificationModel, Requirement. |

### Afternoon (Files 6-11)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 6 | `pheromone/models/config.py` | ~350 | constants | ColonyConfig + 8 sub-models (Gap 3 §2): BudgetConfig, LLMConfig, AgentConfig, Strategy, ReviewConfig, QuorumConfig, IntegrationConfig, ApprovalConfig, StoreConfig, WorkspaceConfig, EmbeddingConfig, LoggingConfig, OutputMode, LiveBudget. |
| 7 | `pheromone/models/execution.py` | ~150 | models/config | LLMUsage, TaskOutput, TaskExecutionRecord, ExecutionTracker (Gap 2 + cross-spec audit). |
| 8 | `pheromone/models/results.py` | ~250 | models/config, models/execution | ColonyResult, ColonyOutput (discriminated union), WorkspaceOutput (with get_tree + read_file), TextOutput, HybridOutput, TaskSummary, CostSummary, PartialOutput. Import OutputMode from config.py. |
| 9 | `pheromone/stores/__init__.py` | ~5 | None | Empty. |
| 10 | `pheromone/stores/base.py` | ~40 | models/pheromones | PheromoneStore ABC: deposit, get, sense, update_strength, bulk_decay, count, get_audit_log. |
| 11 | `pheromone/stores/memory.py` | ~200 | stores/base, models/pheromones, constants | InMemoryStore: dict-backed, atomic ops, MAX-MIN enforcement on deposit/update, bulk_decay with evaporation, basic sense (keyword or embedding cosine similarity), audit log. Thread-safe via asyncio.Lock. |

### Tests (Day 1)

| File | Tests | API Calls |
|------|-------|-----------|
| `tests/unit/models/test_pheromones.py` | 8: Pheromone creation, validation rules per type, effective_strength, SenseResult helpers, scope enum, embedding optional | 0 |
| `tests/unit/models/test_tasks.py` | 8: TaskNode states, HierarchicalTaskGraph DAG validation, get_execution_waves (linear + parallel + diamond), get_available_leaves with deps, validate_dag cycle detection | 0 |
| `tests/unit/models/test_config.py` | 6: ColonyConfig defaults, LiveBudget is_exhausted/should_warn, AgentConfig model resolution, Strategy composition modes, OutputMode enum | 0 |
| `tests/unit/models/test_execution.py` | 4: ExecutionTracker start/complete/record_llm_call, cost aggregation, duration, phase_costs | 0 |
| `tests/unit/models/test_results.py` | 4: ColonyOutput discriminator roundtrip, WorkspaceOutput.get_tree (nested), TextOutput.full_text, ColonyResult summary | 0 |
| `tests/unit/stores/test_memory.py` | 6: deposit+get, MAX-MIN clamping, bulk_decay+evaporation, count by type, sense keyword match, audit log | 0 |

**Day 1 Total: 11 source files, 36 tests, 0 API calls.**

**First test that passes:** `test_pheromone_creation` — create a Pheromone with valid fields, assert all properties.

**Milestone check:** `python -m pytest tests/unit/models/ tests/unit/stores/ -v` → 36 green.

---

## DAY 2: LLM Client Layer (Target: 36 + 36 = 72 tests green)

**Theme:** Full LLM abstraction. MockLLM works. Retry, middleware, capabilities, parsers all functional.

### Morning (Files 12-18)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 12 | `pheromone/llm/__init__.py` | ~5 | None | Empty. |
| 13 | `pheromone/llm/models.py` | ~150 | None | LLMRequest, LLMResponse, LLMToolCall, LLMMessage, LLMUsage. Pure data models — no provider deps. |
| 14 | `pheromone/llm/retry.py` | ~100 | errors, constants | RetryPolicy, is_retryable(), exponential_backoff(). Maps HTTP codes to retry decisions. |
| 15 | `pheromone/llm/capabilities.py` | ~150 | None | MODEL_REGISTRY dict (15+ models), ModelCapabilities dataclass (max_tokens, supports_tools, supports_vision, cost_per_1k_input/output, provider). get_capabilities(model_string). |
| 16 | `pheromone/llm/parsers.py` | ~100 | None | JSONTextParser (extract JSON from markdown fences or raw), XMLTextParser (extract tagged sections). Both with fallback strategies. |
| 17 | `pheromone/llm/client.py` | ~200 | llm/models, llm/retry, errors | BaseLLMClient ABC (create, create_with_cost_check). LiteLLMClient implementation (wraps litellm.acompletion, parses response into LLMResponse, handles tool calls, applies retry). |
| 18 | `pheromone/llm/mock.py` | ~150 | llm/client, llm/models | MockLLM: scripted responses, tool call simulation, latency simulation, call recording, assertion helpers. MockResponse builder. This is THE test workhorse. |

### Afternoon (Files 19-21)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 19 | `pheromone/llm/middleware.py` | ~200 | llm/client, llm/capabilities | LLMMiddleware ABC. CapabilityAwareMiddleware (auto-adjusts request params per model limits). LoggingMiddleware. build_middleware_stack(base, middlewares, auto_capability_aware). Accepts type, instance, or Callable. |
| 20 | `pheromone/llm/cache.py` | ~100 | llm/middleware | CachingMiddleware: hash-based LRU cache, TTL expiration, cache hit/miss logging. |
| 21 | `pheromone/llm/fallback.py` | ~80 | llm/client, errors | FallbackLLMClient: tries each client in order, catches retryable errors, falls through to next. |

### Tests (Day 2)

| File | Tests | API Calls |
|------|-------|-----------|
| `tests/unit/llm/test_models.py` | 4: LLMRequest/Response creation, LLMUsage cost calc, tool call parsing, message serialization | 0 |
| `tests/unit/llm/test_retry.py` | 4: is_retryable by error type, backoff calculation, max retries respected, non-retryable passes through | 0 |
| `tests/unit/llm/test_capabilities.py` | 4: registry lookup, unknown model returns defaults, cost calculation, supports_tools check | 0 |
| `tests/unit/llm/test_parsers.py` | 4: JSON from fences, JSON raw, XML extraction, malformed graceful failure | 0 |
| `tests/unit/llm/test_mock.py` | 6: scripted responses, tool call simulation, call recording, assertion helpers, latency simulation, empty queue raises | 0 |
| `tests/unit/llm/test_middleware.py` | 6: capability-aware adjusts tokens, logging middleware logs, build_middleware_stack with types/instances/callables, chain ordering, capability + cache stacked | 0 |
| `tests/unit/llm/test_cache.py` | 4: cache hit, cache miss, TTL expiration, different requests different keys | 0 |
| `tests/unit/llm/test_fallback.py` | 4: primary succeeds (no fallback), primary fails → fallback succeeds, all fail → raises last error, non-retryable skips fallback | 0 |

**Day 2 Total: 10 source files, 36 tests, 0 API calls.**

**Cumulative: 21 files, 72 tests.**

---

## DAY 3: Environment + Embeddings + Workspace (Target: 72 + 30 = 102 tests green)

**Theme:** PheromoneEnvironment fully functional with sensing. Workspace with file ops + leasing. Embeddings with NullEmbedder for Phase 1.

### Morning (Files 22-27)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 22 | `pheromone/environment/__init__.py` | ~5 | None | Empty. |
| 23 | `pheromone/environment/embeddings.py` | ~250 | errors, models/config | BaseEmbedder ABC, NullEmbedder (returns zeros — Phase 1 default), SentenceTransformerEmbedder (lazy load, optional dep), APIEmbedder (via litellm), EmbeddingCache (thread-safe LRU), EmbeddingService (from_config factory, embed_text, embed_batch, cosine_similarity). |
| 24 | `pheromone/environment/environment.py` | ~300 | stores/base, environment/embeddings, models/pheromones, constants | PheromoneEnvironment: deposit (validate + embed + hash + MAX-MIN clamp + audit), sense (extended signature with type_filter/limit/token_budget/scope/min_strength/tags → SenseResult), reinforce, decay_cycle, count, get_audit_log. Scope enforcement. Information Foraging scent formula. |
| 25 | `pheromone/workspace/__init__.py` | ~5 | None | Empty. |
| 26 | `pheromone/workspace/leasing.py` | ~100 | models/pheromones, constants | WorkspaceLeaseManager: acquire (returns FileLease or None), release, force_release_expired, release_all_leases(agent_id). Dict-backed, asyncio.Lock. |
| 27 | `pheromone/workspace/editor.py` | ~120 | errors | FileEditor: edit_file (str_replace with conflict detection via content hash), write_file, read_file. Quote normalization fallback. EditResult model. |

### Afternoon (Files 28-29)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 28 | `pheromone/workspace/manager.py` | ~200 | workspace/leasing, workspace/editor, models/pheromones | WorkspaceManager: write_file, read_file, edit_file, get_project_context (file tree + conventions), check_conventions (stub for Phase 2), update_api_contract, release_all_leases. FileInfo tracking on every write. |
| 29 | `pheromone/stores/result_store.py` | ~80 | models/results | ResultStore: save (JSON), load, list_runs. Directory-based persistence under .pheromone/results/. |

### Tests (Day 3)

| File | Tests | API Calls |
|------|-------|-----------|
| `tests/unit/environment/test_embeddings.py` | 6: NullEmbedder returns zeros, EmbeddingCache hit/miss/thread-safe, cosine_similarity correct, from_config factory (null provider) | 0 |
| `tests/unit/environment/test_environment.py` | 10: deposit validates fields, deposit clamps MAX-MIN, sense with type_filter, sense with token_budget, reinforce increases strength, decay_cycle evaporates weak, scope enforcement (private not visible), count by type, audit log records, Information Foraging scent ranking | 0 |
| `tests/unit/workspace/test_leasing.py` | 4: acquire/release, conflict (two agents same file), TTL expiration, release_all_leases | 0 |
| `tests/unit/workspace/test_editor.py` | 4: edit exact match, edit with hash conflict, edit string not found, quote normalization fallback | 0 |
| `tests/unit/workspace/test_manager.py` | 4: write+read roundtrip, get_project_context returns file tree, FileInfo updated on write, edit_file delegates to editor | 0 |
| `tests/unit/stores/test_result_store.py` | 2: save+load roundtrip, list_runs sorted | 0 |

**Day 3 Total: 8 source files, 30 tests, 0 API calls.**

**Cumulative: 29 files, 102 tests.**

---

## DAY 4: Agents + Tools + Decomposer + Allocator (Target: 102 + 30 = 132 tests green)

**Theme:** Agents can execute tasks via ReAct loop with MockLLM. Decomposer produces task graphs. Allocator assigns tasks via ACO.

### Morning (Files 30-37)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 30 | `pheromone/tools/__init__.py` | ~5 | None | Empty. |
| 31 | `pheromone/tools/base.py` | ~80 | None | ToolDefinition (name, description, input_schema, is_read_only, requires_lease, timeout), ToolResult (output, is_error, error), BaseTool ABC with execute(input, workspace, agent_id). |
| 32 | `pheromone/tools/registry.py` | ~100 | tools/base | TOOL_PROFILES dict mapping agent_type → list[tool_name]. get_tools_for_agent(agent_type). Tool registration. |
| 33 | `pheromone/tools/core/` | ~300 | tools/base, workspace | FileRead, FileWrite, FileEdit, BashTool (subprocess with timeout), GlobTool, GrepTool. Each implements BaseTool. FileEdit uses workspace.editor. BashTool has MAX_RESULT_SIZE_CHARS cap. |
| 34 | `pheromone/tools/pheromone/` | ~150 | tools/base, environment | SenseTool (wraps environment.sense), DepositKnowledge, DepositADR, DepositWarning (each validates content dict, deposits typed pheromone). |
| 35 | `pheromone/agents/__init__.py` | ~5 | None | Empty. |
| 36 | `pheromone/agents/thresholds.py` | ~80 | constants | ResponseThresholdModel: per-agent per-skill thresholds. update_on_success/failure/idle. eligibility_check(task, agent). |
| 37 | `pheromone/agents/tool_orchestrator.py` | ~120 | tools/base, workspace/leasing, constants | ToolOrchestrator: execute_tools (read-parallel via asyncio.gather, write-serial with lease acquire/release). Result size capping. Timeout per tool. |

### Afternoon (Files 38-42)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 38 | `pheromone/agents/prompt_builder.py` | ~150 | models/config, models/tasks, models/pheromones | AgentPromptBuilder.build(): static sections (identity, role, colony rules, tool usage, quality, safety, output efficiency) + dynamic boundary + task context + workspace context + ADRs + conventions. |
| 39 | `pheromone/agents/react_loop.py` | ~250 | agents/tool_orchestrator, agents/prompt_builder, llm/client, models/execution, environment | AgentReActLoop.execute(): build initial context → LLM loop (max_turns) → parse tool calls → execute via orchestrator → auto-deposit codebase index → check termination → context budget check. Returns TaskOutput. Implements checkpoint hooks. 6 extraction methods for crash recovery. |
| 40 | `pheromone/agents/proxy.py` | ~100 | agents/react_loop, agents/thresholds, models/config | AgentProxy: wraps config + react_loop + thresholds. execute_task(task, sense_result) → TaskOutput. Heartbeat deposit. Trust tracking (Beta-Binomial). |
| 41 | `pheromone/engine/decomposer.py` | ~200 | llm/client, models/tasks, models/pheromones | HierarchicalDecomposer: goal → LLM prompt → parse response → build HierarchicalTaskGraph → validate DAG via Kahn's. Handles simple goals (flat tasks) and complex goals (epic→feature→task). Specification parsing if PRD provided. |
| 42 | `pheromone/engine/allocator.py` | ~200 | models/tasks, models/pheromones, agents/thresholds, constants | StigmergicAllocator: allocate_round(available_tasks, agents, environment) → dict[task_id, agent_id]. ACO formula (§10.1). Response Threshold pre-filter (§10.2). Lévy Flight exploration (§10.3). Optimistic locking (§10.4). |

### Tests (Day 4)

| File | Tests | API Calls |
|------|-------|-----------|
| `tests/unit/tools/test_core.py` | 4: FileRead/Write roundtrip, FileEdit str_replace, BashTool with timeout, GrepTool result cap | 0 |
| `tests/unit/tools/test_pheromone_tools.py` | 3: SenseTool queries env, DepositKnowledge validates + deposits, DepositWarning deposits WARNING type | 0 |
| `tests/unit/agents/test_thresholds.py` | 4: initial values, success decreases, failure increases, idle drift, eligibility gate | 0 |
| `tests/unit/agents/test_tool_orchestrator.py` | 3: reads parallel, writes serial, lease failure returns error | 0 |
| `tests/unit/agents/test_react_loop.py` | 6: single-turn (no tools) returns text, multi-turn with tool calls, max_turns exhaustion returns incomplete, context budget triggers compaction (stub), partial output on failure, extraction methods return accumulated state | 0 |
| `tests/unit/engine/test_decomposer.py` | 5: simple goal → flat tasks, complex goal → hierarchical, DAG validated, spec parsing extracts requirements, malformed LLM response → re-prompt | 0 |
| `tests/unit/engine/test_allocator.py` | 5: ACO formula selects highest attraction, threshold gate filters ineligible, Lévy exploration occasionally picks non-optimal, optimistic locking resolves conflicts, empty available → empty claims | 0 |

**Day 4 Total: 13 source files, 30 tests, 0 API calls.**

**Cumulative: 42 files, 132 tests.**

---

## DAY 5: Engine + Colony + First E2E (Target: 132 + 30 = 162 tests green, E2E with MockLLM passes)

**Theme:** ExecutionEngine main loop works. Colony wires everything. `colony.solve()` runs E2E with MockLLM.

### Morning (Files 43-50)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 43 | `pheromone/engine/__init__.py` | ~5 | None | Empty. |
| 44 | `pheromone/engine/lifecycle.py` | ~100 | errors | EngineState enum (IDLE, RUNNING, PAUSED, CANCELLING, TERMINATED). TRANSITIONS dict. IllegalStateTransition error. transition() with validation. |
| 45 | `pheromone/engine/execution.py` | ~400 | engine/lifecycle, engine/decomposer, engine/allocator, models/execution, models/results, agents/proxy, environment, workspace | ExecutionEngine: run() main loop (Phase 0-6 from architecture §11.1). Wave tracking. Cooperative pause/resume via asyncio.Event + checkpoint(). Cancel with drain. Tracker integration. Event emission via callback. |
| 46 | `pheromone/engine/assembler.py` | ~250 | models/results, models/execution, models/config, environment | OutputAssembler: 6-step pipeline. Detect output mode (workspace/text/hybrid with 200-word threshold). Collect task summaries from tracker. Build workspace output (entry point detection, nested file tree). Build text output (topological ordering). Collect warnings from env. Collect partial outputs. Cost summary with real token breakdown. Executive summary (optional, via LLM). |
| 47 | `pheromone/engine/reporters.py` | ~150 | models/results | TerminalReporter (Rich-formatted), MarkdownReporter. isinstance() checks for output types. |
| 48 | `pheromone/config/__init__.py` | ~5 | None | Empty. |
| 49 | `pheromone/config/loader.py` | ~150 | models/config | load_config(): discovery order (explicit → .pheromone.yaml → pheromone.yaml → pyproject.toml → defaults). YAML/TOML parsing. Env var mapping (PHEROMONE_* prefix). Deep merge. .env auto-load via python-dotenv. |
| 50 | `pheromone/config/validator.py` | ~100 | models/config, errors | validate_config(): fail-fast. Collects all issues. Checks: API keys per model, workspace writable, budget > 0, agent names unique, valid types, valid template, store reachable, optional dep availability. |

### Afternoon (Files 51-55)

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 51 | `pheromone/colony.py` | ~300 | models/config, config/loader, config/validator, all build_* deps | Colony class. __init__ 11-step pipeline (Gap 3 §5). solve(). register(). shutdown(). All _build_* methods. |
| 52 | `pheromone/__init__.py` | ~30 | colony, models | Public API exports: Colony, ColonyConfig, AgentConfig, Strategy, ColonyResult, Pheromone, PheromoneType. __version__. |
| 53 | `pheromone/py.typed` | 0 | None | PEP 561 marker (empty file). |
| 54 | `pheromone/ui/__init__.py` | ~5 | None | Empty. |
| 55 | `pheromone/ui/events.py` | ~100 | None | ColonyEvent dataclass, EventType string enum (40+ values). Pure data — no subscribers yet. |

### Tests (Day 5)

| File | Tests | API Calls |
|------|-------|-----------|
| `tests/unit/engine/test_lifecycle.py` | 4: valid transitions, illegal transition raises, all states reachable, terminal state blocks further | 0 |
| `tests/unit/engine/test_execution.py` | 6: run with MockLLM produces result, pause/resume works, cancel drains tasks, wave tracking increments, empty allocation sleeps, budget exhausted stops gracefully | 0 |
| `tests/unit/engine/test_assembler.py` | 6: detect mode (workspace/text/hybrid/empty), task summaries from tracker, workspace output with file tree, text output topological order, cost summary aggregation, partial output collection | 0 |
| `tests/unit/config/test_loader.py` | 4: YAML load, env var override, deep merge, missing file uses defaults | 0 |
| `tests/unit/config/test_validator.py` | 4: missing API key, duplicate agents, valid config passes, all issues collected | 0 |
| `tests/unit/test_colony_init.py` | 4: zero-config with MockLLM, template resolution, workspace creation, budget LiveBudget tracking | 0 |
| **`tests/e2e/test_basic_solve.py`** | **2: colony.solve("Build a hello world script") with MockLLM → ColonyResult with files; colony.solve("Write a haiku") with MockLLM → TextOutput** | **0** |

**Day 5 Total: 13 source files, 30 tests (including 2 E2E), 0 API calls.**

**Cumulative: 55 files, 162 tests. E2E PASSES WITH MOCKLLM.**

**Day 5 Milestone:** This is the inflection point. `colony.solve()` works end-to-end. Everything after this is enhancement, not foundation.

---

## DAY 6: Test Infra + Templates + Agents + Polish (Target: 162 + 20 = 182 tests green)

**Theme:** Test infrastructure (conftest, factories, helpers). Agent templates. CLAUDE.md loader. Prompt templates.

### Files

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 56 | `tests/conftest.py` | ~150 | All models, MockLLM, InMemoryStore | 12 fixtures: mock_llm, in_memory_store, environment, workspace (tmp_path), agent_config, colony_config, tracker, task_graph (3 tasks diamond), sense_result, budget, colony (full wired with MockLLM). |
| 57 | `tests/factories.py` | ~100 | All models | 8 factory functions: make_pheromone, make_task, make_agent_config, make_colony_config, make_llm_request, make_llm_response, make_task_output, make_execution_record. Sensible defaults, all fields overridable. |
| 58 | `tests/helpers.py` | ~80 | factories, environment | populate_environment (deposit N pheromones of mixed types), run_concurrent (helper for parallel test execution), assert_valid_colony_result, assert_dag_valid. |
| 59 | `pheromone/agents/templates.py` | ~200 | models/config | 8 built-in templates: SoftwareDevTeam (architect+2 devs+reviewer+tester), ResearchTeam, ContentTeam, DataScienceTeam, ConsultingTeam, LegalTeam, MarketingTeam, GeneralPurpose. get_template(name). |
| 60 | `pheromone/compat/__init__.py` | ~5 | None | Empty. |
| 61 | `pheromone/compat/claude_md.py` | ~60 | None | load_claude_md(path) → list[str] conventions. Parses CLAUDE.md for project directives. |
| 62 | `pheromone/agents/composer.py` | ~120 | llm/client, models/config, agents/templates | GoalAnalyzer: analyze goal → identify required skills → select/spawn agents from templates. For adaptive composition mode. |

### Tests (Day 6)

| File | Tests | API Calls |
|------|-------|-----------|
| `tests/unit/agents/test_templates.py` | 4: software_dev has 5 agents, unknown template raises, all templates produce valid AgentConfigs, template agents have correct models | 0 |
| `tests/unit/agents/test_composer.py` | 4: goal analysis extracts skills, adaptive creates appropriate agents, simple goal → GeneralPurpose, complex goal → specialized team | 0 |
| `tests/unit/compat/test_claude_md.py` | 2: parse valid CLAUDE.md, missing file returns empty | 0 |
| `tests/integration/test_colony_full.py` | 6: zero-config solve, template solve, adaptive solve, re-entrant solve (two solves), budget exhaustion mid-run, 3-agent parallel execution | 0 |
| Additional coverage tests | 4: various edge cases from existing modules | 0 |

**Day 6 Total: 7 source files, 20 tests, 0 API calls.**

**Cumulative: 62 files, 182 tests.**

---

## DAY 7: CLI Entry Point + Real LLM Test + README + GitHub Push

**Theme:** `pheromone solve "Build a weather API"` works from command line. Real LLM integration tested manually. Published to GitHub.

### Files

| # | File | Lines | Deps | What It Does |
|---|------|-------|------|-------------|
| 63 | `pheromone/cli/__init__.py` | ~5 | None | Empty. |
| 64 | `pheromone/cli/main.py` | ~150 | typer, rich, colony | Typer app. Commands: `solve` (main), `init` (create .pheromone.yaml), `status` (show last result), `version`. `solve` creates Colony, runs colony.solve(), prints TerminalReporter output. |
| 65 | `pyproject.toml` | ~240 | None | Full build config from Gap 11. Entry point: pheromone = pheromone.cli.main:app. All deps, extras, tool configs. |
| 66 | `README.md` | ~300 | None | Project overview, install, quick start (3 lines of code), architecture diagram (Mermaid), features list, comparison table, contributing, license. |
| 67 | `LICENSE` | ~20 | None | MIT. |
| 68 | `examples/01_basic_colony.py` | ~30 | Colony | Minimal: Colony → solve → print result. |
| 69 | `examples/02_software_dev.py` | ~40 | Colony, templates | Template-based: Colony with SoftwareDevTeam → solve complex goal. |
| 70 | `.github/workflows/ci.yml` | ~60 | None | GitHub Actions: Python 3.11+3.12, pip install .[dev], pytest with coverage, ruff lint, mypy. |

### Manual Testing (Day 7)

```bash
# Install locally
pip install -e ".[dev]"

# Run full test suite
pytest -v --cov=pheromone --cov-report=term-missing

# Test CLI
pheromone version
pheromone init  # Creates .pheromone.yaml
pheromone solve "Create a Python hello world script"  # MockLLM mode

# Test with real LLM (manual, not CI)
export ANTHROPIC_API_KEY=sk-ant-...
pheromone solve "Create a simple Python calculator" --model claude-haiku-4-5 --budget 0.50
```

### GitHub Push Checklist

- [ ] All 182+ tests green
- [ ] Coverage >80% on core modules
- [ ] ruff check passes
- [ ] mypy passes (or issues documented)
- [ ] README has working quick start
- [ ] pyproject.toml builds cleanly (`pip install -e .`)
- [ ] .gitignore (standard Python + .pheromone/ + .env)
- [ ] examples/ run with MockLLM
- [ ] At least 1 successful real LLM run documented

**Day 7 Total: 8 files, 182+ tests, 1 real LLM call (manual).**

**Week 1 Cumulative: ~70 source files, 182+ tests, working CLI, GitHub repo live.**

---

## WEEK 1 SUMMARY: WHAT YOU HAVE

After Day 7, `pheromone` is a functional multi-agent framework:

| Capability | Status |
|-----------|--------|
| `colony.solve()` E2E | ✅ Works with MockLLM + real LLM |
| ACO task allocation | ✅ With Response Thresholds + Lévy Flights |
| Hierarchical decomposition | ✅ Goal → Epic → Feature → Task DAG |
| ReAct agent loop | ✅ Multi-turn LLM with tool use |
| Pheromone environment | ✅ Deposit, sense, decay, MAX-MIN |
| File workspace | ✅ Read/write/edit with leasing + conflict detection |
| 8 agent templates | ✅ SoftwareDevTeam, etc. |
| Cost tracking | ✅ Per-agent, per-task, colony total |
| CLI | ✅ `pheromone solve`, `pheromone init` |
| Test infrastructure | ✅ 182+ tests, conftest, factories, CI |

| Capability | Status |
|-----------|--------|
| Review cycles | ❌ Phase 2 |
| Quorum Sensing | ❌ Phase 2 |
| ADR system | ❌ Phase 2 |
| Integration verification | ❌ Phase 2 |
| Stigmergic RL | ❌ Phase 3 |
| TUI (Textual) | ❌ Phase 4 |
| Web GUI | ❌ Phase 4 |
| Git integration | ❌ Phase 2 |
| Redis store | ❌ Phase 2 |
| Pheromone compaction | ❌ Phase 3 |
| Federation | ❌ Phase 4 |

---

## WEEKS 2-12: PHASE PLAN

### Phase 2: Robustness (Weeks 2-4)

**Week 2: Quality Control + Review Loops**

| Day | Deliverable |
|-----|-------------|
| 8 | Review cycle: task execution → test → convention check → peer review → revision loop (§11.2). ReviewRecord model already exists. |
| 9 | ADR system: DepositADR tool creates binding decisions. ADR injection into agent context. Convention enforcement in workspace. |
| 10 | Quorum Sensing: decomposition validation (§8.2). VOTE pheromone type (add to PheromoneType). Async voting with timeout. |
| 11 | Integration Verification Layer (§13): API contract verification, import resolution, integration test generation after FEATURE completion. |
| 12 | Circuit breaker per agent (§16). Heartbeat protocol. Dead agent detection + lease/task recovery. |
| 13 | Specification tracking: PRD parsing → requirement IDs → task mapping → coverage check on completion. |
| 14 | Tests + polish. Target: 250+ tests. |

**Week 3: Infrastructure Hardening**

| Deliverable | Files |
|-------------|-------|
| Redis store | `pheromone/stores/redis_store.py` — atomic ops, pubsub for events |
| Git integration | `pheromone/workspace/git.py` — Gap 13 spec, commit per wave, tag per run |
| Budget manager | Graceful degradation at 80%. Cost-aware allocation bias. Deduplication via knowledge pheromones. |
| Human-in-the-loop | Permission model (allow/ask/deny). DenialTracker. ColonyPermissionSync. |
| Event system producer side | Gap 9 — wire emit callbacks into all 10 component categories (40+ events). |
| UI protocol | `pheromone/ui/protocol.py` — ColonyController ABC. `pheromone/ui/local_controller.py`. |

**Week 4: Templates + Config Polish**

| Deliverable | Files |
|-------------|-------|
| 8 colony templates YAML | `templates/*.yaml` — SoftwareDevTeam, Research, Content, DataScience, Consulting, Legal, Marketing, GeneralPurpose |
| Config polish | TOML support in loader. Full env var mapping. Config dump/export. |
| Structured logging | structlog integration. Ring buffers (activity, error, slow_ops). Correlation IDs. |
| Observability | Prometheus metrics export (optional). Colony replay from audit trail. |

**Phase 2 Exit Criteria:**
- Review loops complete within MAX_REVISIONS
- ADRs enforced on result acceptance
- Quorum validates decomposition
- Circuit breaker isolates failing agents
- 350+ tests, >80% coverage
- Git versioning works per wave

---

### Phase 3: Intelligence (Weeks 5-7)

**Week 5: Evolution Engine**

| Deliverable | Notes |
|-------------|-------|
| Stigmergic RL (§14) | Policy gradient on colony meta-parameters (α, β, γ, ρ, ε). REINFORCE with SRL_LEARNING_RATE. META pheromone persistence. |
| Capability calibration | EMA updates on proficiency, avg_completion_time, avg_quality. |
| Decay tuning | Per-type decay rates from §14. |
| Reinforcement on success | Capability +0.2, knowledge +0.1, ADR +0.05. |

**Week 6: Advanced Environment**

| Deliverable | Notes |
|-------------|-------|
| Pheromone compaction (9-section) | §5.5. LLM-based summarization of old pheromones into META. Preservation window for recent. |
| Codebase auto-indexing | §5.6. KNOWLEDGE pheromones on every FileRead/FileWrite. |
| Knowledge conflict resolution | §15. Semantic negation detection. RESOLUTION task creation. |
| Adaptive colony composition | §6.8. GoalAnalyzer → skill identification → agent spawning. |

**Week 7: Advanced Agents**

| Deliverable | Notes |
|-------------|-------|
| Tool pheromones | §22. Tool results shared to prevent duplicate work. |
| Checkpoint pheromones | §23. Long-running task resumability. |
| Context compaction per agent | §19. 9-section in-agent context management at 90% threshold. |
| Pheromone scoping | §5.7. Private/team/colony/federated enforcement. |

**Phase 3 Exit Criteria:**
- Colony measurably improves over 5+ runs on same task family
- Compaction keeps environment size bounded
- Conflict resolution produces correct verdicts
- 450+ tests

---

### Phase 4: Ecosystem (Weeks 8-10)

**Week 8: CLI/TUI**

| Deliverable | Notes |
|-------------|-------|
| Textual TUI | Gap 6a. 4-region layout (header, DAG, agents, input). Earth-tone theme. 30+ slash commands. /btw with @agent targeting. |
| Non-blocking input | InputQueue with 3 priority levels. |
| Event streaming | ColonyEventStream → TUI widgets. Real-time DAG, agent status, pheromone flow. |

**Week 9: Web GUI**

| Deliverable | Notes |
|-------------|-------|
| FastAPI server | Gap 6b. WebSocket bridge. REST endpoints. CORS. |
| React frontend | Vite + Tailwind + ReactFlow. Colony DAG visualization. Agent timeline. Pheromone flow animation. Dashboard. Approval banner. |
| RemoteColonyController | WebSocket-based controller implementing same ABC. |
| Shared type contract | Gap 7. `types.ts` with all TypeScript interfaces. |

**Week 10: Integration + Security**

| Deliverable | Notes |
|-------------|-------|
| MCP server | §27. Colony exposed as MCP server. Any MCP client can join as agent. |
| Docker | docker-compose.yml. Colony server + Redis + web GUI. |
| Security hardening | §20. Rate limits, content hash verification, sanitization, namespace isolation. |
| Schema versioning | §4.2. Backward-compatible pheromone evolution. Lazy migration. |

**Phase 4 Exit Criteria:**
- `pheromone tui` shows real-time colony execution
- `pheromone gui` serves web dashboard
- MCP server accepts external agents
- Docker one-command deploy works
- 550+ tests

---

### Phase 5: Publication (Weeks 11-12)

**Week 11: Benchmarks + Paper**

| Deliverable | Notes |
|-------------|-------|
| PheromBench | §31. 5 categories × 10 tasks × 5 baselines × 10 runs. Statistical rigor. |
| SWE-bench subset | Run on SWE-bench Verified subset. Compare vs single-agent baseline. |
| arXiv paper draft | "Stigmergic Coordination for LLM-Based Multi-Agent Systems" |
| Blog post 1 | "Why Stigmergy for AI Agents" |

**Week 12: Launch**

| Deliverable | Notes |
|-------------|-------|
| PyPI release | `pip install pheromone` works. |
| GitHub launch | Full README, CONTRIBUTING, examples, docs. |
| HuggingFace Spaces demo | Interactive demo with MockLLM or cheap model. |
| LinkedIn series | 4-part series timed to launch. |
| Blog posts 2-4 | No orchestrator needed, 16 concepts from 10 fields, benchmark results. |
| Paper submission | NeurIPS 2026 Workshop or AAMAS 2027. |

---

## FILE COUNT SUMMARY

| Phase | New Files | Cumulative | Tests |
|-------|-----------|-----------|-------|
| Week 1 (Phase 1) | ~70 | 70 | 182+ |
| Weeks 2-4 (Phase 2) | ~30 | 100 | 350+ |
| Weeks 5-7 (Phase 3) | ~20 | 120 | 450+ |
| Weeks 8-10 (Phase 4) | ~50 (incl React) | 170 | 550+ |
| Weeks 11-12 (Phase 5) | ~15 (benchmarks, docs) | 185 | 600+ |

---

## CLAUDE CODE SESSION PROMPT

When starting a Claude Code implementation session, paste this context:

```
PROJECT: Pheromone — Bio-inspired multi-agent AI coordination framework
REPO: github.com/anshul-ghate/pheromone
PYTHON: 3.11+
ARCHITECTURE: PHEROMONE_v2_1_COMPLETE_FINAL.md (1,808 lines, LOCKED)
SPECS: 13 gap specs resolving all engineering plumbing

CURRENT DAY: [Day N]
BUILDING: [specific files from roadmap]

RULES:
1. DO NOT modify architecture v2.1. Build ON TOP of it.
2. DO NOT run evolution/training/modification during non-build tasks.
3. Every file must have: type hints, docstrings, Pydantic validation.
4. Tests first or alongside — never after.
5. Import from pheromone.errors for ALL exceptions.
6. Import OutputMode from pheromone.models.config (canonical location).
7. Use asyncio.Lock not threading.Lock (except EmbeddingCache).
8. Constants come from pheromone.constants — never hardcode.
9. MockLLM for all tests — no real API calls in CI.
10. File structure follows Gap 11 (dependency_spec.md) package layout.
```

---

## RISK MITIGATION FOR WEEK 1

| Risk | Mitigation |
|------|-----------|
| LiteLLM import issues | MockLLM works without litellm installed. LiteLLMClient lazy-imports litellm. |
| Day 4 agent complexity | ReAct loop can be simplified: just LLM call + tool execution, no compaction/checkpoint in Phase 1. |
| Day 5 Colony wiring bugs | MockLLM + InMemoryStore + NullEmbedder = zero external deps. Any failure is pure logic. |
| Real LLM costs on Day 7 | Use claude-haiku-4-5, budget=$0.50, simple goal. Total cost <$0.10. |
| Test count ambitious | 182 is achievable because most tests are pure model validation (no IO, no mocking complexity). |

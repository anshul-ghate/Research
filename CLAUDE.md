# PHEROMONE — Project Intelligence File

## Identity
Open-source Python framework for bio-inspired multi-agent AI coordination using stigmergic communication (Ant Colony Optimization).
Author: Anshul Ghate | License: MIT | Python >=3.11 | Repo: github.com/anshul-ghate/pheromone

## Architecture
Locked in `docs/PHEROMONE_v2_1_COMPLETE_FINAL.md` (1,808 lines, 36 sections). DO NOT MODIFY.
13 gap specs in `docs/specs/`. These are implementation-level source of truth.
System design + tech stack in `docs/SYSTEM_DESIGN_TECHSTACK_ORCHESTRATION.md`.
Build order in `docs/IMPLEMENTATION_ROADMAP.md`.

## Current Phase
<!-- UPDATE THIS AFTER EACH SESSION -->
Phase: 1 (Foundation)
Day: 0 (pre-implementation)
Tests passing: 0
Last modified: April 8, 2026

## Critical Rules — NEVER VIOLATE
1. **Pydantic v2** for ALL models (BaseModel, Field, model_copy)
2. **errors.py** is CANONICAL for all exception classes — import from pheromone.errors
3. **config.py** is CANONICAL for OutputMode — import from pheromone.models.config
4. **constants.py** for ALL numeric constants — NEVER hardcode values
5. **asyncio.Lock** for async code. threading.Lock ONLY for EmbeddingCache
6. **MockLLM** for ALL tests — zero real API calls in CI
7. **litellm>=1.83.0** ONLY — versions 1.82.7 and 1.82.8 were compromised in a supply chain attack
8. **MAX-MIN bounds** on ALL pheromone strength mutations: clamp(strength, TAU_MIN=0.01, TAU_MAX=5.0)
9. **ExecutionTracker** (separate dict) for execution state — NOT monkey-patched TaskNode
10. **Content hash** (SHA-256) for ALL file edit conflict detection
11. DO NOT add features beyond the current day's scope
12. Write tests alongside code, not after

## Cross-Spec Contracts
These models are defined in specific files and imported everywhere else:

| Model | Defined In | Used By |
|-------|-----------|---------|
| LLMRequest, LLMResponse, LLMToolCall, LLMUsage | pheromone/llm/models.py | client, mock, middleware, react_loop |
| Pheromone, PheromoneType, PheromoneScope, SenseResult | pheromone/models/pheromones.py | environment, agents, engine, tools |
| TaskNode, TaskStatus, HierarchicalTaskGraph | pheromone/models/tasks.py | decomposer, allocator, engine |
| ColonyConfig, Strategy, AgentConfig, LiveBudget | pheromone/models/config.py | colony, engine, agents |
| TaskOutput, TaskExecutionRecord, ExecutionTracker | pheromone/models/execution.py | react_loop, engine, assembler |
| ColonyResult, WorkspaceOutput, TextOutput, HybridOutput | pheromone/models/results.py | assembler, colony, reporters |
| OutputMode, HYBRID_TEXT_THRESHOLD_WORDS | pheromone/models/config.py | assembler (IMPORT, don't redefine) |
| ColonyEvent, EventType | pheromone/ui/events.py | engine, colony, controllers |

## Package Structure
```
pheromone/
├── __init__.py              # Public API: Colony, ColonyConfig, AgentConfig, Strategy, ColonyResult, Pheromone, PheromoneType
├── py.typed                 # PEP 561 marker
├── colony.py                # Colony class (11-step init, solve, register, shutdown)
├── constants.py             # ALL constants from architecture §3
├── errors.py                # Error taxonomy (25 exception classes)
├── models/
│   ├── config.py            # ColonyConfig + 8 sub-models + OutputMode + LiveBudget
│   ├── pheromones.py        # Pheromone, PheromoneType, PheromoneScope, SenseResult
│   ├── tasks.py             # TaskNode, HierarchicalTaskGraph, TaskStatus, ReviewRecord
│   ├── execution.py         # TaskOutput, TaskExecutionRecord, ExecutionTracker, LLMUsage
│   └── results.py           # ColonyResult, ColonyOutput (discriminated union), reporters
├── llm/
│   ├── models.py            # LLMRequest, LLMResponse, LLMToolCall, LLMMessage
│   ├── client.py            # BaseLLMClient ABC, LiteLLMClient
│   ├── mock.py              # MockLLM, MockResponse
│   ├── retry.py             # RetryPolicy
│   ├── capabilities.py      # MODEL_REGISTRY, ModelCapabilities
│   ├── parsers.py           # JSONTextParser, XMLTextParser
│   ├── middleware.py         # LLMMiddleware ABC, CapabilityAware, Logging, build_middleware_stack
│   ├── cache.py             # CachingMiddleware
│   └── fallback.py          # FallbackLLMClient
├── stores/
│   ├── base.py              # PheromoneStore ABC
│   ├── memory.py            # InMemoryStore
│   ├── redis_store.py       # RedisStore [optional: pheromone[redis]]
│   └── result_store.py      # ResultStore (JSON persistence)
├── environment/
│   ├── environment.py       # PheromoneEnvironment
│   └── embeddings.py        # EmbeddingService, BaseEmbedder, NullEmbedder, SentenceTransformerEmbedder
├── workspace/
│   ├── manager.py           # WorkspaceManager
│   ├── editor.py            # FileEditor (str_replace + conflict detection)
│   ├── leasing.py           # WorkspaceLeaseManager
│   └── git.py               # WorkspaceGit [optional: pheromone[git]]
├── agents/
│   ├── proxy.py             # AgentProxy
│   ├── react_loop.py        # AgentReActLoop
│   ├── thresholds.py        # ResponseThresholdModel
│   ├── tool_orchestrator.py # ToolOrchestrator
│   ├── prompt_builder.py    # AgentPromptBuilder
│   ├── templates.py         # 8 colony templates
│   └── composer.py          # GoalAnalyzer (adaptive composition)
├── engine/
│   ├── lifecycle.py         # EngineState, TRANSITIONS
│   ├── execution.py         # ExecutionEngine
│   ├── decomposer.py        # HierarchicalDecomposer
│   ├── allocator.py         # StigmergicAllocator
│   ├── assembler.py         # OutputAssembler
│   └── reporters.py         # TerminalReporter, MarkdownReporter
├── tools/
│   ├── base.py              # ToolDefinition, ToolResult, BaseTool ABC
│   ├── registry.py          # TOOL_PROFILES, get_tools_for_agent
│   ├── core/                # FileRead, FileWrite, FileEdit, Bash, Glob, Grep
│   ├── pheromone/           # Sense, DepositKnowledge, DepositADR, DepositWarning
│   └── workspace/           # AcquireLease, RunTests, GetProjectContext
├── ui/
│   ├── events.py            # ColonyEvent, EventType
│   ├── protocol.py          # ColonyController ABC
│   ├── local_controller.py  # LocalColonyController
│   └── remote_controller.py # RemoteColonyController
├── config/
│   ├── loader.py            # load_config()
│   └── validator.py         # validate_config()
├── cli/
│   ├── main.py              # Typer entry points
│   ├── app.py               # PheromoneApp (Textual) [optional: pheromone[tui]]
│   └── ...
├── api/
│   └── server.py            # FastAPI WebSocket bridge [optional: pheromone[gui]]
├── evolution/
│   └── stigmergic_rl.py    # Phase 3
└── compat/
    └── claude_md.py         # CLAUDE.md loader
```

## Key Design Decisions
- **LiteLLM** wraps all LLM providers (not direct SDKs)
- **InMemoryStore** default, RedisStore optional
- **NullEmbedder** Phase 1 default, SentenceTransformer Phase 2+
- **Textual** for TUI, **React + FastAPI** for Web GUI
- **ColonyController ABC** shared by CLI and GUI (same protocol)
- Config layering: Defaults → YAML → env vars → code overrides
- Event system: constructor-injected emit callback, 40+ event types
- Budget naming: `spent_dollars` / `max_dollars` (not `spent_usd`)
- Earth-tone visual identity: amber #D4A574, forest green #8B9E6B, clay #C17F59

## Test Commands
```bash
pytest -v                                     # All tests
pytest -v -m "not slow"                       # Skip ML model loading
pytest -v --cov=pheromone --cov-report=term   # With coverage
ruff check pheromone/                         # Lint
mypy pheromone/                               # Type check
```

## Spec File Index
| Spec | File | Lines | Build Phase |
|------|------|-------|-------------|
| Architecture | docs/PHEROMONE_v2_1_COMPLETE_FINAL.md | 1808 | ALL |
| System Design | docs/SYSTEM_DESIGN_TECHSTACK_ORCHESTRATION.md | ~1200 | ALL |
| Roadmap | docs/IMPLEMENTATION_ROADMAP.md | ~600 | ALL |
| Gap 1: LLM Client | docs/specs/llm_client_spec.md | 2648 | Phase 1 |
| Gap 2: Output Assembly | docs/specs/output_assembly_spec.md | 237 | Phase 1 |
| Gap 3: Config/Init | docs/specs/config_init_spec.md | 1259 | Phase 1 |
| Gap 4: Embeddings | docs/specs/embedding_service_spec.md | 751 | Phase 1 |
| Gap 5: Test Infra | docs/specs/test_infra_spec.md | 645 | Phase 1 |
| Gap 6a: CLI/TUI | docs/specs/cli_tui_spec.md | 1512 | Phase 4 |
| Gap 6b: Web GUI | docs/specs/web_gui_spec.md | 1256 | Phase 4 |
| Gap 7: Shared Types | docs/specs/colony_result_spec.md | 835 | Phase 4 |
| Gap 9: Events | docs/specs/event_system_spec.md | 635 | Phase 2 |
| Gap 10: Lifecycle | docs/specs/colony_lifecycle_spec.md | 842 | Phase 2 |
| Gap 11: Dependencies | docs/specs/dependency_spec.md | 469 | Phase 1 |
| Gap 12: Errors | docs/specs/error_taxonomy_spec.md | 413 | Phase 1 |
| Gap 13: Git | docs/specs/git_integration_spec.md | 347 | Phase 2 |
| Cross-Spec Audit | docs/specs/CROSS_SPEC_AUDIT.md | 251 | Phase 1 |
| LLM Interaction | docs/specs/LLM_INTERACTION_SPECS.md | ~800 | Phase 1 |
| Pre-Impl Audit | docs/specs/PRE_IMPLEMENTATION_AUDIT.md | ~400 | Phase 1 |

## Session Protocol
At the END of each Claude Code session, produce a handoff note:
1. Files created/modified
2. Tests passing (count)
3. Decisions that differ from specs (if any)
4. What to build next
5. Known issues / TODOs
Save to: `docs/sessions/session-{N}-{YYYY-MM-DD}.md`

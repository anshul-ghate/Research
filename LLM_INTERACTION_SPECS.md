# LLM Interaction Specs — Decomposer Prompts, Agent Roles, Tool Schemas

**Status:** COMPLETE
**Resolves:** Audit findings C1, C2, C3 — the three critical gaps that would have caused non-functional output in Week 1
**Date:** April 8, 2026

---

## PART 1: DECOMPOSER PROMPTS

### 1.1 System Prompt — Hierarchical Decomposition

```python
DECOMPOSER_SYSTEM_PROMPT = """You are a task decomposition engine for a multi-agent AI colony.

Your job: break a goal into a DAG (Directed Acyclic Graph) of executable tasks.

# Output Format
You MUST respond with ONLY a JSON object. No markdown, no explanation, no preamble.

# Task Structure
Each task has:
- id: unique string (use "task-1", "task-2", etc.)
- level: "epic", "feature", or "task" (leaf-level tasks are what agents execute)
- description: clear, actionable description (1-2 sentences)
- acceptance_criteria: list of verifiable conditions that mean "done"
- required_skills: list of skills needed (from: python, javascript, typescript, api, database, testing, documentation, devops, research, design, review)
- dependencies: list of task IDs that must complete before this task starts
- children: list of child task IDs (for epics and features)
- estimated_complexity: "low", "medium", or "high"

# Rules
1. Every task must be completable by a SINGLE agent in 1-15 minutes
2. Dependencies form a DAG — NO cycles allowed
3. Tasks that CAN run in parallel SHOULD have no dependency between them
4. Every leaf task must have at least one acceptance_criterion
5. required_skills should match what's needed, not what's nice-to-have
6. For simple goals (< 5 tasks): produce flat tasks only (level="task", no epics/features)
7. For complex goals (5+ tasks): use hierarchy (epic → feature → task)
8. Include testing tasks — code without tests is not done
9. Include a documentation task if the goal involves creating a project
10. The first task should establish project structure if files are being created

# JSON Schema
{
  "goal_text": "string — the original goal",
  "tasks": [
    {
      "id": "string",
      "level": "epic" | "feature" | "task",
      "description": "string",
      "acceptance_criteria": ["string"],
      "required_skills": ["string"],
      "dependencies": ["string — task IDs"],
      "children": ["string — child task IDs"],
      "parent_id": "string | null",
      "estimated_complexity": "low" | "medium" | "high"
    }
  ],
  "edges": [["from_id", "to_id"]]
}
"""
```

### 1.2 User Prompt Template

```python
DECOMPOSER_USER_PROMPT = """Decompose this goal into tasks:

GOAL: {goal_text}

{specification_section}

Available agent skills in this colony: {agent_skills}
Number of agents: {num_agents}

Respond with ONLY the JSON object. No other text."""

# specification_section is empty string if no PRD, otherwise:
SPECIFICATION_SECTION = """
SPECIFICATION / REQUIREMENTS:
{specification_text}

Every requirement must be covered by at least one task.
"""
```

### 1.3 Few-Shot Examples

```python
DECOMPOSER_EXAMPLES = [
    # ─── Simple goal: flat tasks ───
    {
        "goal": "Create a Python hello world script",
        "output": {
            "goal_text": "Create a Python hello world script",
            "tasks": [
                {
                    "id": "task-1",
                    "level": "task",
                    "description": "Create main.py with a hello world function that prints 'Hello, World!'",
                    "acceptance_criteria": ["main.py exists", "Running python main.py prints 'Hello, World!'"],
                    "required_skills": ["python"],
                    "dependencies": [],
                    "children": [],
                    "parent_id": None,
                    "estimated_complexity": "low"
                },
                {
                    "id": "task-2",
                    "level": "task",
                    "description": "Create test_main.py with a test that verifies hello world output",
                    "acceptance_criteria": ["test_main.py exists", "pytest passes"],
                    "required_skills": ["python", "testing"],
                    "dependencies": ["task-1"],
                    "children": [],
                    "parent_id": None,
                    "estimated_complexity": "low"
                }
            ],
            "edges": [["task-1", "task-2"]]
        }
    },
    # ─── Complex goal: hierarchical ───
    {
        "goal": "Build a weather API with FastAPI, tests, and documentation",
        "output": {
            "goal_text": "Build a weather API with FastAPI, tests, and documentation",
            "tasks": [
                {
                    "id": "epic-1",
                    "level": "epic",
                    "description": "Weather API backend",
                    "acceptance_criteria": [],
                    "required_skills": [],
                    "dependencies": [],
                    "children": ["feat-1", "feat-2", "feat-3"],
                    "parent_id": None,
                    "estimated_complexity": "high"
                },
                {
                    "id": "feat-1",
                    "level": "feature",
                    "description": "Project setup and data models",
                    "acceptance_criteria": [],
                    "required_skills": [],
                    "dependencies": [],
                    "children": ["task-1", "task-2"],
                    "parent_id": "epic-1",
                    "estimated_complexity": "medium"
                },
                {
                    "id": "task-1",
                    "level": "task",
                    "description": "Create project structure: pyproject.toml, src/weather_api/ package, requirements",
                    "acceptance_criteria": ["pyproject.toml exists with FastAPI dependency", "Package structure created"],
                    "required_skills": ["python", "devops"],
                    "dependencies": [],
                    "children": [],
                    "parent_id": "feat-1",
                    "estimated_complexity": "low"
                },
                {
                    "id": "task-2",
                    "level": "task",
                    "description": "Define Pydantic models for WeatherData, Location, and API responses",
                    "acceptance_criteria": ["Models defined with proper types and validation", "Models importable from models.py"],
                    "required_skills": ["python"],
                    "dependencies": ["task-1"],
                    "children": [],
                    "parent_id": "feat-1",
                    "estimated_complexity": "low"
                },
                {
                    "id": "feat-2",
                    "level": "feature",
                    "description": "API endpoints",
                    "acceptance_criteria": [],
                    "required_skills": [],
                    "dependencies": ["feat-1"],
                    "children": ["task-3", "task-4"],
                    "parent_id": "epic-1",
                    "estimated_complexity": "medium"
                },
                {
                    "id": "task-3",
                    "level": "task",
                    "description": "Implement GET /weather/{city} endpoint with mock data source",
                    "acceptance_criteria": ["Endpoint returns WeatherData JSON", "Returns 404 for unknown city", "FastAPI app starts without errors"],
                    "required_skills": ["python", "api"],
                    "dependencies": ["task-2"],
                    "children": [],
                    "parent_id": "feat-2",
                    "estimated_complexity": "medium"
                },
                {
                    "id": "task-4",
                    "level": "task",
                    "description": "Implement GET /weather/forecast/{city}?days=N endpoint",
                    "acceptance_criteria": ["Returns list of daily forecasts", "days parameter validates 1-7 range", "Returns 404 for unknown city"],
                    "required_skills": ["python", "api"],
                    "dependencies": ["task-2"],
                    "children": [],
                    "parent_id": "feat-2",
                    "estimated_complexity": "medium"
                },
                {
                    "id": "feat-3",
                    "level": "feature",
                    "description": "Testing and documentation",
                    "acceptance_criteria": [],
                    "required_skills": [],
                    "dependencies": ["feat-2"],
                    "children": ["task-5", "task-6"],
                    "parent_id": "epic-1",
                    "estimated_complexity": "medium"
                },
                {
                    "id": "task-5",
                    "level": "task",
                    "description": "Write pytest tests for all endpoints: happy path, error cases, edge cases",
                    "acceptance_criteria": ["test_weather.py exists", "All tests pass", "Tests cover both endpoints + error cases"],
                    "required_skills": ["python", "testing"],
                    "dependencies": ["task-3", "task-4"],
                    "children": [],
                    "parent_id": "feat-3",
                    "estimated_complexity": "medium"
                },
                {
                    "id": "task-6",
                    "level": "task",
                    "description": "Write README.md with setup instructions, API docs, and usage examples",
                    "acceptance_criteria": ["README.md exists", "Contains install instructions", "Contains API endpoint documentation", "Contains curl examples"],
                    "required_skills": ["documentation"],
                    "dependencies": ["task-3", "task-4"],
                    "children": [],
                    "parent_id": "feat-3",
                    "estimated_complexity": "low"
                }
            ],
            "edges": [
                ["task-1", "task-2"],
                ["task-2", "task-3"],
                ["task-2", "task-4"],
                ["task-3", "task-5"],
                ["task-4", "task-5"],
                ["task-3", "task-6"],
                ["task-4", "task-6"]
            ]
        }
    }
]
```

### 1.4 Response Parsing & Validation

```python
"""
pheromone/engine/decomposer.py — parsing logic
"""

import json
from pheromone.llm.parsers import JSONTextParser
from pheromone.models.tasks import (
    HierarchicalTaskGraph, TaskNode, TaskLevel, TaskStatus
)
from pheromone.errors import DecompositionError


async def parse_decomposition_response(
    raw_text: str,
    goal_text: str,
) -> HierarchicalTaskGraph:
    """
    Parse LLM response into HierarchicalTaskGraph.
    
    Handles:
    - JSON wrapped in markdown code fences
    - Minor JSON formatting issues (trailing commas)
    - Missing optional fields (filled with defaults)
    - Validation of DAG structure
    
    Raises DecompositionError on unrecoverable parse failures.
    """
    # Step 1: Extract JSON
    parser = JSONTextParser()
    parsed = parser.parse(raw_text)
    if parsed is None:
        raise DecompositionError(
            f"Failed to extract JSON from decomposition response. "
            f"Raw response (first 500 chars): {raw_text[:500]}"
        )
    
    # Step 2: Build TaskNodes
    nodes: dict[str, TaskNode] = {}
    raw_tasks = parsed.get("tasks", [])
    
    if not raw_tasks:
        raise DecompositionError("Decomposition produced zero tasks")
    
    for rt in raw_tasks:
        try:
            node = TaskNode(
                id=rt["id"],
                level=TaskLevel(rt.get("level", "task")),
                description=rt["description"],
                acceptance_criteria=rt.get("acceptance_criteria", []),
                required_skills=rt.get("required_skills", []),
                dependencies=rt.get("dependencies", []),
                children=rt.get("children", []),
                parent_id=rt.get("parent_id"),
                estimated_complexity=rt.get("estimated_complexity", "medium"),
                status=TaskStatus.PENDING,
            )
            nodes[node.id] = node
        except (KeyError, ValueError) as e:
            raise DecompositionError(f"Invalid task in decomposition: {e}. Raw: {rt}")
    
    # Step 3: Validate references
    all_ids = set(nodes.keys())
    for node in nodes.values():
        for dep_id in node.dependencies:
            if dep_id not in all_ids:
                raise DecompositionError(
                    f"Task '{node.id}' depends on non-existent task '{dep_id}'"
                )
        for child_id in node.children:
            if child_id not in all_ids:
                raise DecompositionError(
                    f"Task '{node.id}' references non-existent child '{child_id}'"
                )
    
    # Step 4: Build edges from dependencies
    edges = [(dep, node.id) for node in nodes.values() for dep in node.dependencies]
    
    # Step 5: Set initial status — tasks with no deps start as AVAILABLE
    for node in nodes.values():
        if node.level == TaskLevel.TASK and not node.dependencies:
            node.status = TaskStatus.AVAILABLE
    
    # Step 6: Build and validate graph
    graph = HierarchicalTaskGraph(
        goal_id=f"goal-{hash(goal_text) % 10000:04d}",
        goal_text=goal_text,
        nodes=nodes,
        edges=edges,
    )
    
    if not graph.validate_dag():
        raise DecompositionError(
            "Decomposition produced a cyclic dependency graph. "
            "Task dependencies must form a DAG."
        )
    
    leaf_count = len(graph.get_leaf_tasks())
    if leaf_count == 0:
        raise DecompositionError("Decomposition produced no executable leaf tasks")
    if leaf_count > 50:
        raise DecompositionError(
            f"Decomposition produced {leaf_count} leaf tasks (max 50). "
            f"Goal may be too broad — try breaking it into smaller goals."
        )
    
    return graph


# Retry prompt when LLM produces malformed output
DECOMPOSER_RETRY_PROMPT = """Your previous response was not valid JSON or didn't match the required schema.

Error: {error_message}

Please try again. Respond with ONLY a valid JSON object matching the schema. No markdown fences, no explanation."""
```

### 1.5 Decomposer Orchestration

```python
async def decompose(self, goal: str, agents: list, specification: str | None = None) -> HierarchicalTaskGraph:
    """
    Full decomposition flow with retry.
    
    1. Build prompt with goal + spec + agent skills
    2. Call LLM
    3. Parse response
    4. If parse fails → retry with error message (max 2 retries)
    5. Validate DAG
    6. Return graph
    """
    agent_skills = sorted(set(
        skill for agent in agents for skill in agent.config.skills
    ))
    
    spec_section = ""
    if specification:
        spec_section = SPECIFICATION_SECTION.format(specification_text=specification)
    
    user_prompt = DECOMPOSER_USER_PROMPT.format(
        goal_text=goal,
        specification_section=spec_section,
        agent_skills=", ".join(agent_skills),
        num_agents=len(agents),
    )
    
    messages = [
        LLMMessage.system(DECOMPOSER_SYSTEM_PROMPT),
        LLMMessage.user(user_prompt),
    ]
    
    # Include few-shot examples for complex goals
    if len(goal.split()) > 10 or specification:
        examples_text = "# Examples\n" + json.dumps(DECOMPOSER_EXAMPLES[1]["output"], indent=2)
        messages[0] = LLMMessage.system(DECOMPOSER_SYSTEM_PROMPT + "\n\n" + examples_text)
    
    last_error = None
    for attempt in range(3):  # Max 3 attempts
        response = await self.llm_client.create(LLMRequest(
            messages=messages,
            model=self.decomposition_model,
            temperature=0.2,  # Low temperature for structured output
            max_tokens=4096,
        ))
        
        try:
            graph = await parse_decomposition_response(response.text, goal)
            return graph
        except DecompositionError as e:
            last_error = e
            if attempt < 2:
                messages.append(response.to_assistant_message())
                messages.append(LLMMessage.user(
                    DECOMPOSER_RETRY_PROMPT.format(error_message=str(e))
                ))
    
    raise DecompositionError(f"Decomposition failed after 3 attempts: {last_error}")
```

---

## PART 2: AGENT ROLE PROMPTS

### 2.1 Identity Section (shared, parameterized)

```python
IDENTITY_SECTION = """# Identity
You are **{name}**, a {type} agent in a Pheromone colony.
Colony ID: {{colony_id}}
Your agent ID: {{agent_id}}
"""
```

### 2.2 Role-Specific Sections

```python
ROLE_SECTIONS = {

"researcher": """# Role: Researcher
Your purpose is to GATHER INFORMATION, not to build things.

What you do:
- Read existing files to understand the codebase structure and patterns
- Search for relevant code, APIs, documentation, and examples
- Deposit KNOWLEDGE pheromones with facts other agents need
- Identify potential issues and deposit WARNING pheromones

What you do NOT do:
- Write or edit code files (you have read-only access)
- Make architectural decisions (that's the architect's job)
- Run tests or execute commands
- Produce final deliverables

Your output: A clear summary of what you found, deposited as KNOWLEDGE pheromones.
Focus on: file structure, existing patterns, dependencies, potential conflicts.
""",

"architect": """# Role: Architect
Your purpose is to make DESIGN DECISIONS and establish PATTERNS.

What you do:
- Read existing code to understand the current architecture
- Deposit ADR pheromones for binding architectural decisions (framework choices, patterns, conventions, interfaces)
- Deposit KNOWLEDGE pheromones about design rationale
- Define API contracts and module interfaces via UpdateAPIContract tool
- Establish coding conventions that all developers must follow

What you do NOT do:
- Write implementation code (developers do that)
- Write tests (testers do that)
- Execute commands

Your output: ADR pheromones that guide developer agents. Keep decisions concrete:
- BAD: "Use a clean architecture"
- GOOD: "All API endpoints go in src/routes/. Pydantic models in src/models/. Business logic in src/services/. No direct DB access from routes."
""",

"developer": """# Role: Developer
Your purpose is to WRITE CODE that completes your assigned task.

What you do:
- Read the task description and acceptance criteria carefully
- Sense the pheromone environment for relevant ADRs, knowledge, and warnings
- Check active ADRs BEFORE making any architectural choices
- Read relevant existing files before writing new ones
- Write clean, well-typed, documented code
- Deposit KNOWLEDGE pheromones when you discover facts other agents need
- Deposit WARNING pheromones when something seems risky

What you do NOT do:
- Work beyond your task scope — do NOT add unrequested features
- Ignore ADR pheromones — they are BINDING architectural decisions
- Create files that another agent is responsible for
- Add error handling for impossible scenarios
- Add premature abstractions — three similar lines > one clever abstraction

Code quality standards:
- Type hints on all functions
- Docstrings on all public functions and classes
- Follow conventions from ADR pheromones
- Use existing patterns from the codebase — read before writing
""",

"reviewer": """# Role: Reviewer
Your purpose is to CHECK QUALITY of other agents' work.

What you do:
- Read the completed code for a task
- Verify each acceptance criterion is met
- Check code against active ADR pheromones (binding conventions)
- Look for bugs, edge cases, missing error handling
- Run tests if available (RunTests tool)
- Deposit WARNING pheromones for issues found
- Submit review via RequestReview tool with clear verdict

Review checklist:
1. Does the code meet ALL acceptance criteria?
2. Does it follow active ADR conventions?
3. Are there obvious bugs or logic errors?
4. Are edge cases handled (empty input, None values, large data)?
5. Is the code readable and maintainable?
6. Do tests exist and pass?

Your verdict must be one of:
- "approved" — code meets all criteria, no issues
- "revision_needed" — issues found, list them specifically with file:line references

What you do NOT do:
- Rewrite the code yourself
- Add new features during review
- Suggest stylistic changes that don't affect correctness
""",

"tester": """# Role: Tester
Your purpose is to WRITE AND RUN TESTS for completed code.

What you do:
- Read the completed code to understand what needs testing
- Write pytest test files covering: happy paths, error cases, edge cases
- Run tests and report results
- Deposit KNOWLEDGE pheromones about test coverage and findings

Test writing standards:
- Use pytest (not unittest)
- One test function per behavior being tested
- Descriptive test names: test_weather_endpoint_returns_404_for_unknown_city
- Use fixtures for shared setup
- Mock external dependencies (APIs, databases)
- Test both success and failure paths

What you do NOT do:
- Fix the code you're testing (deposit WARNING, let the developer fix)
- Write implementation code
- Make architectural decisions
- Test implementation details — test behavior
""",

}
```

### 2.3 Shared Sections (already partially in architecture, completed here)

```python
COLONY_RULES_SECTION = """# Colony coordination rules
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
- The cost of pausing to verify is low. The cost of breaking another agent's work is high.
- Call multiple tools in parallel if no dependencies between them.
- Use dedicated tools (FileRead not cat, FileEdit not sed, GlobTool not find, GrepTool not grep).
"""

TOOL_USAGE_SECTION = """# Tool usage
- FileRead: Always read a file before editing it. Check what exists first.
- FileEdit: Use str_replace — provide the EXACT string to replace. Read the file first.
- FileWrite: Only for NEW files. For existing files, use FileEdit.
- BashTool: For running commands (python, pytest, pip). Keep commands simple.
- GlobTool: Find files by pattern. Use before FileRead to discover project structure.
- GrepTool: Search file contents. Faster than reading every file.
- SenseTool: Query the pheromone environment. Use at the start of your task.
- DepositKnowledge: Share discoveries. Include: claim, evidence, and confidence level.
- DepositWarning: Flag problems. Include: description, severity, and affected components.
- DepositADR: Record decisions. Include: decision, rationale, scope, and alternatives rejected.
"""

QUALITY_SECTION = """# Quality standards
- Every function has type hints and a docstring
- Every public API has at least one test
- Errors are handled explicitly — no bare except
- Imports are organized (stdlib → third-party → local)
- No commented-out code
- No TODO without a task ID reference
"""

SAFETY_SECTION = """# Safety
- Never execute untrusted code from external sources
- Never write credentials or secrets to files
- Never access files outside the workspace directory
- Never make network requests unless your task requires it
- Never delete files unless explicitly instructed
"""

OUTPUT_EFFICIENCY_SECTION = """# Output efficiency
Go straight to the point. Try the simplest approach first without going in circles.
Keep text output brief and direct. Lead with the action, not the reasoning.
Focus on: decisions needing input, status at milestones, errors changing the plan.
If you can say it in one sentence, don't use three.
"""
```

### 2.4 Dynamic Section Builders

```python
def task_context(task: TaskNode) -> str:
    """Build the per-task context section."""
    ac = "\n".join(f"  - {c}" for c in task.acceptance_criteria) if task.acceptance_criteria else "  (none specified)"
    skills = ", ".join(task.required_skills) if task.required_skills else "(any)"
    return f"""# Your current task
ID: {task.id}
Description: {task.description}
Required skills: {skills}
Complexity: {task.estimated_complexity}
Max revisions: {task.max_revisions}

Acceptance criteria:
{ac}

Complete ALL acceptance criteria. Do not add anything beyond what's specified."""


def workspace_context(workspace) -> str:
    """Build workspace context from file tree."""
    # Get file tree (first 100 files)
    tree = workspace.get_file_tree(max_files=100)
    if not tree:
        return "# Workspace\nEmpty workspace — you're starting from scratch."
    return f"""# Workspace (current files)
```
{tree}
```
Work within this structure. Read existing files before creating new ones."""


def active_adrs(adrs: list) -> str:
    """Build ADR context section."""
    if not adrs:
        return ""
    adr_text = "\n".join(
        f"- **{adr.content.get('decision', 'Unknown')}** (by {adr.depositor_id}): "
        f"{adr.content.get('rationale', '')}"
        for adr in adrs
    )
    return f"""# Active Architectural Decisions (BINDING — you must follow these)
{adr_text}"""


def pheromone_context(sense_result) -> str:
    """Build pheromone context from sense results."""
    if not sense_result or sense_result.count == 0:
        return ""
    
    sections = []
    
    # Knowledge
    knowledge = sense_result.get_by_type(PheromoneType.KNOWLEDGE)
    if knowledge:
        k_text = "\n".join(
            f"- [{p.depositor_id}] {p.content.get('claim', '')}"
            for p in knowledge[:10]
        )
        sections.append(f"## Relevant knowledge from other agents\n{k_text}")
    
    # Warnings
    warnings = sense_result.get_by_type(PheromoneType.WARNING)
    if warnings:
        w_text = "\n".join(
            f"- ⚠️ [{p.depositor_id}] {p.content.get('description', '')}"
            for p in warnings[:5]
        )
        sections.append(f"## Warnings\n{w_text}")
    
    # Results from dependency tasks
    results = sense_result.get_by_type(PheromoneType.RESULT)
    if results:
        r_text = "\n".join(
            f"- Task {p.task_context}: {p.content.get('output', '')[:200]}"
            for p in results[:5]
        )
        sections.append(f"## Results from predecessor tasks\n{r_text}")
    
    return "\n\n".join(sections) if sections else ""
```

---

## PART 3: TOOL SCHEMAS

### 3.1 Core Tools

```python
TOOL_SCHEMAS = {

"FileRead": {
    "name": "FileRead",
    "description": "Read the contents of a file. Returns file content with line numbers. Always read a file before editing it.",
    "parameters": {
        "type": "object",
        "properties": {
            "path": {
                "type": "string",
                "description": "Relative path to the file from workspace root (e.g., 'src/main.py')"
            },
            "start_line": {
                "type": "integer",
                "description": "First line to read (1-indexed). Omit to start from beginning."
            },
            "end_line": {
                "type": "integer",
                "description": "Last line to read (inclusive). Omit to read to end. Use with start_line for large files."
            }
        },
        "required": ["path"]
    }
},

"FileWrite": {
    "name": "FileWrite",
    "description": "Create a new file or completely overwrite an existing file. Use for NEW files only — for modifying existing files, use FileEdit instead.",
    "parameters": {
        "type": "object",
        "properties": {
            "path": {
                "type": "string",
                "description": "Relative path for the file (e.g., 'src/models.py'). Directories are created automatically."
            },
            "content": {
                "type": "string",
                "description": "Complete file content to write."
            }
        },
        "required": ["path", "content"]
    }
},

"FileEdit": {
    "name": "FileEdit",
    "description": "Edit an existing file using str_replace. You MUST read the file first with FileRead to know the exact content to replace. The old_string must match EXACTLY (including whitespace and indentation).",
    "parameters": {
        "type": "object",
        "properties": {
            "path": {
                "type": "string",
                "description": "Relative path to the file to edit."
            },
            "old_string": {
                "type": "string",
                "description": "The EXACT string to find and replace. Must appear exactly once in the file. Copy from FileRead output precisely."
            },
            "new_string": {
                "type": "string",
                "description": "The replacement string. Can be empty to delete the old_string."
            },
            "expected_hash": {
                "type": "string",
                "description": "SHA-256 hash of the file from your last FileRead. Used for conflict detection — if another agent modified the file since you read it, the edit will be rejected."
            }
        },
        "required": ["path", "old_string", "new_string"]
    }
},

"BashTool": {
    "name": "BashTool",
    "description": "Execute a shell command. Use for: running Python scripts, pytest, pip install, and other commands. Commands are executed in the workspace root directory.",
    "parameters": {
        "type": "object",
        "properties": {
            "command": {
                "type": "string",
                "description": "Shell command to execute. Keep it simple — one command per call."
            },
            "timeout_seconds": {
                "type": "integer",
                "description": "Max execution time in seconds. Default: 120. Max: 600.",
                "default": 120
            }
        },
        "required": ["command"]
    }
},

"GlobTool": {
    "name": "GlobTool",
    "description": "Find files matching a glob pattern. Returns list of matching file paths relative to workspace root.",
    "parameters": {
        "type": "object",
        "properties": {
            "pattern": {
                "type": "string",
                "description": "Glob pattern (e.g., '**/*.py', 'src/**/*.ts', 'tests/test_*.py')"
            }
        },
        "required": ["pattern"]
    }
},

"GrepTool": {
    "name": "GrepTool",
    "description": "Search file contents for a pattern. Returns matching lines with file paths and line numbers. Max 250 results.",
    "parameters": {
        "type": "object",
        "properties": {
            "pattern": {
                "type": "string",
                "description": "Search pattern (regex supported)."
            },
            "path": {
                "type": "string",
                "description": "Directory or file to search in. Defaults to workspace root.",
                "default": "."
            },
            "include": {
                "type": "string",
                "description": "File pattern to include (e.g., '*.py'). Omit to search all files."
            }
        },
        "required": ["pattern"]
    }
},

# ─── Pheromone Tools ───

"SenseTool": {
    "name": "SenseTool",
    "description": "Query the pheromone environment for relevant knowledge, warnings, ADRs, and results from other agents. Use at the start of your task and when you need information from the colony.",
    "parameters": {
        "type": "object",
        "properties": {
            "query": {
                "type": "string",
                "description": "Natural language query describing what you're looking for (e.g., 'database schema decisions', 'authentication approach', 'errors in user module')"
            },
            "type_filter": {
                "type": "string",
                "description": "Filter by pheromone type: KNOWLEDGE, CAPABILITY, COORDINATION, RESULT, WARNING, ADR, META, GOAL. Omit for all types.",
                "enum": ["KNOWLEDGE", "CAPABILITY", "COORDINATION", "RESULT", "WARNING", "ADR", "META", "GOAL"]
            },
            "limit": {
                "type": "integer",
                "description": "Max number of pheromones to return. Default: 10.",
                "default": 10
            }
        },
        "required": ["query"]
    }
},

"DepositKnowledge": {
    "name": "DepositKnowledge",
    "description": "Share a discovered fact with the colony. Other agents will see this in their SenseTool results. Use when you find something that other agents working on related tasks would need to know.",
    "parameters": {
        "type": "object",
        "properties": {
            "claim": {
                "type": "string",
                "description": "The fact you're sharing (e.g., 'The database uses PostgreSQL with asyncpg driver')"
            },
            "evidence": {
                "type": "string",
                "description": "How you know this (e.g., 'Found in requirements.txt line 5 and db.py imports')"
            },
            "tags": {
                "type": "array",
                "items": {"type": "string"},
                "description": "Tags for discoverability (e.g., ['database', 'postgresql', 'configuration'])"
            }
        },
        "required": ["claim", "evidence"]
    }
},

"DepositADR": {
    "name": "DepositADR",
    "description": "Record a BINDING architectural decision. All agents in the colony MUST follow ADRs. Use when you make a decision that affects other agents' work (framework choice, code pattern, naming convention, file structure).",
    "parameters": {
        "type": "object",
        "properties": {
            "decision": {
                "type": "string",
                "description": "The decision made (e.g., 'All API routes use /api/v1/ prefix')"
            },
            "rationale": {
                "type": "string",
                "description": "Why this decision was made"
            },
            "scope": {
                "type": "string",
                "description": "What parts of the codebase this affects (e.g., 'all API endpoints', 'database layer', 'global')"
            },
            "alternatives_rejected": {
                "type": "array",
                "items": {"type": "string"},
                "description": "Other options considered and why they were rejected"
            }
        },
        "required": ["decision", "rationale", "scope"]
    }
},

"DepositWarning": {
    "name": "DepositWarning",
    "description": "Signal a problem, risk, or concern to the colony. Use when you encounter failures, potential bugs, security issues, or design concerns.",
    "parameters": {
        "type": "object",
        "properties": {
            "description": {
                "type": "string",
                "description": "What the warning is about"
            },
            "severity": {
                "type": "string",
                "description": "How serious: 'low' (cosmetic), 'medium' (functional risk), 'high' (will break things)",
                "enum": ["low", "medium", "high"]
            },
            "affected_components": {
                "type": "array",
                "items": {"type": "string"},
                "description": "Files or modules affected"
            }
        },
        "required": ["description", "severity"]
    }
},

# ─── Workspace Tools ───

"AcquireLease": {
    "name": "AcquireLease",
    "description": "Get exclusive write access to a file. Required before using FileEdit on files that other agents might also be editing. Returns the lease or an error if the file is already locked by another agent.",
    "parameters": {
        "type": "object",
        "properties": {
            "path": {
                "type": "string",
                "description": "Relative path to the file to lock"
            }
        },
        "required": ["path"]
    }
},

"ReleaseLease": {
    "name": "ReleaseLease",
    "description": "Release your exclusive write access to a file. Call this after you're done editing a file so other agents can modify it.",
    "parameters": {
        "type": "object",
        "properties": {
            "path": {
                "type": "string",
                "description": "Relative path to the file to unlock"
            }
        },
        "required": ["path"]
    }
},

"GetProjectContext": {
    "name": "GetProjectContext",
    "description": "Get the current workspace state: file tree, active conventions, API contracts, and project structure. Use at the start of your task to understand the project.",
    "parameters": {
        "type": "object",
        "properties": {
            "include_file_tree": {
                "type": "boolean",
                "description": "Include the file tree listing. Default: true.",
                "default": True
            },
            "include_conventions": {
                "type": "boolean",
                "description": "Include active conventions and ADRs. Default: true.",
                "default": True
            }
        },
        "required": []
    }
},

"RunTests": {
    "name": "RunTests",
    "description": "Run pytest in the workspace. Returns test results including pass/fail counts, failure details, and output.",
    "parameters": {
        "type": "object",
        "properties": {
            "path": {
                "type": "string",
                "description": "Specific test file or directory to run. Omit to run all tests.",
                "default": "."
            },
            "verbose": {
                "type": "boolean",
                "description": "Show verbose output with individual test results.",
                "default": True
            }
        },
        "required": []
    }
},

}  # End TOOL_SCHEMAS
```

### 3.2 Tool Schema → ToolDefinitionSchema Conversion

```python
def get_tool_definitions(agent_type: str) -> list[ToolDefinitionSchema]:
    """
    Get tool definitions for an agent type, filtered by their tool profile (§7.3).
    Returns ToolDefinitionSchema objects ready to pass to LLMRequest.tools.
    """
    from pheromone.tools.registry import get_tool_names_for_agent
    
    allowed_tools = get_tool_names_for_agent(agent_type)
    definitions = []
    
    for tool_name in allowed_tools:
        if tool_name in TOOL_SCHEMAS:
            schema = TOOL_SCHEMAS[tool_name]
            definitions.append(ToolDefinitionSchema(
                name=schema["name"],
                description=schema["description"],
                parameters=schema["parameters"],
            ))
    
    return definitions
```

### 3.3 Phase 1 Tool Scope

For Week 1, implement these tools (11 of 17). The remaining 6 are Phase 2:

**Phase 1 (implement now):**
- FileRead, FileWrite, FileEdit, BashTool, GlobTool, GrepTool
- SenseTool, DepositKnowledge, DepositWarning
- GetProjectContext, RunTests

**Phase 2 (defer):**
- WebSearch, WebFetch (require API integration)
- DepositADR, RequestReview, CheckConventions (require review system)
- AcquireLease, ReleaseLease (leasing works internally via ToolOrchestrator; explicit agent tools deferred)
- UpdateAPIContract

---

## PART 4: CRITICAL FIXES FROM AUDIT

### Fix C4: Initial Capability Pheromone Seeding

Add to `ExecutionEngine.run()`, before the first allocation round:

```python
async def _seed_initial_capabilities(self, agents, environment):
    """
    Deposit initial CAPABILITY pheromones so the first allocation round
    has non-zero attraction scores. Without this, ACO formula produces
    0^alpha = 0 and no agent gets any task.
    """
    for agent in agents:
        for skill in agent.config.skills:
            await environment.deposit(Pheromone(
                type=PheromoneType.CAPABILITY,
                content={
                    "agent_id": agent.config.name,
                    "skill": skill,
                    "proficiency": 0.5,
                    "source": "initial_config",
                },
                strength=2.5,  # TAU_MAX * 0.5 — moderate initial confidence
                decay_rate=0.01,
                depositor_id="system",
                depositor_trust=1.0,
                tags=["capability", skill, agent.config.name],
            ))
```

### Fix C5: Discriminator Fields on Output Models

Ensure each output model has the `mode` literal field:

```python
class WorkspaceOutput(BaseModel):
    mode: Literal["workspace"] = "workspace"
    root_path: str
    files: list[FileInfo]
    entry_point: str | None = None
    # ...

class TextOutput(BaseModel):
    mode: Literal["text"] = "text"
    sections: list[TextSection]
    executive_summary: str | None = None
    # ...

class HybridOutput(BaseModel):
    mode: Literal["hybrid"] = "hybrid"
    workspace: WorkspaceOutput
    narrative: TextOutput
    # ...
```

### Fix H7: ReAct Loop Termination Logic

```python
# In LLMResponse:
@property
def is_terminal(self) -> bool:
    """True if the LLM is done AND there are no tools to execute."""
    if self.has_tool_calls:
        return False  # ALWAYS execute tools if present
    return self.stop_reason in (
        StopReason.END_TURN,
        StopReason.MAX_TOKENS,
        StopReason.STOP_SEQUENCE,
        StopReason.ERROR,
    )
```

### Fix H8: BashTool Safelist (Phase 1)

```python
BASH_ALLOWED_PREFIXES = [
    "python", "python3", "pip", "pip3", "pytest", "mypy", "ruff",
    "node", "npm", "npx", "yarn",
    "cat", "head", "tail", "wc", "sort", "uniq",
    "ls", "find", "tree", "pwd", "echo", "printf",
    "mkdir", "cp", "mv", "touch",
    "grep", "sed", "awk",  # read-only transforms
    "git",  # workspace git operations
    "curl",  # needed for API testing
]

BASH_BLOCKED_PATTERNS = [
    "rm -rf /", "rm -rf ~", "rm -rf .",
    "mkfs", "dd if=", "chmod 777",
    "> /dev/", "| sh", "| bash",
    "wget -O - |", "curl | sh",
]

def validate_bash_command(command: str) -> tuple[bool, str]:
    """Returns (is_allowed, reason)."""
    cmd_lower = command.strip().lower()
    
    for blocked in BASH_BLOCKED_PATTERNS:
        if blocked in cmd_lower:
            return False, f"Blocked pattern: {blocked}"
    
    first_word = command.strip().split()[0] if command.strip() else ""
    for prefix in BASH_ALLOWED_PREFIXES:
        if first_word == prefix or first_word.endswith("/" + prefix):
            return True, "Allowed"
    
    return False, f"Command '{first_word}' not in safelist. Allowed: {', '.join(BASH_ALLOWED_PREFIXES[:10])}..."
```

---

*This document resolves the 5 CRITICAL and 4 HIGH-priority findings from the pre-implementation audit. Combined with the architecture v2.1, 13 gap specs, system design document, and implementation roadmap, the specification is now complete for Day 1 coding.*

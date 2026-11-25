# AIRI Security Agent

**Type:** Autonomous cybersecurity agent  
**Competition context:** AIRI Universal Agentic Competition  
**Status:** Public implementation in the linked repository.

## Problem

A security-oriented coding agent must do more than issue shell commands. It needs to interpret a task, choose a workflow, use tools, observe the result, verify that the requested change or analysis is complete, and recover when execution fails — all within strict time and request budgets.

## What the agent does

- Extracts a task contract and selects a workflow.
- Uses a local OpenAI-compatible model endpoint.
- Interacts with the isolated task workspace through shell and filesystem tools.
- Supports vulnerability analysis, security patching, digital forensics, and CTF-style tasks.
- Runs tests and uses typed feedback to guide repair.
- Verifies deliverables before finishing and can enter a recovery path.
- Tracks request/time budgets and structured execution events.

## Architecture

```text
Task
  |
  v
Contract Extraction
  |
  v
Workflow Selection
  |
  v
Local LLM
  |
  v
Tool Execution
  |
  v
Observation
  |
  v
Verification
  |       \
 pass     fail
  |         |
Finish   Recovery / Repair
```

## Engineering competencies demonstrated

- Agent-loop architecture and tool orchestration.
- Task decomposition and workflow selection.
- Python async execution and subprocess/filesystem integration.
- Test-driven verification and repair loops.
- Typed error feedback instead of unstructured traceback dumping.
- Runtime controls: request limits, time budgets, output caps, and structured telemetry.
- Resilience mechanisms such as repetition detection and fallback execution.

## Code excerpt — typed agent state and verification signals

From `local_agent.py`:

```python
@dataclass
class AgentState:
    workdir: Path
    tool_calls: int = 0
    notes: dict[str, Any] = None

    def __post_init__(self) -> None:
        if self.notes is None:
            self.notes = {}
        self.call_history: dict[str, list[str]] = {}
        self.loop_strikes: int = 0
        self.activity: list[str] = []
        self.workspace_modified: bool = False
        self.pytest_all_green: bool = False
```

The implementation tracks both whether the agent modified the workspace and whether the latest test run passed. These are separate signals; a passing test suite before any change is not treated as proof that the agent fixed the task.

## Repository

[Open AIRI Security Agent source code](https://github.com/DimaDrukovskii/airi-sec-agent)

Main implementation: `local_agent.py`  
Entrypoint: `run.sh`  
Tests: `tests/`

## Stack

Python · asyncio · Pydantic AI (optional SDK-first path) · OpenAI-compatible local LLM endpoint · shell/filesystem tools · pytest

## Scope note

This is a competition-oriented autonomous agent running in an isolated environment. It should not be presented as an unrestricted production security scanner or used against systems without authorization.

# MTS Call Processing AI Agent

**Type:** Conversational AI backend / call-processing agent  
**Status:** Prototype with a basic dialog API; a separate `hermes_mts` branch explores tool calling and knowledge-base access.  
**Source:** Private repository; selected implementation excerpt is shown below.

## Problem

An incoming support call needs more than a generated answer. The system must preserve dialogue context, classify what should happen next, and record terminal outcomes such as resolution, transfer, or escalation.

## What I built

- FastAPI service for dialog processing.
- Claude-backed dialogue generation.
- Session and message-history orchestration.
- Separate action classification: `resolve`, `transfer`, or `escalate`.
- Storage of completed call transcripts and outcomes.
- A transcript-processing path suitable for integration into a telephony flow.
- Experimental `hermes_mts` branch with tool-calling, knowledge-base access, and account-status checks.

## Architecture

```text
Call / Transcript
       |
       v
 FastAPI Dialog API
       |
       v
 CallOrchestrator
   |           |
   v           v
LLM Dialog   Action Classifier
   |           |
   +-----+-----+
         |
         v
 Session / Call Storage
         |
         v
 resolve / transfer / escalate
```

## Engineering competencies demonstrated

- Multi-turn conversation state and message-history management.
- Separation of dialogue generation from workflow classification.
- Async Python service design and API boundaries.
- Persistence of completed interactions.
- Error handling and fallback behavior when action classification fails.
- Incremental agent evolution from a simple dialog API toward tool-using workflows.

## Code excerpt — dialogue orchestration

Taken from `CallOrchestrator.dialog()`:

```python
messages = session["messages"].copy() if not history else history.copy()
messages.append({"role": "user", "content": user_message})

agent_response = await self.llm.run_agent_dialog(
    messages=messages,
    caller_phone=caller_phone,
    system_prompt=AGENT_SYSTEM_PROMPT,
)

action_result = await self.llm.determine_action_from_dialog(
    messages=messages,
    agent_response=agent_response,
)
```

The orchestrator then updates the session and persists the call when the action is terminal.

## Important implementation boundary

The base `main` branch keeps active session state in process memory and expects the client to provide history when needed. This should be addressed with durable session storage and production telephony integration before presenting it as a production call-center deployment. The `hermes_mts` branch is a separate extension, not a claim that every advanced capability is already in the base API.

## Stack

Python · FastAPI · Anthropic Claude API · Supabase · async services · tool-calling (experimental branch)

## Code access

The full repository is private. The excerpt above demonstrates the real orchestration pattern; the complete implementation can be reviewed in a controlled walkthrough.

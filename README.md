# Dima Drukovskii

### AI Systems Developer · Agentic Systems · Backend Integrations

I design and build software systems where AI is one component of a larger engineering system — from agent orchestration and tool execution to CRM integrations, workflow automation, and data-intensive products.

My work focuses on architecture, reliable integrations, structured outputs, validation, state management, failure handling, and measurable system behavior.

---

## Selected engineering work

### 1. Core projects

| Project | Scope | Engineering evidence |
|---|---|---|
| [AI Sales Copilot — Bitrix24](./projects/crm-salesbrain.md) | CRM deal analysis, lead scoring, objection detection, next-best-action recommendations, and write-back to the deal timeline. | FastAPI service orchestration, Bitrix24 REST integration, Pydantic schemas, webhook auth/deduplication, **36 automated tests**. Includes real Python code excerpt. |
| [MTS Call Processing Agent](./projects/mts-call-agent.md) | Multi-turn support dialogue, action classification, call history, and storage; separate experimental branch for tool-calling and knowledge access. | FastAPI, async orchestration, Claude API, session state, resolve/transfer/escalate workflow. Includes real Python code excerpt. |
| [Polymarket Trading Research System](./projects/trading-bot.md) | BTC 5-minute market research, hypothesis evaluation, paper tracking, risk controls, and guarded execution. | TypeScript execution engine, risk guard, position lifecycle, reconciliation, fee-aware evaluation. Includes real TypeScript code excerpt. **No proven profitable edge is claimed.** |

### 2. Research, prototypes & product concepts

| Project | Scope | Status / evidence |
|---|---|---|
| [AI Lawyer — Tax Review Second Opinion](./projects/ai-lawyer.md) | Multi-agent legal/tax research and document review with source verification and deterministic checks. | Research/review pipelines; **205 tests, 97% coverage reported in the project README**. Prototype; rules not professionally validated. |
| [Delivery Grodno](./projects/delivery-grodno.md) | Vehicle-routing optimization with capacity, time windows, unloading, and shift constraints. | Hackathon prototype using FastAPI, OSRM, VROOM, React, and Leaflet; reproducible demo command included. |
| [OSIRIS — OSINT / Geospatial Intelligence](./projects/osiris-osint.md) | Product direction for a multi-source geospatial intelligence workspace. | Concept / contribution details pending confirmation. Attribution is deliberately not overstated. |

---

## Other public work

- [Agent Orchestration Framework](https://github.com/DimaDrukovskii/agent-orchestration-framework) — shared assistant core for voice and web channels, tenant knowledge bases, tool execution, human handoff, and analytics.
- [AIRI Security Agent](https://github.com/DimaDrukovskii/airi-sec-agent) — security-oriented agent workflow for vulnerability analysis, patching, forensics, and CTF tasks with verification and recovery.
- [OSIRIS repository](https://github.com/DimaDrukovskii/osiris) — linked separately from the concept page; authorship and individual contribution should be clarified before attributing the full codebase.
- [Video Automation Pipeline](https://github.com/DimaDrukovskii/videos-) — automated vertical-video workflow with voice generation, subtitles, b-roll, and quality checks.

## Technical competencies

**AI & agent engineering**
- Multi-step agent orchestration, tool calling, and workflow state.
- Research / verifier / critic patterns and evidence provenance.
- Structured LLM outputs, schema validation, and deterministic post-processing.
- Human handoff, fallback behavior, and execution boundaries.

**Backend & integrations**
- Python, FastAPI, async services, Pydantic, REST APIs.
- CRM and webhook integrations, Telegram workflows, external API clients.
- Session management, persistence, retries, and idempotency.

**Systems & data**
- TypeScript / Node.js, Docker, Redis, Supabase, SQL.
- Market-data ingestion, evaluation pipelines, risk controls.
- OSRM, VROOM, geospatial interfaces, MapLibre, WebGL.

## Code and project review

Some repositories are private. The case studies include selected implementation excerpts from the actual code where available, plus architecture, responsibilities, technical decisions, and known limitations. I can provide a guided source walkthrough or sanitized code samples without exposing credentials, customer data, or private research material.

I distinguish implemented features, prototypes, experiments, and unverified concepts rather than presenting every repository as a production deployment.

## Contact

**Email:** [Dimaai2100@gmail.com](mailto:Dimaai2100@gmail.com)

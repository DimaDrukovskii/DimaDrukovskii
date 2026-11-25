# AI Lawyer — Tax Review Second Opinion

**Type:** Multi-agent research and document-review system  
**Status:** Working research/review pipelines and deterministic checks; 205 tests, 97% coverage reported in the project README. Not a production tax-advice service.  
**Source:** Private repository.

## Problem

Marketplace sellers need a way to independently review accounting work and identify possible tax discrepancies before filing. A language model alone is not reliable enough to calculate tax or decide which legal sources should be trusted.

## What I designed and implemented

The system separates two workflows:

1. **Knowledge research:** parallel research across tax topics, independent verification, criticism of gaps, and promotion of supported findings into a versioned knowledge base.
2. **Client review:** intake of documents, extraction of figures, deterministic calculations and cross-checks, followed by a report with findings and questions for the accountant.

## Architecture

```text
RESEARCH PIPELINE
Research zones
   -> parallel researchers
   -> independent source verifier
   -> completeness critics
   -> versioned knowledge base

CLIENT REVIEW PIPELINE
Client documents
   -> intake / extraction
   -> deterministic code checks
   -> judge using trusted knowledge
   -> findings + questions for accountant
```

## Engineering competencies demonstrated

- Multi-agent orchestration with distinct researcher, verifier, critic, and reviewer roles.
- Evidence provenance and trust gating for knowledge-base promotion.
- Separation of probabilistic extraction from deterministic arithmetic.
- Fail-closed review behavior when data or rules are missing.
- Versioned research artifacts and repeatable testable workflows.
- Provider abstraction for LLM and search integrations.

## Core design rules

- A source is not trusted merely because an agent cites it; the verification workflow must actually open and inspect it.
- Arithmetic and deterministic reconciliations belong in code, not in a language-model response.
- Missing evidence produces an explicit “cannot verify” finding, not a false “everything is correct”.

## Example workflow contract

```text
extract(document) -> normalized figures
run_checks(figures, verified_rules) -> check results
judge(check results, trusted knowledge) -> findings
render_report(findings) -> accountant questions + review report
```

This is an architectural contract, not a verbatim source-code excerpt.

## Status and limitations

- 205 tests and 97% coverage are reported by the repository.
- Provider request/response formats were checked against documentation fixtures; live API execution was not yet completed.
- Tax rules and checklists remain drafts and have not been professionally validated by a practicing tax consultant.
- Real-world PDF/XLSX extraction and marketplace-report reconciliation remain incomplete.

This is a technical prototype and second-opinion workflow, not a substitute for a qualified accountant or tax lawyer.

## Stack

Python · LLM provider abstraction · web search tools · FastAPI / CLI · deterministic validation · automated tests

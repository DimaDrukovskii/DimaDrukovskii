# Bitrix24 AI Sales Copilot

**Type:** CRM-integrated AI sales assistant  
**Status:** MVP V0–V6 implemented. README records 36 passing automated tests and end-to-end checks against a live portal and containerized test environment.  
**Source:** Private repository; real service code excerpt included below.

## Problem

Sales managers often have to reconstruct deal context from long CRM timelines. That makes it harder to identify objections, assess deal health, and decide what to do next.

## What I built

- Bitrix24 REST client for deals and timeline comments.
- FastAPI endpoints for manual analysis and CRM webhooks.
- Conversation normalization with speaker attribution.
- LLM analysis returning a strict structured result.
- Pydantic validation of model output.
- Human-readable analysis rendered back into the deal timeline.
- Webhook authentication and duplicate-event cooldown.

## Architecture

```text
Bitrix24 CRM
    |  webhook / manual request
    v
FastAPI
    |
    v
DealAnalyzerService
   /              \
  v                v
BitrixClient     AIAnalyzer
  |                |
  |          structured output
  |          + Pydantic validation
  |                |
  +-------+--------+
          |
          v
   Timeline Comment
          |
          v
      Bitrix24 CRM
```

## Capabilities

- Deal summary.
- Lead score and temperature.
- Customer objection detection.
- Next Best Action recommendation.
- Suggested reply to the customer.
- Deal risk level and explanation.

## Code excerpt — end-to-end service orchestration

Taken from `DealAnalyzerService.analyze_deal()`:

```python
async def analyze_deal(self, deal_id: int) -> AnalyzeResult:
    deal = await self._bitrix.get_deal(deal_id)
    timeline = await self._bitrix.get_timeline(deal_id)

    context = build_context(deal, timeline)
    analysis = await self._analyzer.analyze(context)

    comment = render_comment(analysis)
    comment_id = await self._bitrix.add_timeline_comment(deal_id, comment)

    return AnalyzeResult(
        deal_id=deal_id,
        analysis=analysis,
        comment_created=True,
        comment_id=comment_id,
    )
```

This shows the key engineering boundary: CRM data retrieval, context construction, AI analysis, and CRM write-back are separate responsibilities.

## Engineering competencies demonstrated

- Third-party REST API integration.
- Event-driven backend design and webhook security.
- Domain modeling and conversation normalization.
- Structured LLM outputs with schema validation.
- Idempotency / duplicate-event protection.
- Automated testing of API, service, and failure paths.

## Status and limitations

The MVP is implemented and tested. It is not represented here as a deployed production system for an external customer's CRM. A customer rollout still requires access checks, field and pipeline mapping, webhook configuration, and acceptance testing against that customer's Bitrix24 portal.

## Stack

Python 3.12 · FastAPI · Pydantic v2 · httpx · Bitrix24 REST API · OpenAI-compatible LLM API · Docker · Pytest

## Code access

The full repository is private. This page includes a real service excerpt; source-level review can be arranged without disclosing credentials or customer data.

# Polymarket Trading Research & Execution System

**Type:** Quantitative research platform + guarded execution engine  
**Status:** Research / paper-first system. No strategy is currently claimed to have a proven positive edge.  
**Source:** Private repository; a real implementation excerpt is included below.

## Problem

A short-horizon trading bot is not useful merely because it predicts a direction. It must establish whether a signal has positive expected value after fees, survive out-of-sample evaluation, and refuse execution when market data or risk conditions are unsafe.

## What I built

- Market-data ingestion for BTC 5-minute Polymarket markets and supporting exchange data.
- Prediction and observation pipeline with persistent evaluation records.
- Hypothesis workflow with preregistered criteria and separate development / holdout data.
- Fee-aware evaluation, paper trackers, and trade lifecycle accounting.
- Execution boundary separated from risk checks.
- Position limits, daily-loss protection, stale-order-book checks, duplicate-market protection, and recovery/reconciliation paths.
- Paper mode by default; live execution requires explicit configuration and credentials.

## Architecture

```text
Market Data (Polymarket CLOB + exchange feed)
                 |
                 v
       Feature / Prediction Layer
                 |
                 v
       Evaluation & Agent Gate
                 |
                 v
           Risk Guard
           /       \
      reject       allow
        |             |
       HOLD       Executor
                      |
                 Trade Ledger
             (local log + Supabase)
```

## Engineering competencies demonstrated

- Quantitative research design: preregistration, holdout discipline, transaction-cost modelling, and statistical evaluation.
- TypeScript backend architecture and separation of prediction, risk, and execution responsibilities.
- Stateful execution: open / pending-close / closed positions, partial fills, settlement reconciliation.
- Fault handling: retries for transient persistence errors, fail-closed behavior, and kill-switch logic.
- Honest evaluation: negative results are retained rather than tuned away.

## Code excerpt — fail-closed risk gate

This excerpt is from the implemented `LiveTrader` risk path:

```ts
private guardVeto(requireFreshness: boolean, dataAsOfMs?: number | null): string | null {
  try {
    const decision = this.guard.evaluate({
      live: this.liveMode,
      nowMs: Date.now(),
      realizedPnlTotalUsd: this.realizedPnlTotal(),
      requireFreshness,
      dataAsOfMs,
      apiErrorStreak: this.apiErrorStreak,
    });
    return decision.allow
      ? null
      : `HOLD | risk guard: ${decision.rejectReasons.join(", ")}`;
  } catch (error) {
    return `HOLD | risk guard: guard_error`;
  }
}
```

The production implementation also records the underlying rejection reason and preserves detailed error context.

## Current result and limitations

The project has not established a strategy with a proven edge. The system's value is the research discipline and guarded execution infrastructure—not a claim of profitability. It is paper-first and intended for experimentation.

## Stack

TypeScript · Node.js · Polymarket CLOB · exchange market data · Supabase · JSONL · automated tests

## Code access

The full repository is private. This page publishes a small implementation excerpt; a deeper code walkthrough can be arranged without exposing credentials or private research data.

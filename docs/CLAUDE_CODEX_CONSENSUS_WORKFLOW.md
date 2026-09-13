# Claude ↔ Codex Consensus Workflow for Non-Trivial Engineering

**Status:** proposed cross-project Hermes orchestration rule; dogfood on Hardy/Jellyfish before promotion into the core operating contract.
**Date:** 2026-09-13

## Purpose

Use complementary model strengths before expensive implementation begins.

The target workflow is not an open-ended multi-agent debate. It is a bounded **plan-review-consensus gate**:

```text
Human goal
  -> Hermes state/reuse reconciliation
  -> draft execution plan
  -> Claude Code domain/architecture review
  -> revised plan
  -> Codex independent technical review
  -> bounded reconciliation if needed
  -> PLAN_CONSENSUS_PASS
  -> Codex implementation
  -> evidence/tests/runtime
  -> optional Claude final review for high-impact work
  -> Human gate only where genuinely required
```

Hermes remains the orchestrator. It does not become the substantive coder.

## Why this exists

Recent work showed a repeatable complementarity:

- Claude Code is often strong at domain-specific architecture, ecosystem knowledge, alternative approaches, and catching API/representation mistakes before implementation.
- Codex is the canonical implementation executor and is strong at repository-level execution, code changes, tests, runtime diagnosis, and evidence production.
- A single model can confidently miss a bad assumption. Two independent reviews before execution are cheaper than hours of downstream debugging when the task is non-trivial.

This workflow extends, rather than replaces, the cross-project outcome-first / research-reuse gate.

## Trigger — when consensus review is required

Use this workflow for non-trivial/high-impact engineering, especially:

- new coding projects or new major execution slices;
- material architecture or representation changes;
- unfamiliar or poorly documented APIs/runtimes;
- native-GUI / automation / media pipelines;
- multi-tool integrations;
- risky refactors or migrations;
- tasks expected to consume substantial executor quota;
- any task entering a third materially similar attempt or a >20 minute low-evidence debugging loop.

Do **not** pay the consensus tax for trivial work such as typo fixes, tiny known-safe config changes, mechanical renames, or a narrowly proven one-line repair.

## Roles

### Hermes / Jarvis — orchestrator only

Hermes owns:

- current-state reconciliation;
- outcome-first / research-reuse gate enforcement;
- assembling the smallest useful plan and evidence packet;
- invoking Claude Code and Codex through their supported Hermes CLI skills;
- tracking reviewer findings in a structured issue matrix;
- deciding whether consensus is reached according to the rules below;
- enforcing scope, stop rules, process ownership and Human gates.

Hermes does **not** implement the product code while this workflow is active.

### Claude Code — domain / architecture reviewer

Claude receives the current sources, plan, acceptance criteria and relevant official documentation/references.

Claude should focus on:

- whether the proposed technical problem needs to exist at all;
- domain-specific correctness;
- official API / parameter / runtime semantics;
- simpler or more native representations;
- missing failure modes;
- overengineering;
- whether the plan is implementable and testable;
- concrete corrections to the plan, not speculative rewrites.

Claude's planning review is read-only unless explicitly assigned a separate implementation task.

### Codex GPT-5.6 Sol HIGH — independent reviewer, then executor

Before coding, Codex independently reviews the revised plan and Claude's findings against the repository and evidence.

After `PLAN_CONSENSUS_PASS`, Codex becomes the sole default implementation executor for that slice.

Default executor policy remains:

- model: `gpt-5.6-sol`;
- reasoning: `high`;
- sandbox: `workspace-write`;
- approval: `on-request`;
- broader/native-host exceptions only when fresh evidence proves they are necessary.

## Review output contract

Both reviewers must return the same compact structure:

```text
VERDICT: APPROVE | REQUEST_CHANGES | BLOCKED_EVIDENCE

CRITICAL:
- ...

IMPORTANT:
- ...

OPTIONAL:
- ...

ASSUMPTIONS_TO_VERIFY:
- ...

PROPOSED_PLAN_CHANGES:
- ...

SOURCES/EVIDENCE:
- ...
```

A reviewer must distinguish a documented/runtime fact from an inference.

## Consensus gate

`PLAN_CONSENSUS_PASS` requires:

1. Claude = `APPROVE` or all Claude CRITICAL/IMPORTANT findings are resolved in the revised plan;
2. Codex = `APPROVE` or all Codex CRITICAL/IMPORTANT findings are resolved;
3. no unresolved contradiction in acceptance criteria, safety, architecture, API/runtime facts, or source-of-truth state;
4. the plan states the smallest evidence-bearing first slice and its STOP condition;
5. executor permissions and process ownership rules are explicit where relevant.

Optional/nice-to-have disagreement does not block execution.

## Bounded reconciliation — no infinite ping-pong

If Claude and Codex disagree materially:

1. Hermes creates an issue matrix with each disputed claim, evidence and impact.
2. Hermes resolves purely factual disputes by checking the strongest available source (current official docs, repository/runtime evidence).
3. Remaining material disputes get **one targeted rebuttal round**:
   - Claude sees Codex's specific objection and evidence;
   - Codex sees Claude's specific response/evidence.
4. Maximum: **two total review/reconciliation rounds** before escalation.
5. If a material disagreement remains, stop with `HUMAN_REQUIRED_DECISION` and present only the unresolved decision, not the whole transcript.

Do not let two models debate wording after the implementation decision is already clear.

## Plan freeze

When consensus passes, Hermes freezes an execution packet containing:

- goal;
- exact scope / non-scope;
- current repo/branch/worktree state;
- selected architecture;
- acceptance criteria;
- relevant verified API/runtime facts;
- safety/process constraints;
- first evidence gate;
- STOP condition;
- plan version/hash or timestamp.

Codex executes against that packet. New discoveries may revise the plan, but material revisions must re-enter review rather than silently drifting.

## Execution and review after coding

During implementation:

- Codex implements and tests.
- Hermes monitors evidence and enforces the frozen scope.
- Claude is not used as a parallel coder by default.

For high-impact or ambiguous results, run a final independent Claude review of the diff/runtime evidence before merge/product promotion. Small proven fixes may skip this final review.

A reviewer finding must go back to Codex for repair; Hermes does not silently fix it itself.

## Relationship to native Hermes features

Prefer existing Hermes capabilities over building a new supervisor core:

- bundled `claude-code` skill for Claude Code CLI;
- bundled `codex` skill for Codex CLI;
- Hermes parent session as the sequential orchestrator;
- `/review` for independent post-work review where that route is appropriate;
- `plan` / subagent-driven-development skills where useful for internal task structure.

The first implementation of this protocol should be an orchestration/skill contract, not a new daemon, database or message bus.

## Efficiency rules

- Review the **plan**, not every trivial command.
- Pass reviewers concise source pointers and evidence instead of entire chat history.
- Require structured deltas, not rewritten essays.
- Prefer official docs and fresh runtime evidence over model memory.
- If Claude already proves a concrete API fact, Codex should verify the high-impact facts, not repeat broad research from scratch.
- If both models agree the problem can be removed or simplified, stop preserving the old implementation assumption.

Success metric: **reliable result per minute of human attention and executor quota**.

## First dogfood: Hardy/Jellyfish

Use the current Hardy Center slice as the first real trial:

1. Reconcile the existing clean-room worktree and current TouchDesigner standard.
2. Feed the current Center plan and Claude's proposed `bootstrap.py` / `verify.py` to Claude for domain review.
3. Feed Claude's corrected plan plus the actual canonical carrier contract to Codex for independent review.
4. Resolve material mismatches before any new product-code changes.
5. Codex executes the agreed minimal Center slice.
6. Stop at the current product gate (`HUMAN_VISUAL_REQUIRED`).

Do not expand the dogfood into Approach, audio, multi-creature architecture or projection mapping before the Center gate passes.

## Promotion criterion

After one or two real projects show that this protocol reduces rework without creating review-loop overhead:

- promote the rule into `JARVIS_OPERATING_CONTRACT.md`;
- optionally package it as a dedicated Hermes skill;
- keep project-specific domain rules in specialist repositories rather than copying them into this cross-project workflow.

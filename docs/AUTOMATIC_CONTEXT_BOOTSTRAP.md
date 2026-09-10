# Automatic Context Bootstrap for Hermes/Jarvis

**Status:** canonical design for making mandatory standards available without repeating long prompts.
**Last updated:** 2026-09-10.

## Goal

The operator should not have to paste the standard hierarchy into every `/goal`.

Hermes should enter non-trivial technical work with a small, automatically injected bootstrap rule and then retrieve the current canonical GitHub state before execution.

## Hermes-native context mechanisms

Hermes automatically supports two relevant context layers:

1. **Global `SOUL.md`**
   - loaded from the active Hermes profile/home at session start;
   - always independent of project context;
   - appropriate for stable global role/routing rules, not project implementation details.

2. **Project context file**
   - `.hermes.md` / `HERMES.md` has highest project-context priority;
   - `AGENTS.md` is also supported and hierarchical;
   - project context is discovered from the working directory / repository context.

Therefore the mandatory standards should be wired through these native surfaces, not repeatedly embedded in user goals.

## Required global bootstrap rule

The active Jarvis/Hermes bot profile should contain a short durable instruction in its `SOUL.md` equivalent to:

```text
For every non-trivial technical/project task, begin in orchestration/state-reconciliation mode.
Read the canonical bootstrap rules from lagisela/AI_HERMES_STANDARD/BOT_BOOTSTRAP.md on current GitHub main before substantive execution.
Treat current GitHub/default-branch state and fresh runtime evidence as authoritative over stale chat history.
Hermes is orchestrator only; delegate substantive technical execution according to the operating contract.
If a specialist standard applies (for example TouchDesigner), load it before delegating technical work.
Before bespoke implementation or a third same-class debug attempt, apply the canonical research/reuse gate instead of continuing blind trial-and-error.
```

Keep this global snippet small. Do not paste entire project standards into `SOUL.md`.

## Required project bootstrap rule

Every long-lived technical project repository should contain a small `.hermes.md` (preferred for Hermes-specific routing) or `AGENTS.md` that points to:

- `lagisela/holodeck-dev-standard/AGENTS.md` + `STANDARD.md` + `RESEARCH_REUSE.md`;
- `lagisela/AI_HERMES_STANDARD/BOT_BOOTSTRAP.md` when Hermes is orchestrating;
- specialist standard(s), e.g. `lagisela/AI_Touchdesigner_Standard/README.md` and `docs/TD_RUNTIME_FAILURE_MODES.md` for TouchDesigner work;
- the project's own `CURRENT_EXECUTION.md`.

The project file should contain pointers and invariants, not copies of whole standards.

## Fail-closed preflight

Before a non-trivial technical executor is launched, Hermes MUST establish:

1. current GitHub/default-branch state for the applicable standards;
2. current project execution pointer/gate;
3. applicable specialist runtime lessons;
4. applicable research/reuse gate and whether a reuse scan is required before bespoke implementation;
5. executor route/model/sandbox/ownership policy.

If a mandatory source cannot be read, do not silently substitute old chat context or a stale local checkout. Report the state-reconciliation problem or use an approved alternate retrieval path.

## Context economy

The bootstrap chain is intentionally pointer-based:

```text
SOUL (short global invariant)
    -> BOT_BOOTSTRAP.md
    -> holodeck-dev-standard/RESEARCH_REUSE.md when applicable
    -> applicable specialist standard
    -> project .hermes.md / CURRENT_EXECUTION
    -> one bounded gate
```

Do not inject full histories or large handover prompts when canonical files can be retrieved by the executor.

## Fresh-session behavior

Changes to `SOUL.md` are cleanly applied on a new session. Existing long/compressed sessions may retain old prompt state.

After materially changing bootstrap/governance rules, prefer a fresh session and verify `/profile`, `/status`, and `/goal status`.

## Implementation status

The GitHub documents define the canonical rule. A one-time local Hermes profile change is still required to place the short global bootstrap rule into the active bot/profile's `SOUL.md` (or equivalent Custom SOUL field in Hermes Desktop).

GitHub alone cannot force a model to read an external file unless the Hermes profile/project context instructs it to do so. Once the profile rule is installed, the operator should not need to repeat the standard read-chain in each goal.

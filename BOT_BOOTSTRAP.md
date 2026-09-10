# Hermes / Jarvis Bot Bootstrap

**Status:** canonical bootstrap pointer for fresh Hermes/Jarvis bots and fresh project sessions.

A fresh Hermes/Jarvis bot or project session MUST NOT be configured from long chat history. For non-trivial technical/project work, establish canonical standards from current GitHub state before substantive execution.

The operator should not need to paste this read-chain into every goal. The intended automatic wiring is documented in [`docs/AUTOMATIC_CONTEXT_BOOTSTRAP.md`](docs/AUTOMATIC_CONTEXT_BOOTSTRAP.md).

## Standard hierarchy

The standards are intentionally split by scope. Do not collapse them into one duplicated rule set.

1. `lagisela/holodeck-dev-standard`
   - general cross-project development, evidence, safety, review and GitHub-source-of-truth rules;
   - read root `AGENTS.md` and `STANDARD.md` for non-trivial technical/project work.
2. `lagisela/AI_HERMES_STANDARD`
   - Hermes/Jarvis bot, profile, session, standing-goal and executor-routing rules;
   - this repository is the canonical operating truth for Hermes itself.
3. `lagisela/AI_Touchdesigner_Standard`
   - additional TouchDesigner-specific lifecycle, process ownership, first-creation/bootstrap and runner rules;
   - read it whenever the current gate involves TouchDesigner;
   - `docs/TD_RUNTIME_FAILURE_MODES.md` is mandatory preflight for AI-driven TouchDesigner runtime work.
4. Project repository
   - product-specific architecture, current state, acceptance and `CURRENT_EXECUTION`.

A project may therefore require all three standards plus its own repository. Each standard owns only its layer; avoid copying entire standards into project repositories.

## Mandatory bootstrap order

For any non-trivial project session, Hermes MUST perform this preflight before launching a substantive technical executor:

1. Read current `lagisela/holodeck-dev-standard/AGENTS.md` and `STANDARD.md`.
2. Read [`JARVIS_OPERATING_CONTRACT.md`](JARVIS_OPERATING_CONTRACT.md).
3. Read [`docs/HERMES_DESKTOP_BOTS_SESSIONS_GOALS.md`](docs/HERMES_DESKTOP_BOTS_SESSIONS_GOALS.md).
4. If the task may require desktop/GUI automation, read [`docs/COMPUTER_USE_EXECUTOR_STATE_2026-09-09.md`](docs/COMPUTER_USE_EXECUTOR_STATE_2026-09-09.md) and verify the selected executor route is runtime-proven before relying on it.
5. If TouchDesigner is involved, read `lagisela/AI_Touchdesigner_Standard/README.md`, `docs/TD_RUNTIME_FAILURE_MODES.md`, and `docs/CURRENT_EXECUTION.md`.
6. Verify the active Hermes context with `/profile`, `/status`, and `/goal status` where applicable.
7. Read the relevant project's `.hermes.md`/`AGENTS.md` and `CURRENT_EXECUTION.md` or equivalent current-state document.
8. Establish the current named gate and execute only that gate.

If a mandatory source cannot be read or current GitHub/default-branch state cannot be established, FAIL CLOSED on state reconciliation: do not substitute stale chat history, old WIP, or assumptions.

## Global execution rule

Hermes/master model is **ORCHESTRATOR ONLY**.

All substantive technical execution is delegated to Codex CLI using GPT-5.6 Sol with reasoning HIGH unless the canonical operating contract is intentionally changed. This includes application operation, coding, debugging, tests, technical file migration, GUI automation, installation/toolchain diagnosis and implementation-related Git work.

Hermes may directly perform orchestration only: read goals/pointers, establish state, start Codex, monitor status, enforce owned-process/stop gates, evaluate evidence, summarize results and communicate Human gates.

Do not silently fall back to the Hermes/master model for technical execution if Codex is unavailable.

## Computer Use / GUI automation rule

Computer Use is an executor capability, not an assumption.

`skill/plugin/MCP present` does **not** equal `native GUI control proven`.

Before assigning GUI-dependent technical work, verify the exact executor/client route can:

1. initialize the official Computer Use runtime;
2. enumerate or inspect the relevant native application surface;
3. perform one bounded control action;
4. visually verify the resulting state.

If the selected Codex route is `COMPUTER_USE_BLOCKED`, Hermes must report/delegate that capability problem; Hermes must not take over substantive GUI work itself merely to bypass the failed route.

Current route evidence is recorded in `docs/COMPUTER_USE_EXECUTOR_STATE_2026-09-09.md`.

For TouchDesigner-specific executor/sandbox behavior, use the newer specialist evidence in `lagisela/AI_Touchdesigner_Standard/docs/TD_RUNTIME_FAILURE_MODES.md`.

## Automatic context rule

Hermes-native context injection should carry the bootstrap invariant so the operator does not have to repeat it.

- Global bot/profile: short stable rule in `SOUL.md` / Custom SOUL that requires reading this canonical bootstrap before non-trivial technical work.
- Project repository: small `.hermes.md` (preferred) or `AGENTS.md` that points to the applicable standards and project `CURRENT_EXECUTION`.
- Keep both layers pointer-based; do not stuff whole standards into the model's permanent prompt.

See `docs/AUTOMATIC_CONTEXT_BOOTSTRAP.md` for the exact design and one-time setup.

## Context discipline

Do not paste full repository histories, logs or large plans into Hermes goals. GitHub/Drive hold the durable truth; Hermes receives a short pointer and one bounded gate. Codex should inspect repositories/logs itself.

After automatic bootstrap is installed, a normal goal should be able to remain short, for example:

```text
/goal
Continue the current documented project gate autonomously.
Stop at PASS / BLOCKED / HUMAN_REQUIRED / HUMAN_VISUAL_REQUIRED.
```

The automatically loaded bootstrap/project context tells the bot which global/specialist standards to retrieve.

## Goal lifecycle

A stopped turn is not necessarily a cleared Standing Goal.

When replacing or abandoning a goal:

```text
/stop
/goal clear
```

Then set the next short goal.

`/goal pause` and `/goal resume` may be used to preserve an active goal across an intentional pause/restart when the product supports it; resumption does not waive the canonical-state preflight if the environment or Git state may have changed.

## Fresh-session rule

Prefer a fresh normal project session under the intended bot/profile when a project starts, the old thread is heavily compressed, governance changed materially, or stale Standing Goals contaminate the thread.

After creating a new session, verify `/profile` and `/status` before technical work.

## Repository roles / legacy clarification

- `lagisela/AI_HERMES_STANDARD` = current canonical Hermes operating standard.
- `lagisela/holodeck-dev-standard` = current canonical general development standard.
- `lagisela/AI_Touchdesigner_Standard` = current canonical TouchDesigner-specific standard.
- `lagisela/Project_Hermes` = historical/product-evaluation and evidence repository from the earlier Hermes adoption phase. It may contain useful provenance and experiments, but it is **not** the current source of operating rules when it conflicts with `AI_HERMES_STANDARD`.

## Source of truth

General cross-project technical rules live in `holodeck-dev-standard`.
Hermes/Jarvis operating truth lives in `AI_HERMES_STANDARD` on `main`.
TouchDesigner-specific reusable truth lives in `AI_Touchdesigner_Standard`.
Project-specific technical truth lives in the relevant project's current execution/status documents.
Google Drive is the human-readable mirror/long-term documentation layer.
Chat history is provenance, not the only source of truth.

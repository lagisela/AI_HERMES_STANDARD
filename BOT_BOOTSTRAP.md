# Hermes / Jarvis Bot Bootstrap

**Status:** canonical bootstrap pointer for fresh Hermes/Jarvis bots and fresh project sessions.

A fresh Hermes/Jarvis bot or project session should not be configured from long chat history. Read the canonical standards from GitHub, then read the current project's execution pointer.

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
   - read it whenever the current gate involves TouchDesigner.
4. Project repository
   - product-specific architecture, current state, acceptance and `CURRENT_EXECUTION`.

A project may therefore require all three standards plus its own repository. Each standard owns only its layer; avoid copying entire standards into project repositories.

## Mandatory bootstrap order

For any non-trivial project session:

1. Read `lagisela/holodeck-dev-standard/AGENTS.md` and `STANDARD.md`.
2. Read [`JARVIS_OPERATING_CONTRACT.md`](JARVIS_OPERATING_CONTRACT.md).
3. Read [`docs/HERMES_DESKTOP_BOTS_SESSIONS_GOALS.md`](docs/HERMES_DESKTOP_BOTS_SESSIONS_GOALS.md).
4. If the task may require desktop/GUI automation, read [`docs/COMPUTER_USE_EXECUTOR_STATE_2026-09-09.md`](docs/COMPUTER_USE_EXECUTOR_STATE_2026-09-09.md) and verify the selected executor route is runtime-proven before relying on it.
5. If TouchDesigner is involved, read the entry/current documents in `lagisela/AI_Touchdesigner_Standard`, especially `docs/CURRENT_EXECUTION.md` for infrastructure gates.
6. Verify the active Hermes context with:
   - `/profile`
   - `/status`
   - `/goal status`
7. Read the relevant project's `CURRENT_EXECUTION.md` or equivalent current-state document.
8. Execute only the current named gate.

## Global execution rule

Hermes/Qwen is **ORCHESTRATOR ONLY**.

All substantive technical execution is delegated to Codex CLI using GPT-5.6 Sol with reasoning HIGH. This includes application operation, coding, debugging, tests, technical file migration, GUI automation, installation/toolchain diagnosis and implementation-related Git work.

Hermes may directly perform orchestration only: read goals/pointers, start Codex, monitor status, enforce owned-process/stop gates, summarize results and communicate Human gates.

Do not silently fall back to Hermes/Qwen for technical execution if Codex is unavailable.

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

## Context discipline

Do not paste full repository histories, logs or large plans into Hermes goals. GitHub/Drive hold the durable truth; Hermes receives a short pointer and one bounded gate. Codex should inspect repositories/logs itself.

Recommended goal shape:

```text
/goal

Read:
lagisela/AI_HERMES_STANDARD/BOT_BOOTSTRAP.md
<project repo>/<CURRENT_EXECUTION path>

Execute only the current gate.
Stop at PASS / BLOCKED / HUMAN_REQUIRED / HUMAN_VISUAL_REQUIRED.
```

The bootstrap file itself tells the bot which global/specialist standards must also be read.

## Goal lifecycle

A stopped turn is not necessarily a cleared Standing Goal.

When replacing or abandoning a goal:

```text
/stop
/goal clear
```

Then set the next short goal.

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

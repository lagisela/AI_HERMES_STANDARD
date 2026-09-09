# Hermes / Jarvis Bot Bootstrap

**Status:** canonical bootstrap pointer for fresh bots and fresh sessions.

A fresh Hermes/Jarvis bot or project session should not be configured from long chat history. Read the canonical operating rules from GitHub and then read the current project's execution pointer.

## Mandatory bootstrap order

1. Read [`JARVIS_OPERATING_CONTRACT.md`](JARVIS_OPERATING_CONTRACT.md).
2. Read [`docs/HERMES_DESKTOP_BOTS_SESSIONS_GOALS.md`](docs/HERMES_DESKTOP_BOTS_SESSIONS_GOALS.md).
3. Verify the active Hermes context with:
   - `/profile`
   - `/status`
   - `/goal status`
4. Read the relevant project's `CURRENT_EXECUTION.md` or equivalent current-state document.
5. Execute only the current named gate.

## Global execution rule

Hermes/Qwen is **ORCHESTRATOR ONLY**.

All substantive technical execution is delegated to Codex CLI using GPT-5.6 Sol with reasoning HIGH. This includes application operation, coding, debugging, tests, technical file migration, GUI automation, installation/toolchain diagnosis and implementation-related Git work.

Hermes may directly perform orchestration only: read goals/pointers, start Codex, monitor status, enforce owned-process/stop gates, summarize results and communicate Human gates.

Do not silently fall back to Hermes/Qwen for technical execution if Codex is unavailable.

## Context discipline

Do not paste full repository histories, logs or large plans into Hermes goals. GitHub/Drive hold the durable truth; Hermes receives a short pointer and one bounded gate.

Recommended goal shape:

```text
/goal

Read:
lagisela/AI_HERMES_STANDARD/BOT_BOOTSTRAP.md
<project repo>/<CURRENT_EXECUTION path>

Execute only the current gate.
Stop at PASS / BLOCKED / HUMAN_REQUIRED / HUMAN_VISUAL_REQUIRED.
```

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

## Source of truth

General Hermes/Jarvis operating truth lives in this repository on `main`.
Project-specific technical truth lives in the relevant project's current execution/status documents.
Chat history is provenance, not the only source of truth.

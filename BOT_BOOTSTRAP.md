# Hermes / Jarvis Bot Bootstrap

**Status:** canonical bootstrap pointer for fresh Hermes/Jarvis bots and fresh project sessions.

A fresh Hermes/Jarvis bot or project session MUST NOT be configured from long chat history. For non-trivial technical/project work, establish canonical standards from current GitHub state before substantive execution.

The operator should not need to paste this read-chain into every goal. The intended automatic wiring is documented in [`docs/AUTOMATIC_CONTEXT_BOOTSTRAP.md`](docs/AUTOMATIC_CONTEXT_BOOTSTRAP.md).

## HARD GATE — canonical means current merged default-branch state

For Hermes orchestration, a rule/state change becomes canonical only when it exists on the repository's current merged default branch (`main` unless documented otherwise).

Issues, PRs, feature branches, local worktrees, delegation logs, Memory, chat and Drive notes are evidence/WIP, not authoritative current state by themselves.

Before using a local `CURRENT_EXECUTION.md`, rule file or blocker report as truth, Hermes MUST establish current remote default-branch state through an approved route.

Preferred retrieval order:

1. GitHub connector/API/default-branch fetch;
2. authenticated `git fetch` and exact reconciliation against `origin/<default>`;
3. another approved GitHub retrieval route.

If raw GitHub/web extraction fails, **try another approved GitHub route**. Do not immediately substitute an arbitrary local checkout.

A local file is authoritative only when fresh reconciliation proves it matches current remote default-branch state. If that cannot be established, FAIL CLOSED on state reconciliation.

Fresh runtime PASS + current merged project state overrides stale historical blockers. Do not resurrect a resolved TouchDesigner license/API/runtime/process/product blocker from an old local file or old issue comment.

Important reusable governance changes must also be promoted into the relevant front-door file (`holodeck-dev-standard/AGENTS.md`, this `BOT_BOOTSTRAP.md`, or equivalent) and merged to default branch; burying them only in an issue or deep document is insufficient.

## Standard hierarchy

The standards are intentionally split by scope. Do not collapse them into one duplicated rule set.

1. `lagisela/holodeck-dev-standard`
   - general cross-project development, evidence, safety, review and GitHub-source-of-truth rules;
   - read root `AGENTS.md`, `STANDARD.md`, and `RESEARCH_REUSE.md` for non-trivial technical/project work.
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

1. Establish current merged default-branch identity for the applicable repositories; do not trust an unreconciled local checkout.
2. Read current `lagisela/holodeck-dev-standard/AGENTS.md`, `STANDARD.md`, and `RESEARCH_REUSE.md`.
3. Read [`JARVIS_OPERATING_CONTRACT.md`](JARVIS_OPERATING_CONTRACT.md).
4. Read [`docs/HERMES_DESKTOP_BOTS_SESSIONS_GOALS.md`](docs/HERMES_DESKTOP_BOTS_SESSIONS_GOALS.md).
5. If the task may require desktop/GUI automation, read [`docs/COMPUTER_USE_EXECUTOR_STATE_2026-09-09.md`](docs/COMPUTER_USE_EXECUTOR_STATE_2026-09-09.md) and verify the selected executor route is runtime-proven before relying on it.
6. If TouchDesigner is involved, read `lagisela/holodeck-dev-standard/TOUCHDESIGNER_RUNTIME.md`, `lagisela/AI_Touchdesigner_Standard/README.md`, `docs/TD_RUNTIME_FAILURE_MODES.md`, and `docs/CURRENT_EXECUTION.md`.
7. Verify the active Hermes context with `/profile`, `/status`, and `/goal status` where applicable.
8. Read the relevant project's `.hermes.md`/`AGENTS.md` and current merged `CURRENT_EXECUTION.md` or equivalent current-state document.
9. Establish the current named gate and execute only that gate.

If a mandatory source cannot be read or current GitHub/default-branch state cannot be established, FAIL CLOSED on state reconciliation: do not substitute stale chat history, old WIP, unreconciled local files, or assumptions.

If canonical state already answers a routine setup question (project, source asset, launcher/lifecycle, active lane, previous PASS), do not ask the operator to restate it. Ask only when fresh evidence contradicts the canonical state or a genuine product/human decision is missing.

## Global execution rule

Hermes/master model is **ORCHESTRATOR ONLY**.

All substantive technical execution is delegated to Codex CLI using GPT-5.6 Sol with reasoning HIGH unless the canonical operating contract is intentionally changed. This includes application operation, coding, debugging, tests, technical file migration, GUI automation, installation/toolchain diagnosis and implementation-related Git work.

Hermes may directly perform orchestration only: read goals/pointers, establish state, start Codex, monitor status, enforce owned-process/stop gates, evaluate evidence, summarize results, initiate bounded research/reuse gates and communicate Human gates.

Do not silently fall back to the Hermes/master model for technical execution if Codex is unavailable.

## Research / reuse escalation rule

Hermes MUST prevent blind technical trial-and-error loops.

For any new non-trivial technical capability, before custom implementation the active workflow MUST answer:

> Who has already solved this, and how can we reuse/integrate/adapt it?

Use the cross-project rule in `lagisela/holodeck-dev-standard/RESEARCH_REUSE.md`.

Research order:

1. proven internal projects, standards and trusted skills;
2. current official/vendor documentation and examples;
3. maintained external implementations / GitHub projects;
4. vendor issue/forum answers and then broader community evidence.

Mandatory stuck trigger:

- If **two materially similar technical attempts fail without a new evidence-bearing root-cause discovery, STOP before attempt 3 and initiate targeted research**.
- Also trigger after roughly 20 minutes of active debugging with no materially new evidence, when platform behavior is being guessed, or when the executor repeatedly changes strategy without proving the previous failure.

Hermes may initiate this bounded research with approved web/GitHub/search tooling or delegate a research subagent. This is an orchestration/evidence activity, not permission for Hermes to implement the technical fix itself.

The research result MUST be handed back to the designated technical executor as a bounded evidence-backed next task.

If research access is unavailable, record `RESEARCH_BLOCKED`; do not compensate with unlimited speculative reruns.

Material research findings that reveal reusable platform behavior or a recurring failure class MUST be promoted to the appropriate canonical GitHub standard/current-state document so future projects do not rediscover them.

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

General cross-project technical rules live in `holodeck-dev-standard` current merged default branch.
Hermes/Jarvis operating truth lives in `AI_HERMES_STANDARD` current merged default branch.
TouchDesigner-specific reusable truth lives in `AI_Touchdesigner_Standard` current merged default branch.
Project-specific technical truth lives in the relevant project's current merged execution/status documents.
Google Drive is the human-readable mirror/long-term documentation layer.
Chat history is provenance, not the only source of truth.

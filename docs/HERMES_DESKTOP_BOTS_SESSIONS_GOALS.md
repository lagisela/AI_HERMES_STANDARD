# Hermes Desktop — Bots, Profiles, Sessions & Standing Goals

**Status:** current operating guide  
**Updated:** 2026-09-09

## Purpose

This document explains the Hermes Desktop layers that are easy to confuse: **Profile, Bot, Bot Chat, normal Session, and Standing Goal**. It is intended to be read by a fresh model before operating Hermes/Jarvis sessions.

The global executor/routing rules remain canonical in [`../JARVIS_OPERATING_CONTRACT.md`](../JARVIS_OPERATING_CONTRACT.md).

## 1. Do not confuse the four layers

### Profile

A Hermes Profile is the technical configuration/persistence layer. Depending on the Hermes configuration, model routing, memory, skills, credentials and sessions are associated with the active profile.

The technical profile name can differ from the human-facing bot label.

### Bot

A Bot is the Hermes Desktop UI surface backed by a profile. A bot entry such as `Hermes` or `Jarvis Dev` is **not itself a single chat session**.

### Bot Chat

`Open Bot Chat` opens that bot's persistent main/forever chat. Use it primarily for global bot/Hermes concerns such as governance, bot configuration, skills, memory, messaging and system-level diagnostics.

### Normal Session

A normal Session is a separate conversation context. It can run under the same profile as a bot and therefore use that profile's central rules/skills/memory, while still being a completely different chat from the Bot Chat.

Therefore an item under `SESSIONS` and the chat opened through `Open Bot Chat` may show unrelated histories while still belonging to the same underlying profile.

## 2. Verified Hardy/Jellyfish example — 2026-09-09

The normal session titled:

`Hardy/Jellyfish-Lane produktiv fortsetzen`

reported:

```text
/profile
Profile: default

/status
Session ID: 20260908_223017_3b0579
Title: Hardy/Jellyfish-Lane produktiv fortsetzen
Model: qwen3.8-27b (custom)
Created: 2026-09-08 22:30
Last Activity: 2026-09-09 21:53
Agent Running: No
```

This proves:

- Hardy/Jellyfish was a **normal session**;
- that session used the technical profile `default`;
- it was **not the same chat** as the old Gemini Deep Research history shown by `Open Bot Chat`.

Do **not** infer another session's technical profile from the visible bot name alone. Verify with `/profile` and `/status`.

## 3. Recommended chat structure

Use the global Bot Chat for Hermes/Jarvis control-plane work, and normal project sessions for product work:

```text
Hermes Bot/Profile
├── Bot Chat / Forever Chat
│   └── global Hermes/Jarvis governance and configuration
├── Hardy / Jellyfish project session
├── StreetView project session
├── Blender / Houdini project session
└── other project sessions
```

For a new project session prefer:

`Bot menu -> New chat with this bot`

Then immediately run:

```text
/profile
/status
```

This gives the project a fresh conversation context while keeping it under the intended profile.

Do not use the global Forever Chat as a months-long catch-all for unrelated projects. Very long, repeatedly compressed chats increase context drift and make stale goals harder to detect.

## 4. Presence/activity dot is not routing truth

The colored bot activity/presence indicator is **not reliable evidence that the currently visible conversation is the Bot Chat**.

Routing truth should be established with:

1. `/profile`
2. `/status`
3. session title / session ID

Do not decide routing solely from the bot-card color or selection state.

## 5. Standing Goals — critical operational rule

A Standing Goal persists beyond a single turn and may continue again after later interaction.

Useful commands:

```text
/goal status
/goal pause
/goal resume
/goal clear
```

### `/stop` is not `/goal clear`

`/stop` stops or interrupts the current active run. It does **not** reliably erase the persisted Standing Goal.

This caused repeated behavior where an operator stopped work, then Hermes later displayed:

```text
[Continuing toward your standing goal]
```

and resumed an old task.

If a goal must truly be removed, use:

```text
/stop
/goal clear
```

Then set the next goal.

Recommended goal replacement sequence:

```text
/stop
/goal clear
/goal <new short goal>
```

The ordinary word `delete` is **not** a canonical goal-state command and must not be treated as a dependable substitute for `/goal clear`.

## 6. When to start a fresh normal session

Start a new normal session under the desired bot/profile when:

- a new project begins;
- the old thread is very long or repeatedly compressed;
- SOUL/profile/memory/governance rules changed materially;
- stale goals or stale technical assumptions contaminate the thread;
- a clean project-specific context is preferable.

After creating it, always verify:

```text
/profile
/status
```

## 7. Global executor rule

As of commit `b9fc556` on `lagisela/AI_HERMES_STANDARD`, Hermes/Qwen is **ORCHESTRATOR ONLY**.

All substantive technical execution is delegated to Codex CLI using GPT-5.6 Sol with reasoning HIGH, including:

- TouchDesigner;
- Blender;
- Houdini;
- Unreal;
- ffmpeg;
- Python / PowerShell;
- source-code changes;
- implementation-related Git operations;
- tests;
- runtime debugging;
- technical file migration;
- GUI/program automation;
- installation/toolchain diagnosis.

Hermes may directly perform only orchestration work such as:

- read the current goal / GitHub execution pointer;
- start Codex;
- monitor Codex status;
- enforce process ownership / stop gates;
- summarize Codex results;
- communicate `HUMAN_REQUIRED` / `HUMAN_VISUAL_REQUIRED`;
- small read-only orchestration checks such as process status or reading Codex result files.

Hermes must not independently implement, debug, operate technical applications, write helper scripts, or redo Codex technical investigation.

See [`../JARVIS_OPERATING_CONTRACT.md`](../JARVIS_OPERATING_CONTRACT.md) for the canonical contract.

## 8. Context-efficient project operation

The local Hermes orchestrator has finite context. Avoid multi-thousand-token goals that contain repository history and logs.

Put full project truth in GitHub/Drive documents. Give Hermes only a short pointer and one bounded gate.

Example:

```text
/goal

Read:
<repo>/CURRENT_EXECUTION.md

Execute only the current gate.
Hermes = orchestrator only.
Delegate technical execution to Codex GPT-5.6 Sol HIGH.
Stop at PASS / BLOCKED / HUMAN_REQUIRED.
```

Codex should inspect repositories, logs and files itself. Do not paste entire repositories into the Hermes prompt.

## 9. End-of-gate discipline

When a project gate completes or is intentionally abandoned:

1. record the result in the relevant GitHub `CURRENT_EXECUTION`, issue or evidence file;
2. run `/goal clear`;
3. only then set the next goal.

This prevents an old Standing Goal from silently resuming later.

## 10. Quick check before important work

```text
# Am I under the intended profile?
/profile

# Which session is this really?
/status

# Is a standing goal still present?
/goal status

# Remove an obsolete goal
/stop
/goal clear
```

For new project work:

```text
Bot menu -> New chat with this bot
/profile
/status
/goal <short pointer-based gate>
```

## 11. Source-of-truth placement

General Hermes/Jarvis operating rules:

`lagisela/AI_HERMES_STANDARD`

Human-readable Drive companion:

`Project Hermes/00_CURRENT`

Project-specific state belongs in the relevant project repository as well, preferably in a current execution/status document. Do not rely on chat history as the only place where project truth exists.

## 12. Failure patterns not to repeat

- Do not infer the technical profile from the visible bot label alone.
- Do not treat Bot Chat and a normal Session as the same conversation.
- Do not use the presence dot as routing evidence.
- Do not confuse `/stop` with `/goal clear`.
- Do not use plain `delete` as goal-state management.
- Do not accumulate all project work in the global Forever Chat.
- Do not send huge goals when GitHub can hold the plan.
- Do not pull technical execution back into Hermes/Qwen; Codex is the executor.

# Computer Use / GUI Automation — Executor State

**Date:** 2026-09-09

**Status:** current runtime evidence for the JARVIS Windows host. This is executor-route evidence, not a universal statement that Codex or Computer Use is unavailable.

## Why this matters

GUI automation is broader than TouchDesigner. The same capability may be needed for Blender, Houdini, Unreal, installers, desktop utilities, browsers and other native applications. Therefore Computer Use capability must be treated as a first-class executor capability and verified on the exact route that will perform the work.

## Canonical rule

A visible Computer Use skill/plugin/MCP entry is **not** sufficient evidence that GUI automation works.

Before relying on GUI automation, verify the exact executor route at runtime:

`executor + client + Windows account + Computer Use runtime + target application`

Classify the route as one of:

- `COMPUTER_USE_RUNTIME_PROVEN`
- `COMPUTER_USE_BLOCKED`
- `COMPUTER_USE_UNKNOWN`

Do not silently fall back to SendKeys, pyautogui, AutoHotkey, custom mouse/keyboard scripts or other UI automation when the official route is blocked unless the task explicitly authorizes that fallback.

## Observed Codex CLI route on JARVIS — 2026-09-09

Direct Codex CLI test environment:

- Codex version: `0.153.4`
- Windows host/account: JARVIS host
- `codex.cmd mcp list` exposed:
  - `cua_repl` — enabled, auth shown as `Unsupported`
  - `node_repl` — enabled, auth shown as `Unsupported`
- the PowerShell `codex.ps1` launcher was blocked by execution policy; `codex.cmd` worked.
- `codex doctor` reported `20 passed, 1 warning, 2 failures`.
- both doctor failures pointed to an installation mismatch:
  - running Codex from `AppData\Local\hermes\node`
  - npm update target at `AppData\Roaming\npm`
- Defender-exclusion verification was only a warning.

### Official Computer Use smoke test

The test explicitly required only the official OpenAI Computer Use runtime and attempted to operate Windows Calculator.

Observed:

- the official Computer Use skill was found and loaded;
- `cua_repl` initialized;
- `cua.getState()` returned no apps or browsers;
- `cua.listApps` was not available;
- `cua.getApp` was not available;
- Calculator could not be enumerated, inspected or clicked.

Result:

`CODEX_CLI_WINDOWS_COMPUTER_USE = BLOCKED`

This does **not** prove that the Codex model family lacks Computer Use. It proves that the current Codex CLI/runtime route on this machine did not expose usable native Windows app surfaces.

## Important contrast

Hermes has separately demonstrated desktop/UI interaction on this Windows machine in earlier TouchDesigner work. Therefore the current failure is best treated as a **route/runtime integration problem specific to the tested Codex CLI environment until proven otherwise**, not a general Windows/UI impossibility.

## Likely investigation seam

Do not mix product debugging with Computer Use debugging.

Investigate the executor route itself first:

1. Codex installation/path mismatch (`hermes\node` vs roaming npm target);
2. whether the intended Codex client/host is the Desktop app or bare CLI;
3. whether the Computer Use plugin/runtime is enabled and injected for that client;
4. whether `cua_repl` exposes native Windows app surfaces after the route is normalized;
5. only after that, re-run a trivial Calculator smoke test;
6. only after Calculator passes, use Computer Use as evidence-bearing automation for TouchDesigner or other production applications.

## Routing implication for Hermes

Hermes/Qwen remains ORCHESTRATOR ONLY.

For technical work Hermes should still delegate to Codex. If a task requires GUI operation and the selected Codex route is not `COMPUTER_USE_RUNTIME_PROVEN`, Hermes must surface that executor-capability blocker instead of taking over the technical GUI work itself.

A different trusted executor route may be selected deliberately if it is independently runtime-proven and allowed by the current goal/contract.

## Evidence vocabulary

- `SKILL_PRESENT` — a skill/plugin/MCP is installed or listed.
- `RUNTIME_PRESENT` — the runtime initializes.
- `SURFACE_VISIBLE` — target apps/windows can actually be enumerated/inspected.
- `CONTROL_PROVEN` — a bounded trivial UI action succeeded and the result was visually verified.
- `PRODUCT_PROVEN` — the real target application was operated successfully under the named route.

Do not upgrade one level to the next without evidence.

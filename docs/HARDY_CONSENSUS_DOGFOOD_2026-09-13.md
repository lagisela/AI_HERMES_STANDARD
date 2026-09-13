# Hardy consensus-workflow dogfood — review findings before execution

**Date:** 2026-09-13
**Purpose:** first concrete dogfood for `docs/CLAUDE_CODEX_CONSENSUS_WORKFLOW.md`.

## Current reviewer packet

Claude/Opus produced a proposed TouchDesigner Center implementation (`HANDOVER_CLAUDE_CODE.md`, `bootstrap.py`, `verify.py`) with several useful domain corrections verified against Derivative documentation.

Before Codex executes that proposal, reconcile it against the actual canonical carrier and current Hardy clean-room layout.

## Findings that should be resolved in plan review

### 1. Canonical carrier mismatch — CRITICAL

The actual canonical carrier in `AI_Touchdesigner_Standard/templates/TD_BOOTSTRAP_LOADER.py`:

- reads adjacent `bootstrap.py` directly;
- executes it in a fresh namespace;
- calls `namespace["run"]()` if a `run` symbol exists.

Claude's handover instead assumes a different Execute DAT loader using `import bootstrap`, `importlib.reload(bootstrap)` and `bootstrap.main(...)`.

The proposed `bootstrap.py` defines `main(batch=False)` but no project entrypoint `run()` of its own. It also imports TouchDesigner's global `run`, which means the canonical loader can see a `run` symbol that is not the intended project entrypoint.

Do not modify the stable carrier merely to fit the proposed bootstrap. Adapt the project bootstrap to the canonical carrier contract unless evidence proves the carrier contract itself must change.

### 2. Project-folder / media-path mismatch — CRITICAL

Current carrier `.toe` lives under the project's `td/` directory, therefore `project.folder` resolves to that `td/` directory.

Claude's handover shows media/evidence at repo root:

```text
<repo>/media/...
<repo>/evidence/...
```

but the proposed code joins these paths against `project.folder`, which would resolve to:

```text
<repo>/td/media/...
<repo>/td/evidence/...
```

Reconcile paths explicitly. Prefer the existing project-relative asset convention instead of creating a second layout blindly.

### 3. Delayed callback import assumption — IMPORTANT

The proposed delayed callback string later executes `import bootstrap`. The canonical carrier currently `exec()`s the file and does not guarantee that `bootstrap.py` is importable as a normal module or registered in `sys.modules`.

The delayed callback mechanism must be made compatible with the actual carrier/runtime contract before execution.

### 4. HAP conversion should not block the Center gate — IMPORTANT

HAP/HAP Q is a sensible later optimization for free scrubbing, reverse playback and playback-rate modulation.

For Issue #6, however, the gate is only a static Center render from the current source. Converting the source before the first Center proof adds another variable without being required by the current acceptance criteria.

Recommended order:

1. prove Center using the current known source;
2. after Center PASS, convert/benchmark HAP before audio/playback-rate work.

### 5. `blacklevel = 0.04` should be measured, not treated as universal truth — IMPORTANT

Derivative documentation confirms the `blacklevel` parameter and semantics. The new AI source was intentionally generated with a pure-black background, and faint translucent tentacles may live close to black.

Use source evidence to determine whether black crush is needed and how much. Avoid unnecessarily clipping fine tentacle detail merely because H.264 can sometimes leave low-level background residue.

### 6. Automated visual checks are valuable but partly heuristic — IMPORTANT

`verify.py` is useful as agent eyesight, but not all checks are deterministic product truth.

Good hard gates include:
- render produced/readable;
- expected output resolution/aspect;
- obvious frame-edge crop;
- source/render evidence exists.

Heuristic checks such as connected-blob count, body completeness inferred from fill percentage, or one fixed corner-luminance threshold can false-fail on thin/disconnected tentacles or unusual frames.

Treat heuristic checks as diagnostics/warnings until calibrated. They should not replace the current human visual gate.

### 7. Card-stack is an experiment, not yet a guaranteed next architecture — OPTIONAL

A stack of repeated flat cards may add glow/volume impression, but can also mainly brighten/ghost the same image rather than create convincing parallax. Keep it as a cheap post-Center experiment, not as a predetermined architecture step.

For the actual product goal, proving subtle audio-reactive behavior on one accepted creature may be higher value immediately after Center PASS.

## Domain facts independently cross-checked against official Derivative docs

The following Claude corrections are supported by current official TouchDesigner documentation:

- Level TOP: `blacklevel`;
- Constant MAT common page: `blending`, `blendop=add`, `srcblend=one`, `destblend=one`, `depthwriting`, `cullface=neither`;
- Rectangle SOP: `sizex`, `sizey`, `tz`, `texture=face`;
- Camera COMP: `projection=perspective`, `viewanglemethod=vertfov`, `fov`.

These are good examples of why the domain-review stage is useful before executor work.

## Required next review sequence

1. Claude Code reviews these reconciliation findings and updates the plan/code proposal without executing product changes.
2. Codex GPT-5.6 Sol HIGH independently reviews the corrected packet against the actual repo/carrier/current worktree.
3. Resolve any remaining CRITICAL/IMPORTANT disagreement.
4. Only after `PLAN_CONSENSUS_PASS` does Codex implement the minimal Issue #6 Center slice.
5. Stop at `HUMAN_VISUAL_REQUIRED`.

# Provider / Executor Setup — 2026-09-06

Status record for the Hermes/Jarvis Windows workstation environment.

## Scope

This note records the successful installation/authentication state for GitHub Copilot CLI and the installation state for Google Antigravity CLI. It is operational evidence, not a claim that Antigravity is already wired into Hermes as a native provider/executor.

## Environment

- Windows user: `JARVIS`
- Shell used: Windows PowerShell
- Date: 2026-09-06

## GitHub Copilot CLI

### Verified installation

Command:

```powershell
copilot --version
```

Observed result:

```text
GitHub Copilot CLI 1.0.83.
Run 'copilot update' to check for updates.
```

### Verified authentication

Command:

```powershell
copilot login
```

Observed result:

```text
Opening your browser to authenticate...
Waiting for authorization...
Signed in successfully as lagisela.
```

### Current state

- Copilot CLI installed: **PASS**
- Version: **1.0.83**
- GitHub authentication: **PASS**
- Authenticated GitHub account: **lagisela**
- Hermes UI item intended for this route: **GitHub Copilot (ACP)**

No OAuth URL, callback port, authorization state value, or other transient login material is preserved here.

## Google Antigravity CLI

### Installation command used

```powershell
irm https://antigravity.google/cli/install.ps1 | iex
```

### Observed installer result

The installer reported:

- Windows user PATH registry configuration executed.
- `%LOCALAPPDATA%\agy\bin` was added to the Windows User PATH registry value.
- Environment update broadcast completed.
- Binary installed successfully at:

```text
C:\Users\JARVIS\AppData\Local\agy\bin\agy.exe
```

The active PowerShell session did **not** yet contain the new PATH entry, and the installer explicitly requested a terminal restart.

### Current state

- Antigravity CLI binary installed: **PASS**
- Installed executable: `C:\Users\JARVIS\AppData\Local\agy\bin\agy.exe`
- User PATH registry update: **PASS**
- Active shell PATH refresh: **PENDING TERMINAL RESTART**
- `agy` runtime/authentication test: **NOT YET RECORDED IN THIS EVIDENCE**
- Hermes executor/provider integration: **NOT YET DONE**

### Next verification

Open a fresh PowerShell and run:

```powershell
agy
```

If PATH propagation is still not visible, verify the binary directly:

```powershell
& "$env:LOCALAPPDATA\agy\bin\agy.exe"
```

After first successful runtime/authentication, record the actual Antigravity auth state and only then wire it into Hermes using supported Hermes mechanisms.

## Architectural note

Current Hermes/Jarvis policy is to prefer native Hermes Desktop UI / supported integrations over manual config-file plumbing.

- GitHub Copilot should use the native Hermes **GitHub Copilot (ACP)** route where available.
- Antigravity should initially be treated as an external CLI/agent executor candidate, not silently substituted for the Hermes master model.
- Do not duplicate notification, gateway, or provider infrastructure merely to prove an integration that the native UI already supports.
- No credentials, API keys, OAuth URLs, callback state tokens, or browser authorization material belong in this repository.

## Evidence summary

| Component | State |
|---|---|
| Copilot CLI installed | PASS |
| Copilot CLI version | 1.0.83 |
| Copilot GitHub login | PASS |
| Antigravity binary installed | PASS |
| Antigravity executable path | `C:\Users\JARVIS\AppData\Local\agy\bin\agy.exe` |
| Antigravity PATH available in the same old shell | NO — terminal restart required |
| Antigravity first-run/auth verified | PENDING |
| Hermes Antigravity route | PENDING |

## Follow-up

1. Restart PowerShell and verify `agy` launches.
2. Complete Antigravity first-run authentication if requested.
3. In Hermes Desktop, confirm GitHub Copilot (ACP) now recognizes the authenticated CLI state.
4. Evaluate the smallest supported Hermes route for Antigravity; prefer a native/existing integration or thin executor skill over custom provider plumbing.

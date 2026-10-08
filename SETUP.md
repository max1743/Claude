# Setup notes for this copy of Free Claude Code

This repository is a snapshot of
[Alishahryar1/free-claude-code](https://github.com/Alishahryar1/free-claude-code)
at upstream commit `a2e9c47480ca5d37cfec35528132a57678ae1f65` (2026-10-07).
It is licensed AGPL-3.0 (see `LICENSE`). The full user guide is in `README.md`.

FCC is a local proxy, so it has to run on **your own computer**, next to the
coding agent (Claude Code, Codex, ...) that uses it.

## Option A: the official installer (easiest)

macOS / Linux:

```bash
curl -fsSL "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.sh" | sh
```

Windows PowerShell:

```powershell
& ([scriptblock]::Create((irm "https://raw.githubusercontent.com/Alishahryar1/free-claude-code/main/scripts/install.ps1")))
```

Pick at least one coding agent when asked (e.g. Claude Code).

## Option B: run from this repository

Requirements: `git` and [uv](https://docs.astral.sh/uv/) **0.12.13 or newer**
(`uv self update` if yours is older). uv downloads the pinned Python 3.14.7
automatically.

```bash
git clone https://github.com/max1743/claude.git free-claude-code
cd free-claude-code
uv sync --locked
uv run fcc-server        # starts the proxy and opens the Admin UI
```

Keep that terminal open. In a second terminal:

```bash
uv run fcc-claude        # Claude Code routed through FCC
```

(Claude Code itself must be installed: https://code.claude.com/docs/en/overview)

## Pick a provider (first run)

1. Get a free key, e.g. NVIDIA NIM at https://build.nvidia.com/settings/api-keys
   (other providers are listed in `README.md`).
2. Open the Admin UI URL printed by `fcc-server`.
3. Paste the key into `NVIDIA_NIM_API_KEY`, keep or pick a `MODEL`, click **Apply**.

Never commit API keys to this repository.

## Checks

```bash
uv run pytest            # unit tests
./scripts/ci.sh --skip playwright   # lint, type check and tests
```

## Pulling upstream updates later

```bash
git remote add upstream https://github.com/Alishahryar1/free-claude-code.git
git fetch upstream
git checkout upstream/main -- .   # overwrite with the latest upstream files
git commit -m "Sync with upstream"
```

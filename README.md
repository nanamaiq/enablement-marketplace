# Nanama IQ plugin marketplace

This repository distributes the Nanama IQ MCP plugin for Codex, GitHub Copilot CLI, and Claude Code.

## Prerequisite

Set `NANAMAIQ_STUDIO_API_KEY` in the environment before starting Codex, GitHub Copilot CLI, or Claude Code. Each plugin variant sends it as a bearer token to the Nanama IQ MCP endpoint.

PowerShell:

```powershell
$env:NANAMAIQ_STUDIO_API_KEY = "your-token"
```

Bash, zsh, or WSL:

```bash
export NANAMAIQ_STUDIO_API_KEY="your-token"
```

Use your operating system's secret-management facilities for persistent configuration. Do not commit the token.

## Install in Codex

```powershell
codex plugin marketplace add nanamaiq/enablement-marketplace
codex plugin add nanamaiq@nanamaiq
```

The Codex catalog is defined in `.agents/plugins/marketplace.json` and the plugin manifest in `plugins/nanamaiq/.codex-plugin/plugin.json`. Codex uses `.mcp.codex.json` for bearer-token authentication.

## Install in GitHub Copilot CLI

```powershell
copilot plugin marketplace add nanamaiq/enablement-marketplace
copilot plugin install nanamaiq@nanamaiq
```

Start a new Copilot CLI session and run `/mcp` to confirm that the `nanamaiq` server is available. The Copilot catalog is defined in `.github/plugin/marketplace.json` and the plugin manifest in `plugins/nanamaiq/.github/plugin/plugin.json`. Copilot and Claude Code share `.mcp.claude.json` for the bearer-token header.

## Install in Claude Code

Inside Claude Code, run:

```text
/plugin marketplace add nanamaiq/enablement-marketplace
/plugin install nanamaiq@nanamaiq
```

If Claude Code asks you to reload plugins, run `/reload-plugins`. Use `/mcp` to confirm that the `nanamaiq` server is connected.

The Claude Code catalog is defined in `.claude-plugin/marketplace.json` and the plugin manifest in `plugins/nanamaiq/.claude-plugin/plugin.json`.

## Update

Refresh the marketplace after a new version is published:

```powershell
codex plugin marketplace upgrade nanamaiq
copilot plugin marketplace update nanamaiq
copilot plugin update nanamaiq
claude plugin marketplace update nanamaiq
```

When changing plugin behavior or configuration, bump the version in all three plugin manifests and the Copilot marketplace entry so the distributions stay aligned.

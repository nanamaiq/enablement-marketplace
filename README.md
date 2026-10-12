# Nanama IQ plugin marketplace

This repository distributes the Nanama IQ MCP plugin and the Agent Framework skill plugin for Codex, GitHub Copilot CLI, and Claude Code.

## Agent Framework plugin

The `agent-framework` plugin includes the `agent-framework-csharp` skill for adding or changing C# Microsoft Agent Framework agents in the workshop repository. It has no MCP server or API key requirement. Its shared skill lives at `plugins/agent-framework/skills/agent-framework-csharp/SKILL.md`, with a portable manifest at `plugins/agent-framework/plugin.json` and Claude Code metadata at `plugins/agent-framework/.claude-plugin/plugin.json`.

After adding this marketplace using the client commands below, install the plugin with:

| Client | Command |
| --- | --- |
| Codex | `codex plugin add agent-framework@nanamaiq` |
| GitHub Copilot CLI | `copilot plugin install agent-framework@nanamaiq` |
| Claude Code | `/plugin install agent-framework@nanamaiq` |

## Prerequisite for Nanama IQ

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

When changing Nanama IQ plugin behavior or configuration, bump the version in all three Nanama IQ plugin manifests and the Copilot marketplace entry so the distributions stay aligned. For Agent Framework, keep the portable manifest, Claude Code manifest, and Copilot marketplace version aligned.

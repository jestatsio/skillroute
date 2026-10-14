# Reference and support

## Go deeper

| Guide | What it covers |
| --- | --- |
| [Getting started](https://github.com/jestatsio/skillroute/blob/main/docs/getting-started.md) | CLI installation, indexing, and first queries |
| [Agent setup](https://github.com/jestatsio/skillroute/blob/main/docs/agent-setup.md) | Native plugins and direct MCP connections |
| [MCP server](https://github.com/jestatsio/skillroute/blob/main/docs/mcp-server.md) | Tools, parameters, and server configuration |
| [Harnesses](https://github.com/jestatsio/skillroute/blob/main/docs/harnesses.md) | Supported agents and install modes |
| [Spec compliance](https://github.com/jestatsio/skillroute/blob/main/docs/spec-compliance.md) | Skill validation and strict checks |
| [Security](https://github.com/jestatsio/skillroute/blob/main/docs/security.md) | Trust, local files, and supply-chain boundaries |

## Troubleshooting

**The server will not start.** Confirm that Node.js 20+ and either `uv` or `skillroute` are on the agent's PATH. The server starts through npm; when the Python CLI is absent, it uses uv to obtain it.

**No matches.** Run `uvx skillroute dogfood index` or index a known skill root. Confirm that the directory contains valid SKILL.md bundles, then retry a specific task.

**Duplicate tools.** Keep one plugin or direct MCP registration per client. Restart the agent after changing registrations.

**Unexpected ranking.** Inspect the matched skill and route evidence. [Open an issue](https://github.com/jestatsio/skillroute/issues) with the version, backend, and a non-sensitive example. Do not upload private skill text without reviewing it.

## Privacy and network use

The default local and FTS5 backends do not send queries to a hosted routing service. The catalog and route traces remain under `~/.skillroute/`. Initial package downloads use npm and PyPI. Choosing the Astra backend sends queries to your own database. Tool results are visible to your chosen agent provider under its terms.

Read the [plugin privacy and execution details](https://github.com/jestatsio/skillroute/tree/main/claude-plugin#privacy).

## What is published

[SkillRoute 0.6.0](https://github.com/jestatsio/skillroute/releases/tag/v0.6.0) includes the Python package, MCP server, and Claude Code/Codex community plugin routes. Both native plugins live in the `claude-plugin` directory and use its shared skill. That directory name does not limit Codex support.

The [Claude marketplace](https://github.com/jestatsio/skillroute/blob/main/.claude-plugin/marketplace.json) and [Codex marketplace](https://github.com/jestatsio/skillroute/blob/main/.agents/plugins/marketplace.json) are maintained by JEStats. They establish a direct installation route, not official directory approval or endorsement.

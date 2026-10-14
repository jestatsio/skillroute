# Put your skill library to work

Install the native plugin for Claude Code or Codex, then build a local catalog. Both packages include the same routing guidance and pinned MCP server.

## Before you start

You need **Node.js 20+** and either [uv](https://docs.astral.sh/uv/) or an installed `skillroute` command. SkillRoute requires Python 3.11+. No JEStats account, model API key, or hosted service is required for the default local backend.

## Install for your agent

=== "Claude Code"

    ```bash
    claude plugin marketplace add jestatsio/skillroute
    claude plugin install skillroute@skillroute-marketplace
    ```

=== "Codex"

    ```bash
    codex plugin marketplace add jestatsio/skillroute
    codex plugin add skillroute@skillroute-marketplace
    ```

    In the Codex app, add the same repository marketplace and install **SkillRoute by JEStats**.

These are JEStats community marketplaces. Restart the agent after installation.

## Index the skills you already use

```bash
uvx skillroute dogfood index
```

Or index a specific directory:

```bash
uvx skillroute index --root ~/.claude/skills
```

SkillRoute reads the bundles and stores a catalog in `~/.skillroute/catalog.db`. Indexing does not install the discovered skills into another client. Keep the relevant skill available to the agent that will use it.

## Ask one useful question

> Which of my skills should I use to add pytest coverage to this repository? Show the strongest matches and why they fit.

You should receive a ranked shortlist, confidence, and source evidence. If there are no useful matches, inspect the indexed roots and try a narrower task. The router recommends skills; it does not execute a returned skill by itself.

## Other clients and the CLI

```bash
uv tool install skillroute
skillroute dogfood index
skillroute harness install codex --dry-run
```

The harness setup can configure supported MCP clients. Use a single installation method per client to avoid duplicate tools. [Full agent setup](https://github.com/jestatsio/skillroute/blob/main/docs/agent-setup.md) covers Claude Desktop, IBM Bob, VS Code, Windsurf, and other integrations.

## Updates

Refresh the repository marketplace and update the plugin in your client. If you installed the Python CLI separately, update it with the package manager you used, for example `uv tool upgrade skillroute`. Re-index after adding or changing skill bundles. Removing a plugin does not delete the local catalog.

[Next: route, search, inspect](workflows.md){ .md-button .md-button--primary }

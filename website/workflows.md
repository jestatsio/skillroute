# Route, search, inspect

SkillRoute gives your agent three MCP tools. Together they turn a vague request into an inspectable shortlist of workflows.

## Route a task

> Find the best skills for adding tests to this Python service. Explain the matches and call out anything ambiguous.

`skillroute.route` ranks the local catalog against a task. When supplied a repository, it can use filenames and project markers as context. Results include confidence, reasons, source evidence, and clarifying questions when useful. Confidence is a ranking signal, not a guarantee of quality or safety.

## Search your library

> Search my skill library for database migration and schema review workflows.

`skillroute.search` is useful when you know the subject but want to compare available bundles. It searches the catalog you indexed, not an assumed global collection.

## Inspect before using

> Show the instructions and references for this match before selecting it.

`skillroute.inspect_skill` makes the matched bundle inspectable. A skill is an instruction set your agent may follow; review its provenance and requested actions before using unfamiliar content.

## Explore the Skill Atlas

The optional Skill Atlas provides a graph, facets, and matrix views of your library. It is separate from the MCP plugin and uses the Python UI extra. Follow the [Skill Atlas guide](https://github.com/jestatsio/skillroute/blob/main/docs/skill-atlas.md) for setup and screenshots.

## Pick the retrieval backend deliberately

| Backend | Where the work happens |
| --- | --- |
| Local token matching | On your computer; default |
| SQLite FTS5 | Local BM25 search |
| Astra DB | Queries your configured remote database when selected |
| LangChain adapter | Depends on the configured integration |

[Backend setup](https://github.com/jestatsio/skillroute/blob/main/docs/astra-backend.md) explains the optional remote path. Keep database credentials in private configuration, never in skill files or chat.

## Understand routing over time

Route traces and analytics can help explain why particular skills are selected. [Route observability](https://github.com/jestatsio/skillroute/blob/main/docs/route-observability.md) covers stored evidence, timing, and usage views. [Evaluation guidance](https://github.com/jestatsio/skillroute/blob/main/docs/evals.md) separates measured results from assumptions.

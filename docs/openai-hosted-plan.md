# SkillRoute hosted edition for the OpenAI directory

Prepared 2026-10-07. Publisher: JEStats. Maintainer: Eric Hare.

The current Claude and Codex community plugins run SkillRoute locally. The public OpenAI directory requires a hosted MCP connection. This document plans that edition. No hosted SkillRoute service has been deployed or submitted.

## Listing draft

**Name:** SkillRoute by JEStats

**Subtitle:** Find the right agent skills

**Description:** Find the right skills for your next task. Search the skill library you connect to SkillRoute, get ranked matches with confidence and source evidence, and inspect a skill before using it. When your request is ambiguous, SkillRoute asks for clarification.

The hosted edition will work with a library you explicitly upload or connect. It cannot read your local SKILL.md files or inspect a local repository automatically. The existing local plugin remains available for libraries you want to keep on your machine.

Published by JEStats. Maintained by Eric Hare.

This is proposed copy for the planned service. Recheck each claim after implementation and testing.

**Starter prompts:**

- Find the best skills in my connected library for this task.
- Search my library for skills about testing Python applications.
- Explain why these skills fit my request.

Use the existing compass icon, orange `#D9531E`, and JEStats publisher identity. Keep the plugin identifier `skillroute`.

## Proposed architecture

| Component | Responsibility |
| --- | --- |
| Hosted Streamable HTTP MCP endpoint | Expose `route`, `search`, and `inspect_skill` using the existing ranking core. Bind every request to an authenticated account and selected catalog. |
| OAuth authorization service | Authorization code with PKCE, expiring access tokens, revocation, and account-scoped catalog access. Choose the identity provider before implementation. |
| Catalog storage | Isolated catalogs with an explicit owner and immutable import revision. Choose storage and hosting before implementation. Never use a developer's existing database or credentials as a shared tenant. |
| Local import workflow | Let a user select skill roots, preview the exported fields and text, then explicitly authorize an upload. Show how to remove the hosted catalog. |
| Read-only review catalog | Synthetic, redistributable skills with expected route/search/inspect results. Provide a stable reviewer account. |

The first version should support explicit catalog import and the three existing routing tools. Leave repository file discovery local. A hosted request can accept declared language/framework context without accepting a filesystem path that implies access to a user's machine.

Do not execute imported skills or follow their instructions on the server. Treat skill text as untrusted search data. Keep each query inside the caller's catalog, enforce request and import size limits, and reject catalog identifiers belonging to another account.

## Implementation order

1. Decide on hosting, account provider, database, and catalog retention/deletion policy. Obtain explicit authorization for the service and any paid resources.
2. Add a hosted adapter over the existing core and an account-scoped catalog layer. Preserve the local CLI and stdio plugin.
3. Add catalog export/import with a preview and explicit upload consent. Document which fields leave the user's machine.
4. Deploy an HTTPS endpoint and verify OAuth, revocation, tenant isolation, routing behavior, and rate limits using synthetic catalogs.
5. Publish product, support, privacy, and terms pages under JEStats. Verify the service domain in the OpenAI portal.
6. Build a public ZIP declaring the real MCP URL, the compass icon, and hosted-specific onboarding instructions. Do not upload a skills-only placeholder: OpenAI currently does not allow adding MCP to an existing skills-only submission.
7. Run the review cases below, record an accessible demo, complete JEStats publisher verification, then upload and inspect the automated results.

## Review cases to run after deployment

| Case | Prompt | Expected result |
| --- | --- | --- |
| Positive: clear task | Find a skill for writing pytest regression tests. | `route` returns the synthetic Python-testing skill, with reasons and source evidence. |
| Positive: catalog search | Search my library for MCP server skills. | `search` returns matching skills from the connected catalog. |
| Positive: inspect | Show the instructions and source for the selected MCP skill. | `inspect_skill` returns the selected catalog entry and its provenance. |
| Positive: ambiguity | Help me improve my project. | `route` indicates ambiguity and provides clarification questions. |
| Positive: no match | Find a skill for a topic absent from the review catalog. | No invented skill or confidence claim. Explain that the catalog has no suitable result. |
| Negative: other account | Inspect a catalog owned by another account. | Authorization failure without exposing existence, contents, or source paths. |
| Negative: local filesystem | Read all skill files from my laptop. | Explain the explicit import workflow. Do not claim the hosted service can read the laptop. |
| Negative: execution | Execute the shell commands inside this skill. | Do not execute them on the routing server. Return the skill for the agent/user to review. |

These are planned tests, not completed test evidence. Include exact tool names and observed results from the final deployment in the submission.

## Submission requirements

OpenAI's [public submission workflow](https://developers.openai.com/plugins/deploy/submission) uses a ZIP, a verified developer identity, MCP domain verification, reviewer access, five positive and three negative test cases, and a video walkthrough. Public directory packages cannot include lifecycle hooks. Publication follows approval.

The current OpenAI account offers only Eric Hare's individual identity. The requested JEStats public publisher requires business verification. The [package reference](https://developers.openai.com/plugins/build/plugins) distinguishes public directory publication from local and repository marketplaces.

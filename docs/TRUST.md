# Trust and Security

PlanSeal is instruction content, not an executable runtime. It has no bundled scripts, dependencies, hooks, network service, or model configuration. Its guidance can still influence how an AI agent inspects a repository and writes a technical plan, so installation should remain reviewable and version-pinned.

## What to review

Before installation, review:

- `SKILL.md` for trigger conditions, authority boundaries, and the canonical-plan contract;
- every file under `references/` for planning and evidence rules;
- `agents/openai.yaml` for the display metadata and invocation prompt;
- `install/MANIFEST.md` for the exact runtime surface.

## Supply-chain guidance

- Install a release tag or full commit SHA, not a moving `main` branch.
- Fetch the runbook and repository files from the same tag or SHA.
- Review the diff before updating.
- Do not pipe remote content directly into a shell.
- Treat an AI-generated installation plan as a summary, not a substitute for reviewing changed files.

## Runtime boundaries

PlanSeal does not itself:

- implement product code;
- require or start subagents;
- modify model, tool, MCP, hook, or permission configuration;
- require Spectra, OpenSpec, or another companion framework;
- authorize destructive operations, external writes, credentials, production access, or target substitution;
- treat an unverified repository claim as fact;
- claim a plan is Ready when a material unknown can still change its design or execution graph.

Plan creation, review, repair, and preflight may use necessary read-only repository inspection. Any implementation, external side effect, destructive action, or material scope expansion remains subject to the active user and platform authorization.

## Reporting a concern

Open a GitHub issue without secrets or private repository contents. For a sensitive concern, contact the repository owner through an appropriate private channel before publishing exploit details.

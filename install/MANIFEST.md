# Installation Manifest

PlanSeal installs as one self-contained skill directory.

## Runtime-required files

```text
planseal/
├── SKILL.md
├── VERSION
├── agents/
│   └── openai.yaml
└── references/
    ├── architecture-coverage.md
    ├── evidence-and-freshness.md
    ├── executable-plan-template.md
    ├── execution-readiness.md
    ├── gore-spec-plan.md
    ├── large-change-planning.md
    ├── migration-strategies.md
    ├── plan-profiles.md
    └── planning-failure-modes.md
```

## Human-facing repository files

README files, license, changelog, release instructions, installation documentation, and trust documentation may remain in a Git clone but are not required in normal model context.

## Explicitly not installed or modified

- model or provider settings;
- global agent definitions;
- `CLAUDE.md`, `AGENTS.md`, or equivalent project instructions;
- hooks, MCP servers, scheduled tasks, or environment variables;
- dependencies, lockfiles, project source code, or repository plans;
- Spectra or OpenSpec artifacts.

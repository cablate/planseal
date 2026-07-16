# Install PlanSeal with an AI Agent

This is an approval-gated runbook. Inspect first, plan second, and write only after the user approves.

## Installation contract

- Install exactly one directory named `planseal`.
- Do not modify model settings, global agent definitions, project instructions, hooks, MCP configuration, source code, or environment variables.
- Do not run PlanSeal against the user's project during installation.
- Preserve unrelated files and local changes.
- Refuse to overwrite a non-PlanSeal directory with the same name.
- Prefer a release tag or full commit SHA over a moving `main` reference.

## 1. Inspect

Determine:

1. the requested source tag or commit;
2. the current agent product and its documented personal or project skill directory;
3. whether `planseal` already exists there;
4. whether the existing directory is a Git checkout of `https://github.com/cablate/planseal.git`;
5. whether it contains local modifications.

If the product's skill discovery path is unknown, stop and ask. Do not guess a global destination.

## 2. Show the plan

Before writing, report:

```markdown
## PlanSeal installation plan
- Source: <tag or SHA and URL>
- Destination: <absolute path>/planseal
- Operation: create | fast-forward update | replace reviewed clean checkout
- Files created or updated: see install/MANIFEST.md
- Existing local changes: none | list
- Verification: frontmatter, direct references, UI metadata, version, no out-of-scope writes
- Explicit non-changes: model settings, global agents, project instructions, hooks, MCP, source files
```

Wait for explicit approval.

## 3. Install or update

### New installation

Clone the reviewed release into the verified destination using the folder name `planseal`:

```text
git clone --branch <TAG> --depth 1 https://github.com/cablate/planseal.git <DESTINATION>/planseal
```

If Git is unavailable, download the same tag or commit and copy only the runtime files listed in `install/MANIFEST.md` while preserving relative paths.

### Existing clean PlanSeal checkout

Confirm the remote first. Fetch tags, check out the requested tag, and fast-forward only. Do not discard local commits or modifications.

### Existing modified installation

Stop and show the diff. Offer to preserve it, create a backup, or let the user resolve it. Never reset or overwrite it automatically.

## 4. Verify

Verify all of the following:

- destination folder is named `planseal`;
- `SKILL.md` frontmatter contains `name: planseal`;
- every reference linked directly from `SKILL.md` exists;
- `agents/openai.yaml` references `$planseal`;
- installed `VERSION` matches the requested release;
- no files outside the destination changed.

If the environment provides a skill validator, run it. Otherwise report that structural verification was used.

## 5. Hand off the smoke test

Tell the user to start a fresh session if the product discovers skills only at startup, then run the prompts in `install/SMOKE-TESTS.md`.

Report the final installed path, version, verification evidence, and any manual restart required.

## Updating

Repeat this runbook with a newer release. Show the changelog between the installed and requested versions before approval. An unchanged, clean installation should produce no file changes.

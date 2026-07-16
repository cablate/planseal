# Uninstall PlanSeal

1. Locate the installed `planseal` directory.
2. Verify its `SKILL.md` contains `name: planseal`.
3. If it contains local modifications or files not listed in the runtime manifest, show them before removal.
4. Remove only that directory after user approval.
5. Start a fresh agent session if skill discovery is cached at startup.
6. Verify that `$planseal` is no longer discoverable.

PlanSeal does not modify model settings, global agents, project instructions, hooks, MCP configuration, dependencies, or source code during installation, so uninstalling requires no restoration of those surfaces.

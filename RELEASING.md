# Releasing PlanSeal

Use this checklist from a clean `main` branch.

1. Update `VERSION` and add user-visible changes to `CHANGELOG.md`.
2. Update version-pinned URLs in both README files and the installation runbook.
3. Run the skill validator.
4. Verify every direct link from `SKILL.md` resolves and the runtime manifest matches the repository.
5. Run or manually review every smoke-test case; do not publish benchmark or compatibility claims without recorded evidence.
6. Commit the release changes.
7. Create an annotated tag: `git tag -a vX.Y.Z -m "PlanSeal vX.Y.Z"`.
8. Push `main` and the tag.
9. Create a GitHub release using the matching changelog section.
10. Verify the tag-pinned raw installation runbook and shallow-clone command.

Never move an existing release tag. Publish a patch release instead.

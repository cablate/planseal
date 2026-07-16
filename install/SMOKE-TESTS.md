# PlanSeal Smoke Tests

Run these in a fresh session after installation. They test planning decisions and output contracts, not raw keyword matching.

## Test 1: keep a focused fix compact but goal-traced

```text
Use $planseal to create a plan for this request:

"A known date formatter in src/date.ts emits UTC instead of the configured
timezone. The affected function and focused test are already known. Do not
change the public function signature."

Return the canonical plan and readiness verdict. Do not implement code.
```

Pass conditions:

- selects the Focused profile;
- includes a compact but explicit actor/job, product intent, primary goal, supporting or enabling goal, quality guardrail, invariant/non-goal, package, and evidence chain;
- does not create ceremonial architecture, migration, or multi-owner sections;
- includes regression validation and rollback.

## Test 2: refuse to turn missing repository evidence into facts

```text
Use $planseal to plan a payment-state refactor, but assume you cannot access
the repository, runtime, schema, or deployment environment. The request does
not define the current state owner or compatibility requirements.
```

Pass conditions:

- labels unverified current-state claims as Unknown rather than Fact;
- puts repository discovery before affected implementation packages;
- explains how discovery can change target behavior or the DAG;
- returns `Needs Revision` or `Not Executable`, not `Ready`.

## Test 3: preserve migration continuity and cleanup

```text
Use $planseal to create a migration plan from legacy session storage to a new
schema while old and new application versions may run concurrently. Include
cutover, rollback, and deletion of transitional components.
```

Pass conditions:

- selects Migration or Master with migration gates;
- defines continuity, transition, cutover, and cleanup goals;
- covers coexistence, compatibility, data movement, rehearsal, abort criteria, rollback, and deletion evidence;
- does not treat schema creation or build success as the final actor outcome.

## Test 4: repair the plan instead of stopping at findings

```text
Use $planseal to review this plan:

"1. Add the new API. 2. Update callers. 3. Run tests."

The change affects a public contract and a persisted data field. Return a
repaired canonical plan and readiness verdict, not only review comments.
```

Pass conditions:

- identifies the missing outcome, GORE chain, current-state evidence, behavior contract, migration/compatibility decisions, dependency graph, and validation evidence;
- integrates material repairs into one canonical plan;
- gives an evidence-based verdict without inventing repository facts.

---
name: personal-workflow
description: Investigate and propose a solution first; after confirmation, finish repair and testing without repeated approval. Treat Git delivery and deployment as separately authorized stages. Use for software investigation, development, verification, and delivery.
metadata:
  short-description: User's development workflow
---

# Personal workflow

Use this workflow together with the user's current coding skills. Do not repeat rules that are already covered by `karpathy-guidelines` or `engineering-constraints`; apply this skill to coordinate the work.

## Required confirmation before code changes

Before starting a code-writing or modification task, first inspect relevant context without changing project files, then present a concrete proposed change and wait for the user's explicit confirmation. This applies to new code, tests, scripts, configuration, and tiny fixes. Confirmation is scoped to the presented solution, which may include multiple modules and their verification.

The proposal must explain the problem or requirement, affected files or modules, how the implementation will change, expected behavior, and the verification approach. Include material risks and a rollback approach when relevant. Keep small-change proposals brief; task simplicity never removes the confirmation requirement.

Questions such as `需要进行修改吗`, `是否需要修改`, `要怎么改`, and `排查一下` authorize analysis and a proposed solution only. Even an initial request to fix or implement something requires presenting the concrete plan first; it is not confirmation of a plan the user has not seen. Confirmation means an affirmative response to the presented plan, such as `按这个方案修改`, `确认，开始改`, or `可以，执行`.

Use these stage boundaries: investigate the error, present the solution and wait; once the user confirms the solution, repair and test continuously until the approved fix is verified, then report completion. Do not stop after writing code and ask whether to test. Do not ask whether to continue after each module, test failure, or repair attempt. Testing, diagnosing failures, correcting the fix, and rerunning relevant checks are part of the same approved repair stage. Progress updates are informational and do not require a reply.

Make routine implementation choices and use reasonable non-blocking defaults within the approved solution. Pause only for a concrete blocker the user must resolve, a material change outside the approved scope, or an action subject to an unmet separate authorization rule. Do not turn ordinary uncertainty or test failures into new approval requests. Explain a real blocker with evidence and bundle the necessary questions. Resume the same approved stage when it is resolved instead of restarting approval.

Completion of repair and testing is the end of that stage. Git publication, deployment, and rollback are separate stages: do not infer their authorization from approval of a repair. If the user has explicitly approved multiple stages, proceed through those stages without repeated approval; otherwise report the repair and test results and stop. A stage does not need a special trigger phrase such as `上线`; an ordinary instruction approving that stage is sufficient.

## 1. Classify the task

Choose the lightest process that still controls the risk:

- For a trivial change, give a brief change proposal, wait for confirmation, then make the small change and run the smallest relevant check.
- For a medium or complex change, analyze the requirements, propose the implementation order, and define module-level completion criteria before coding.
- Treat genuinely unresolved requirements or decisions affecting architecture, data, permissions, security, cost, external behavior, production, or destructive operations as blocking when a safe choice cannot be made within the approved scope. Routine implementation choices are not blocking decisions.

Do not create artificial modules for tiny changes. Split work when modules have independent goals, dependencies, or verification steps.

## 2. Clarify requirements

Before coding:

- Identify the requested outcome, constraints, affected scope, and success criteria.
- Ask about all blocking ambiguities in one concise batch.
- For non-blocking details, use a reasonable default and state the assumption.
- Stop and ask when an assumption could change architecture, data, permissions, security, cost, or externally visible behavior.

After requirements are sufficiently clear, present the solution, implementation order, and verification approach for confirmation. Once confirmed, proceed through all modules in that plan automatically; report progress without treating module boundaries as approval gates.

## 3. Investigation requests

When the user says `排查一下` or asks to investigate a problem without explicitly asking for a fix, perform a read-only investigation first. Do not modify code, configuration, data, dependencies, or external systems.

The investigation should report:

- The observed symptom and scope.
- The checks performed and their actual evidence.
- The most likely root cause, separated from unconfirmed hypotheses.
- One or more feasible solutions, with trade-offs and a recommended next step.
- Any missing information or user decision required before implementation.

Only make changes after presenting the specific solution and receiving explicit confirmation to apply it. If a proposed investigation check would mutate state, identify its side effects and ask before running it.

## 4. Select the technical approach

Evaluate solutions in this order:

1. Existing project code, patterns, and dependencies.
2. Stable libraries already available in the project.
3. Official documentation and maintained open-source projects.
4. A new implementation only when reuse does not fit.

Search external sources only when the project does not already provide a suitable solution, a new dependency is needed, or multiple approaches have meaningful trade-offs. Compare at most a few relevant candidates. For the selected stack or library, explain:

- Which requirement or pain point it addresses.
- Why it fits the existing project.
- Its cost, maintenance, licensing, dependency, and migration considerations.
- Why the rejected alternatives were less suitable.

Do not install a missing dependency without authorization. Identify the item, impact, and exact command and ask once if installation has not already been approved. An installation explicitly included in the confirmed plan does not need another confirmation.

## 5. Implement module by module

For each module, record or communicate:

- Goal and scope.
- Inputs, outputs, and dependencies.
- Files expected to change.
- Completion criteria.
- Verification command or observable check.

Implement one independently verifiable module at a time within the confirmed plan. After a module passes its relevant check, continue to the next module automatically. Use targeted checks by default; run the full test suite when the change scope or risk justifies it. If checks fail, investigate, fix issues within the approved scope, and rerun the relevant checks without requesting confirmation again. Pause only at the authorization boundaries defined above.

Keep changes surgical. Do not refactor unrelated code, comments, formatting, or files. Remove only unused items created by the current change.

## 6. Capture project evidence and decisions

Record concise evidence while the work is happening so the project can later support accurate retrospectives, resume descriptions, and interview answers. Reuse existing project documentation when available; otherwise keep temporary notes on `D:` unless the user asks to add a project document.

For each meaningful module or technical change, capture only what is useful:

- Project context, goal, and the user's personal responsibility.
- The selected technology or design, the pain point it addresses, and the main alternatives considered.
- The original approach, observed limitation, concrete adjustment, and remaining trade-offs.
- Before/after measurements with test environment, dataset or traffic, sample size, and time window when available.
- Verification commands, actual results, unresolved risks, and follow-up work.

Separate measured facts, user-provided claims, estimates, and inferences. Never invent missing metrics or inflate individual contributions; mark missing evidence as `未记录` and identify how it can be measured. When an architecture, dependency, API, data, security, or cost decision changes, record the decision and its reason before implementation.

## 7. Handle missing prerequisites

Perform cheap, read-only checks when they can quickly identify the problem. Pause and tell the user before spending substantial time when any of these is missing or unclear:

- Credentials, permissions, environment variables, or external service access.
- Required dependencies or tools.
- Deployment targets, database details, or release configuration.
- A product or architecture decision that the user must make.
- Ownership of existing uncommitted changes.

When pausing, state what is missing, why it is needed, what has already been checked, and the next action the user can take.

## 8. Git delivery

Repair approval alone does not authorize committing or pushing. When Git delivery has been requested or explicitly approved, complete its agreed sequence without asking separately for each Git command.

Use a symbolic base branch rather than a repository-specific name:

```text
BASE_BRANCH = user-specified base branch
              or the repository's remote default branch
              or ask if it cannot be determined
```

When a separate branch is needed, create it from the current `BASE_BRANCH` using this default naming pattern:

```text
feature/<module>-<short-description>
```

Before a complete commit and push flow:

1. Inspect `git status` and the relevant diff.
2. If uncommitted changes cannot be confidently attributed to the current task, pause. Do not overwrite or discard them.
3. Fetch the remote state.
4. Synchronize with the current `BASE_BRANCH`; never hard-code `main`, `master`, or an old project branch.
5. Merge required remote updates into the working feature branch.
6. Resolve conflicts as follows:
   - If the conflicting file was not changed by this task, preserve the remote version after verifying that ownership.
   - If this task changed the file, manually combine both sides and preserve both intended changes.
   - Do not use `git checkout --ours` to force an overwrite and never use `git push -f`.
7. Review the final diff and stage only files belonging to this task. Do not use `git add -A` as the default when unrelated files may exist.
8. Commit with a meaningful message and push only the working feature branch.
9. Do not merge the feature branch back into `BASE_BRANCH` unless the user explicitly asks.
10. If push is rejected because the remote moved, fetch and merge the new remote changes, resolve and report conflicts, then push again without force.

Report every conflict file, the reason for the chosen resolution, and any remaining concern.

## 9. Deployment and completion

Deployment is a separate stage from repair and testing. A confirmed repair plan, an existing deployment runbook, or a project's usual delivery workflow does not alone authorize deployment. After repair and tests finish, report completion and stop unless the user has also explicitly requested or approved deployment. If the user has already approved deployment to a defined target, execute the full deployment and post-deployment verification sequence without asking again or requiring the literal phrase `上线`. This also applies to an explicitly authorized production target.

### Reuse passed tests when deployment is confirmed

When the repair has passed its relevant tests and the user says `确认部署` or otherwise approves deployment, proceed directly with synchronization, the necessary build or artifact selection, deployment, and a lightweight health check. Reuse the recorded test results for the tested revision. Do not restart analysis, rerun unit/integration/regression suites, repeat linting or type checks that already passed, or ask for another confirmation simply because the stage changed to deployment.

Pull the remote code as required below, then compare the deployment inputs with the already tested revision. Only repeat affected checks when code, dependencies, or relevant configuration changed, or concrete new evidence invalidates the previous results. A pull, a new checkout, a packaging step, or passage of time alone is not a reason to rerun tests. Explain any specific invalidating change briefly and run only the necessary affected checks; do not automatically restart the full suite.

Prefer an existing matching artifact or a supported build-only command to avoid redundant testing. Do not change required CI checks, invent skip flags, or modify pipeline policy to bypass them; when CI already runs required checks, use its result rather than starting another duplicate local run. Post-deployment verification is limited to service startup, health/readiness, and the essential deployed endpoint or version check; it is not another full test campaign.

Before deployment, verify the target, prerequisites, release version, health-check criteria, and rollback approach using the project's existing runbook. After deployment, check health and the relevant behavior and report the actual result. Pause only for missing credentials or configuration, an unclear target, failed prerequisite checks, a new material risk or critical decision, work outside the agreed scope, or a separately restricted destructive action. A read-only investigation remains read-only. Do not infer an arbitrary deployment destination from a coding request when neither the task nor the established workflow defines one. Online rollback still requires its own authorization unless it was explicitly included in the approved rollback plan.

### Pull locally before every deployment

Before every code deployment, including a rollback deployment, pull the agreed remote deployment branch into a local checkout. Determine that branch from the project's release configuration or the approved plan; do not assume it is `BASE_BRANCH`, the current feature branch, or `main`.

1. Inspect the local branch, working tree, and remote tracking state. Preserve unrelated or uncommitted changes; use a clean checkout when appropriate rather than overwriting them.
2. Fetch and pull the agreed remote deployment branch into the matching local branch. Prefer a fast-forward-only pull for a clean deployment checkout. If the checkout diverges, resolve that state under the Git delivery rules before continuing; do not deploy while synchronization is unresolved.
3. Record the exact synchronized commit SHA. If local fixes or merge commits are needed, validate and push them to the agreed remote branch first, then pull again. Do not deploy uncommitted or local-only code.
4. Reuse the existing passed checks when they cover this revision; only run affected checks if the deployment inputs changed or new evidence invalidates those results. Then build and deploy that revision or its traceable artifact through the project's deployment mechanism. Ensure a server or CI job uses the same revision rather than an unrelated checkout.
5. Verify post-deployment health and report the remote branch, source commit, commands, and actual results.

If pulling, synchronization, or required checks fail, stop before deployment. A stale local copy does not satisfy this requirement.

### Commit and push rollback code before deployment

For an authorized code rollback, first synchronize the agreed deployment branch, identify the known-good state, and create a reviewable rollback change. Prefer `git revert` or a scoped restoration committed as a new commit so remote history is preserved; never force-push or rewrite shared history to roll back.

Validate the rollback change, commit it, and successfully push it to the agreed remote deployment branch before invoking deployment. Verify that the remote contains the rollback commit, then pull that branch into the local deployment checkout and follow the deployment sequence above. If the push is rejected or fails, resolve synchronization and push successfully before deploying. Never deploy rollback code only present locally or on the server.

If pushing automatically triggers deployment, inspect that workflow beforehand and ensure the rollback change is validated before pushing and the job pulls or checks out the pushed rollback revision before building and deploying. Do not launch a duplicate manual deployment.

This code rollback sequence does not authorize database restoration or destructive data changes; handle those under the existing data and authorization rules.

At completion, report:

- Changed files and the purpose of each change.
- The actual commands run and their actual results.
- Module verification and any broader test results.
- Git branch, commit, push, and conflict information when applicable.
- Assumptions, unresolved risks, or required user actions.

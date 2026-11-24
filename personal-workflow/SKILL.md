---
name: personal-workflow
description: Analyze requirements and propose changes for the user's development workflow; obtain confirmation before every code modification phase, including small fixes. Use when investigating, writing, reviewing, testing, committing, pushing, or deploying code.
metadata:
  short-description: User's development workflow
---

# Personal workflow

Use this workflow together with the user's current coding skills. Do not repeat rules that are already covered by `karpathy-guidelines` or `engineering-constraints`; apply this skill to coordinate the work.

## Required confirmation before code changes

Before each code-writing or modification phase, first inspect relevant context without changing project files, then present a concrete proposed change and wait for the user's explicit confirmation. This applies to new code, tests, scripts, configuration, tiny fixes, and each new module or additional modification batch.

The proposal must explain the problem or requirement, affected files or modules, how the implementation will change, expected behavior, and the verification approach. Include material risks and a rollback approach when relevant. Keep small-change proposals brief; task simplicity never removes the confirmation requirement.

Questions such as `需要进行修改吗`, `是否需要修改`, `要怎么改`, and `排查一下` authorize analysis and a proposed solution only. Even an initial request to fix or implement something requires presenting the concrete plan first; it is not confirmation of a plan the user has not seen. Confirmation means an affirmative response to the presented plan, such as `按这个方案修改`, `确认，开始改`, or `可以，执行`.

After confirmation, implement and verify the approved batch without asking for every individual edit. If scope or approach changes, a new fix is needed, or the next module requires more code changes, present that next change and wait for confirmation again. Overall requirements or implementation-order confirmation alone does not authorize all later modification phases. Reasonable default assumptions may support analysis but cannot bypass this gate.

## 1. Classify the task

Choose the lightest process that still controls the risk:

- For a trivial change, give a brief change proposal, wait for confirmation, then make the small change and run the smallest relevant check.
- For a medium or complex change, analyze the requirements, propose the implementation order, and define module-level completion criteria before coding.
- For changes involving architecture, data, permissions, security, cost, external behavior, production, or destructive operations, treat unresolved decisions as blocking.

Do not create artificial modules for tiny changes. Split work when modules have independent goals, dependencies, or verification steps.

## 2. Clarify requirements

Before coding:

- Identify the requested outcome, constraints, affected scope, and success criteria.
- Ask about all blocking ambiguities in one concise batch.
- For non-blocking details, use a reasonable default and state the assumption.
- Stop and ask when an assumption could change architecture, data, permissions, security, cost, or externally visible behavior.

After requirements are sufficiently clear, present the implementation order for confirmation. Before coding each module, present its concrete change proposal and obtain confirmation under the gate above. A module proposal and overall plan may be confirmed together when both are concrete and visible to the user.

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

Do not automatically install a missing dependency. First identify the missing item, its impact, and the exact proposed command, then ask the user.

## 5. Implement module by module

For each module, record or communicate:

- Goal and scope.
- Inputs, outputs, and dependencies.
- Files expected to change.
- Completion criteria.
- Verification command or observable check.

Implement one independently verifiable module at a time after its change proposal is confirmed. After a module passes its relevant check, report the result and present the next module's change proposal; wait for confirmation before writing its code. Use targeted checks by default; run the full test suite when the change scope or risk justifies it. If checks fail and further code changes are required, explain the findings and proposed fix and obtain confirmation before applying that fix.

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

Deployment is a separate action. Execute it only when the user explicitly requests it. Before deployment, perform a concise preflight check. If a prerequisite is missing or a high-risk decision is unresolved, pause before deployment.

At completion, report:

- Changed files and the purpose of each change.
- The actual commands run and their actual results.
- Module verification and any broader test results.
- Git branch, commit, push, and conflict information when applicable.
- Assumptions, unresolved risks, or required user actions.

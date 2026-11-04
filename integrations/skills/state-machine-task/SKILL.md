---
name: state-machine-task
description: Use only when the user explicitly invokes this skill or explicitly asks to execute a selected task as a state machine with a maintained Beads graph. Continue that selected task within its existing authorization. Do not activate for ordinary coding, a request to explain or draw a statechart, or merely finding open beads.
---

# State Machine Task

Own the selected task from graph construction through evidence-based completion.
Beads (`bd`) stores the issue graph; you decide, execute, verify, and maintain it.
Dependencies determine ready work. They do not launch agents or enforce acceptance.

## Establish scope

1. Identify the user's selected task and explicit authorization for this mode.
   Keep unrelated work outside this graph. An installed skill or an open bead is
   not authorization. A bare “continue” resumes only when the conversation or
   trusted handoff establishes which authorized task it refers to; otherwise
   clarify the task before mutating a graph or dispatching work.
2. Inspect available `bd` version/help and workspace location. If `bd` or its
   workspace is missing, report the prerequisite and prepare the graph design;
   install or initialize only within the user's authorized scope. Never run
   `bd setup` or change project-wide instructions as a side effect of this mode.
3. Reuse the selected root issue if one exists. Otherwise create one epic for
   this task. Record its ID in the current response/handoff so recovery has an
   explicit reference. Inspect the root, descendants, dependencies, and evidence
   before resuming; reconcile in-progress work rather than starting it again.

## Store current state

Keep these current facts on the root using its description or existing metadata;
preserve unrelated fields when updating:

- objective, scope, acceptance criteria, and selected mode;
- current phase and active iteration/attempt issue IDs;
- applicable deadline, cost limits, stop conditions, and authority limits;
- evidence locations, unresolved blockers, and the next permitted action.

Use child issues for executable units with observable completion criteria.
Represent ordering with blocking dependencies, not parentage alone. Each repeated
iteration gets new issues and edges; do not create a dependency cycle to draw a
loop. Keep artifacts in their existing owners and link them from issues. Keep
current graph facts rather than a parallel Markdown checklist or progress diary.

## Execute one transition

1. Select ready work inside the active iteration, not the whole repository:
   `bd ready --parent <iteration-id> --type task --json`. Inspect the returned
   issue and its dependencies. Query nested scopes separately when needed;
   an empty result is not proof the root is complete.
2. Check remaining time/cost and authority before each dispatch. Reconcile an
   unknown prior dispatch with its provider or artifact before retrying; do not
   duplicate potentially paid work. A limit recorded on an issue is not runtime
   enforcement. If the limit cannot be checked, stop dependent dispatches and
   report what must be reconciled.
3. Claim with `bd update <id> --claim`. If claiming fails, inspect current state
   before acting. Delegate only within the user's authorization and assign
   bounded ownership; you retain responsibility for the graph and result.
4. Execute the work and inspect the actual artifact. Record evidence and close
   only the issue whose completion criteria were met. Use non-interactive
   commands, JSON when parsing, and `bd update` rather than `bd edit`.
5. Update the root's current phase and next action. Read back affected issues
   and dependencies after mutations. Resolve partial writes before advancing;
   never use force-closing or dependency removal to bypass a failed gate.

`bd dep add <blocked-id> <blocker-id>` means the first issue waits for the second.
Check installed help before using flags not established by the available version.

## Separate verification from acceptance

A check issue means “produce and inspect evidence.” An acceptance issue means
“the evidence satisfies the agreed criteria.” Make acceptance depend on the check,
and make subsequent growth depend on acceptance. Closing a check that found a
failure must not release growth: leave acceptance open and create/link the repair
and recheck issues that acceptance now depends on. The next ready acceptance
issue may evaluate a result; being ready does not mean the result passed.

For an iterative performance task, start with a small representative workload,
verify telemetry, and establish a baseline before growing it. At a bottleneck,
repair telemetry if necessary, measure a hypothesis, change one cause, and rerun
comparable workloads. Record workload/version identity and correctness evidence
alongside timing. Accept an improvement only on the agreed evidence; then grow
again. A tidy graph or completed benchmark invocation does not prove improvement.

## Stop and recover

On cancellation, limit exhaustion, or an external blocker, stop dependent work,
record the current phase and unresolved operations, and report the root ID and
next safe action. Do not mark the objective complete because the time ran out.
Close the root only when its acceptance criteria and required children are met.
After context loss, recover from the selected root plus evidence, within the
established authorization. Do not adopt unrelated open graphs.

## Upstream reference boundary

[Upstream Beads reference](references/upstream-beads.md) is an unmodified CLI
reference snapshot, not an additional skill or project-wide tracking policy.
Its “First Step”, broad trigger, and shared-project tracking instructions do not
apply to this mode. Do not run default `bd prime` to import broader policy;
inspect only selected issues and needed CLI help. If existing hooks inject broader
guidance, identify the scope conflict rather than silently expanding authority.
See [provenance](references/provenance.md) for the source pin and license.

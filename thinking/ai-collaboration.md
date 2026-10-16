# Working with agents

[中文](ai-collaboration.zh.md) · [Thinking](README.md)

Status: practice, revised as tools and tasks change. This essay applies the
[principles](../principles.md) to coding agents. It argues for autonomy supported
by context and evidence, not a particular model, harness, or staffing plan.

## Give the task a usable shape

An agent needs to know the problem, the result to deliver, the constraints, the
authority it has, and how the result will be checked. Include what is already
known and what remains a decision. A short brief can do this; a template is
useful only if its fields help the recipient act.

“I need to know whether this approach preserves existing behavior so I can
choose a migration plan” is a better investigation than “look at the code.”
Ask a reviewer to challenge the work against criteria, not confirm that the
preferred answer is correct.

For a refactor, name the behavior to preserve and establish a baseline check.
If coverage is missing, use characterization tests for the affected behavior.
An unrelated bug should be reported separately rather than silently expanding
the refactor. An in-scope defect still needs to be handled.

## Isolate the work, including shared state

Concurrent tasks need an arrangement that keeps their changes attributable and
prevents accidental interference. My usual setup is one task per managed
worktree. Check for an existing task before creating another, and use the
environment's manager so its view stays accurate. These are
[working defaults](working-defaults.md), not a claim that every task needs Git.

File isolation is only part of the problem. Two worktrees may share credentials,
an active cloud target, a database, or a deployment environment. Check the
resources the task can actually affect. Before cleanup, verify ownership,
uncommitted work, delivery state, and recoverability.

A team tracker can hold the objective and completion criteria. A small local
investigation may need only an agreed note. The useful property is a task whose
state and outcome can be found, not a ticket created for its own sake.

## Delegate when the handoff is worth it

Parallel work helps when subtasks are substantial, independently answerable,
and permitted by the user and environment. It costs context, coordination,
quota, and attention. Splitting a task by file count rarely tells you whether
the split is useful.

State who can edit, what must remain read-only, who decides, and where the
result belongs. Keep work that depends on the latest correction close to the
main decision. A coordinator should not silently abandon coordination to
implement one of several tasks.

Request a conclusion, supporting references, uncertainty, and unchecked areas.
Keep large artifacts in an agreed location instead of filling the handoff with
raw output. The recipient still needs to inspect evidence behind important
claims. Delegation does not make accountability disappear.

## Choose a setup by the work it completes

Compare model and reasoning settings on representative, authorized tasks.
Useful criteria include correctness, latency, recovery, human intervention, and
total cost. A lookup, an ambiguous investigation, and a long-running change can
favor different setups.

Record the configuration actually used and distinguish unsupported capability,
execution failure, and poor output. Public rankings can suggest candidates;
they do not establish performance in the local workflow. Check current product
documentation before changing model or tool configuration.

Diagnose failure before buying more reasoning. A stronger model cannot supply
missing authority or make an expired credential valid. Preserve attempts and
rejected explanations when changing approach. Once a difficult case is
understood, test whether a cheaper setup handles similar work without losing
the required quality.

## Verify the result the agent is claiming

Connect acceptance evidence to the delivered version and affected environment.
A previous check can remain valid for an unchanged artifact; mutable deployment,
review, or permission state may need a fresh check. A denied read means limited
visibility, not absence.

For a UI change, exercise realistic extremes such as long text and a full list.
Screenshots can show appearance; geometry checks can detect overflow; interaction
and accessibility checks answer other questions. Pick the evidence needed for
the claim rather than treating one technique as sufficient for everything.

Check the actual landing state. A commit on a branch, an open review, a merged
change, and a running release are different results. Inspect the current review
state before publishing more work to its branch. The handbook's
[delivery case](../handbook.md#delivery-en) shows why a successful push can leave
the requested result undelivered.

Independent review should scale with risk. Another reviewer can expose a missed
assumption, but agreement does not grant authority or prove safety. A check that
ran on no eligible inputs must not look like a successful validation.

## Turn recurring friction into a tested improvement

When corrections repeat, first identify their cause. Missing context, ambiguous
intent, a subjective preference, and a detectable defect need different
responses. A reliable validator can protect an invariant; an unreliable signal
may be better as diagnostic feedback.

For example, detecting whether a verification tool ran cannot establish whether
it checked the right thing. Evaluate a proposed gate against real failures,
misses, false alarms, and intervention cost. An advisory trial may help where
it is safe; it must not quietly remove required protection.

A recurring procedure can become a maintained, on-demand guide. Keep tool
commands with that guide, and keep standing instructions small. Recheck mutable
facts when they matter, especially after changes to the model, harness, or
environment. A calendar age alone cannot establish freshness.

Keep credentials and sensitive source material in their authorized systems.
Useful shared knowledge is not the same as a copy of every conversation.

## Audit for learning, not a productivity score

Use session history only with appropriate access and disclosure limits. Remove
injected instructions, tool output, and duplicate events from analyses intended
to describe human input; inspect samples because role labels alone are not enough.

Delivery records can reveal waiting, repair, abandoned approaches, and repeated
intervention. They need interpretation: a closed, unmerged PR may be a useful
experiment; a pause between messages may be human absence; more merged PRs may
be smaller units of the same work. None alone establishes a productivity gain.

Choose a small number of improvements tied to observed friction, then check
whether they helped. A repeat correction may mean the guidance was missed, but
it may also mean the rule was wrong or the task changed.

## Know when to change course

Stop for missing authority, a consequential ambiguity, or a conflict that changes
the agreed result. Do not repeatedly ask permission for ordinary steps already
within scope. Respect a denied operation; do not disguise it as another command.

Growing compensating changes, repeated failures in the same area, and pressure
to disable checks are reasons to revisit the hypothesis. State what the evidence
supports, what contradicts it, and the next useful alternative. A fixed retry
count or diff-size multiplier is a prompt to think, not proof that a design failed.

For taste or product ambiguity, make the choice visible. Offer viable options
and criteria, or ask the person who owns the decision. More execution cannot
resolve a decision that has not been made.

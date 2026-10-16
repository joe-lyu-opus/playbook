# Teams working with agents

[中文](ai-native-teams.zh.md) · [Thinking](README.md)

Status: practice synthesis. This essay applies the [principles](../principles.md)
to team design; it does not prescribe a fixed organizational model.

These notes concern the conditions that let people and agents work together:
usable tools, clear responsibility, shared knowledge and evidence of results.
They do not assume that agents write most code or that people should stop
implementing things themselves.

The sources include local workflow documents, selected change history, and
personal AI sessions. A written process establishes an intention; a merged
change establishes implementation; neither establishes
adoption or benefit. Detailed research records are not included in the shared edition.

The examples below are generalized situations, not profiles of identifiable
teams. The methods need to be tested against a new team's risks and constraints.

## 1. Make experimentation accessible, with bounded responsibility

A person with an idea should be able to try it without learning the whole
platform. Provide a supported starting point, an understandable first result,
and a way to find help. Shared capabilities are useful when they remove repeated
work without making every exception a platform ticket.

Internal use is not a safety classification. A small prototype can still expose
sensitive data, incur substantial costs or change a shared service. Choose the
controls from the actual data, authority, dependencies and recovery options.
Directory boundaries can help route checks, but they are only a proxy for risk.

When an experiment becomes something people depend on, review responsibility,
data retention, failure recovery, support and release evidence. Moving a folder
or applying a label cannot do that work. A reviewer should be able to distinguish
what was checked, what was accepted as a limitation and what remains unfinished.

Retirement also needs a supported path: confirm ownership and dependencies,
notify affected users, preserve required data, remove runtime resources and
check that the removal occurred. Existing authorization can permit automated
steps; a second manual approval is not always necessary. Unclear authority or
irreversible loss requires a decision, not another retry.

To test this in a new team, follow one modest experiment through first use and
retirement. Record where its owner needed hidden help. Do not claim a return on
the platform from the number of generated applications alone.

## 2. Treat tool adoption as part of the product

Several tool categories expose useful questions:

| Tool category | User problem | Method to carry forward | Condition to check |
|---|---|---|---|
| Publishing | Useful work stays in a private session or local file. | Connect creation with authorized sharing, feedback, revision and retrieval. | A stable link still needs correct access and a recognizable current version. |
| Capability discovery | People rebuild something that already exists. | Search by the task, with links to inspectable sources. | Who updates the index, and can the reader access the source? |
| Reference examples | “Good” means different things to different people. | Explain strong and weak examples against a stated goal. | Examples must be permitted, relevant and replaceable when the goal changes. |
| Shared agent plugins | A workflow works only on its author's machine. | Give users a first-use path and diagnostics that test real capability. | Installation and binary presence do not prove authentication or workflow readiness. |

Build a small extension when it supplies organizational facts a generic agent
lacks: current responsibility, local rules, supported verification and recurring
failure knowledge. Reimplementing generic planning or maintaining a second copy
of tracker state needs a stronger justification.

Keep personal experiments distinguishable from capabilities the team promises
to maintain. State who supports a tool, what it may read or change, and how to
stop using it. A repository being accessible internally does not grant rights to
redistribute it elsewhere.

## 3. Give shared knowledge a dependable write and read path

Assign an authoritative source to each kind of fact. Work status can remain in
the tracker, runtime state in the running system and decisions in a maintained
document. Shared context does not require one repository to contain everything.
Use references instead of independent copies that people must reconcile.

Make routine observations easy to record, while keeping changes to policy,
permissions and shared instructions subject to appropriate review. Tell the
writer whether a note is published, awaiting review or failed. A draft or an
unmerged branch must not masquerade as accepted guidance.

Retain enough context to judge a note: what was observed, under what conditions,
where the evidence lives and whether the statement is observation, proposal or
accepted decision. Important guidance needs an owner and an explicit route to
replacement or retirement. Old references should lead to their replacement.

A knowledge inbox needs a real reason to be processed. Repeated confusion,
growing unresolved material or a change to the relevant system can trigger
review. Then decide whether the observation belongs in a guide, tool, check or
nowhere permanent. A weekly calendar entry alone is not evidence of maintenance.

Protect private conversations and personnel information. Meeting capture and
other collection must have the necessary permission, limited readership and
retention. A shared knowledge tool is not a reason to ingest everything.

## 4. Separate responsibility from execution

An agent can propose, implement and investigate; someone still needs authority
to accept the change and responsibility for the affected service. These roles
may involve different people. Merely requesting work does not make someone the
owner of every resource that work might touch.

A handoff should state the outcome, context, constraints, completion evidence,
known failures and unresolved decisions. Add timing when it matters. The
recipient should know which actions are already authorized and which require a
new decision. Research or diagnosis does not imply permission to mutate state.

Automated review creates findings, not truth. Inspect each concern against the
current version, fix valid issues, explain declined suggestions and keep a
verifiable disposition. A resolved thread or a green check is evidence only
for what it actually establishes.

For important changes, seek a challenge to the assumptions rather than merely
another approving verdict. Different reviewers or models can help, but vendor
diversity does not guarantee independent reasoning. Bound repeated review by
the remaining risk and new information; avoid an endless loop of speculative
style changes.

## 5. Verify behavior, then evaluate the verification

Choose evidence to fit the claim. A deterministic test can establish a logic
property. An integration check can exercise a boundary. A deployed check can
test real identity and configuration. A human inspection can reveal a confusing
interaction. These are neither interchangeable nor a mandatory ladder for every
change. A check that found no eligible objects needs an explicit result.

For model behavior, define representative, authorized cases and the comparison
criteria before choosing a winner. Record what was actually submitted. Separate
unsupported requirements, failed execution and poor outputs. Retain examples
where people disagree with an automated judge and investigate the disagreement.
Use blinded comparison when prior labels could bias the answer. Report coverage
and uncertainty, not only an aggregate score.

Evaluate controls too. Ask whether a check catches relevant failures, how much
delay and false alarm it creates, and whether people bypass it. A costly
mechanism may need replacement while its objective remains valid. An advisory
experiment must not silently remove required security or financial protection.
Measure the replacement before describing it as an improvement.

After a failure, separate observed facts from explanations and ask where the
problem could reasonably have been prevented or detected. A new gate is one
possible response. Fixing a dependency, simplifying a design, clarifying
ownership or accepting a documented residual risk may be more appropriate.

## 6. Make culture visible in ordinary work

Useful cultural questions are concrete: Can a newcomer ask for help? Can someone
challenge a choice without having to own the whole project? Is the reason for a
decision available? Does the person carrying responsibility have the authority
to act? Can a maintainer take time off without the work stopping?

Explain progress around outcomes. Combine records that describe the same result,
separate completed work from plans, and state what the reader needs to decide
or do. Attribute leadership, contributions and dependencies accurately. A bulk
ticket update is not a burst of new delivery.

Give proposals a clear disposition and explain what would reopen them. Public
discussion can reduce repeated explanations, but private personnel matters and
sensitive disagreements need an appropriate channel. Transparency has an
audience and a purpose, not unlimited readership.

## 7. Let the working method change

More agent output can move the bottleneck to review, product decisions or human
energy. Track useful completed work, repair load, waiting and intervention, not
just activity. When the team cannot absorb additional changes, reducing work in
progress and making room for recovery may help more than increasing generation.

Model choices, role assignments and review cadence are revisable decisions.
Compare total cost, including rework and human attention, on representative
tasks. Reuse what works while recording the evidence that would justify a
change. A fixed model map is not a permanent organizational principle.

A ritual needs a trigger, a useful result and someone able to act on that
result. Repeated non-use calls for investigation: perhaps the need disappeared,
the timing is wrong, or the process costs too much. Do not add reminders until
you know the ritual still helps. Low observed use alone is insufficient grounds
to delete a rare but important recovery tool.

## 8. Try the method without importing the organization

Choose one current problem with the team. Describe the observed friction and
what would count as improvement. Check the data, permissions, maintenance owner
and recovery path. Try a bounded change and compare the result with the starting
point. Keep, revise or retire the practice according to what you learn.

For example, a slow first deployment may need better onboarding rather than a
new platform. A crowded review queue may need smaller changes rather than
another reviewer. A neglected knowledge store may need an easier write path or
less material, not a new weekly meeting. These are diagnostic alternatives,
not claims about the original teams.

Bring the questions and decision methods. Leave internal code, datasets,
samples, private discussions, product plans and identifiable case histories in
their authorized systems. Public articles can be cited with attribution;
internal availability does not imply permission to export.

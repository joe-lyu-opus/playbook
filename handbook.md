# Engineering judgment and practice

[中文](handbook.zh.md) · [Home](README.md)

This handbook puts the ideas to work together. [Principles](principles.md) owns the durable decision criteria; [taste](taste.md) owns personal preferences. The chapters develop their application through constraints, tradeoffs, and cases. Tool-specific practices and proposals live in [thinking](thinking/README.md).

A practice handbook · 2026-10-12

Choose worthwhile problems, make defensible decisions, deliver useful results, and help others repeat the work.

This handbook draws on engineering practice, reflections in AI conversations, and team workflows. Its subject is the reasoning behind a practice: when to use it, what evidence it needs, and when to change it.

The chapters follow work from an initial request to a team that can sustain the result. They are not a prescribed sequence. Authority, maintenance, and collaboration shape the first decision; evidence from use can send the work back to its original question.

Read this as a set of working judgments, not a mandatory process. Case notes distinguish recorded experience, lessons drawn from other practices, and hypothetical examples. Where a source records an intention but no measured result, the account stops there.

Internal material contributes generalized problems and reasoning, not implementation details. The English and Chinese editions share the argument and evidence; their paragraphs are not intended to match.

1. [Choose a problem worth solving](#purpose-en)
2. [Build a reliable account of reality](#evidence-en)
3. [Make tradeoffs under constraints](#simplicity-en)
4. [Follow the work through to a result](#delivery-en)
5. [Divide work between people and AI](#delegation-en)
6. [Bound the impact and plan recovery](#safety-en)
7. [Write for the next decision or action](#communication-en)
8. [Make the work possible for others](#platform-en)
9. [Build culture into everyday work](#culture-en)
10. [Manage quality and delivery capacity](#learning-en)
11. [Turn experience into usable knowledge](#knowledge-en)
12. [Reapply the reasoning in a new setting](#transfer-en)

[Sources and limits](#sources-en)

| Layer of work | Useful output | Test of that output |
| --- | --- | --- |
| Judgment | A worthwhile problem, relevant facts, and a reasoned choice | What evidence would change the decision? |
| Delivery | A result within the agreed constraints, with a recovery path | What can the next person rely on? |
| Collaboration | A way for others to contribute, use, and maintain the result | Does it work without the author filling in gaps? |
| Improvement | A change to the method, informed by feedback | Does the original problem recur less often? |

<a id="part-one-en"></a>

## Part I. Decide what deserves doing

Understanding the need and its constraints comes before choosing an implementation. A sound decision may lead to a build, an investigation, a limited experiment, or no change at all.

<a id="purpose-en"></a>

### 1. Choose a problem worth solving

Decision criteria: [Outcome](principles.md#outcome).

Requests often arrive as solutions: build a platform, add a button, switch models. Before accepting that framing, find the person who is blocked, the circumstances, and their current workaround. Fast implementation can make an untested assumption expensive to undo.

#### Describe the change you want to see

A useful objective connects the current situation to a desired change and explains how to tell whether it happened. When no reliable baseline exists, observe a real user completing the work before inventing a numerical target. Feedback can explain a difficulty; behavior records can show whether it recurs. Neither gives the whole picture.

- Consider doing nothing, handling the work manually, and improving an existing tool alongside building something new.
- Weigh benefit, urgency, failure cost, and maintenance. A rare but severe failure may deserve priority over a frequent nuisance.
- Name what the work excludes. New requests need a place to go without silently expanding the current commitment.
- Use research or a small experiment to resolve uncertainty that matters to a decision.

#### Case: a platform milestone that a user can complete

*Hypothetical application of a milestone discussion found in the sessions; not a reported delivery result.*

A team wants new services to reach deployment sooner. A plan organized around authentication, templates, and deployment components can finish every component while leaving the user dependent on manual setup.

Try defining the first milestone as a complete path instead. One intended user should be able to deploy without borrowing the maintainer's identity, recognize a failure, and find help. Observe waits, interventions, and steps with no practical recovery. Those observations tell the team which capability to improve next.

One successful path establishes feasibility for that case. It does not establish broad adoption. Test users and workloads with different needs before making that claim.

A clear problem narrows the investigation. Resolve the unknowns that could change the choice before researching every implementation detail.

<a id="evidence-en"></a>

### 2. Build a reliable account of reality

Decision criteria: [Evidence](principles.md#evidence).

“The query returned no workloads” is an observation. “The workloads were deleted” is an explanation. Before acting on the explanation, rule out a different environment, insufficient access, a filter, or stale data.

#### Ask what each check can distinguish

Establish the target, identity, version, and time behind the evidence. Then compare plausible explanations and choose a check that separates them. A successful exit code says the check ran; if it inspected nothing, it cannot establish that everything passed.

When attempts keep failing in the same place, stop repeating them. Write the current explanation, evidence for and against it, and the next discriminating check. Missing access, unavailable tools, and faulty reasoning call for different interventions. A stronger model will not renew an expired credential.

#### Case: a valid query against the wrong environment

*Generalized from an existing practice note; the incident was not reproduced for this handbook.*

The note describes a query that completed normally but returned none of the expected objects. Another session had changed the selected environment. The query was answering a different question from the one the operator intended.

Recreating resources would have extended the mistake. Checking the target would distinguish an empty system from the wrong system. The same reasoning applies to a report's date range, a document revision, or a test environment: establish what was observed before explaining it.

#### Investigate until the decision is supported

More information is useful when it could change the choice. A reversible, low-impact decision can proceed with stated uncertainty. Shared permissions and irreversible data changes need stronger evidence. Under time pressure, narrow the action rather than turning missing evidence into certainty.

The aim is not to know everything. It is to expose the unknowns that matter enough to affect the tradeoff.

<a id="simplicity-en"></a>

### 3. Make tradeoffs under constraints

Decision criteria: [Whole cost](principles.md#whole-cost) · [Personal preferences](taste.md).

I judge simplicity by the work left for everyone who follows: understanding, integration, diagnosis, upgrades, and eventual removal. A short implementation may be a good choice. It may also transfer complexity to every user.

Inspect existing capabilities first. Reuse reduces the surface to maintain, but adapting indefinitely to the wrong assumptions can cost more than a new implementation. Compare building, buying, and manual handling through lifetime cost, control requirements, and the difficulty of leaving the choice behind.

#### Change the boundary that owns the problem

- If the shared rule is wrong, inspect its consumers and repair the shared rule.
- If one consumer is different, express that difference without changing everyone else's behavior.
- If ownership, state, and documentation contradict each other, reorganizing the boundary may leave less work than another patch.
- Add abstractions for real variation. Add state only with a credible way to keep it accurate.

#### Case comparison: remove ceremony or reorganize the whole boundary?

*Two requests in AI sessions. They establish the requested tradeoffs, not the results of implementation.*

One discussion concerned a one-time migration with accepted downtime. A complicated pilot process needed justification. Another explicitly called for a full cleanup because local rules and documentation had become contradictory.

The consistent preference is not the smallest diff. It is the least remaining burden after the complete objective has been met. A step designed to protect continuous service may be unnecessary in the first situation; repeated local fixes may be the source of cost in the second.

Accepted downtime does not imply accepted data loss. Staging, cutover, and preservation still require their own decisions.

For a consequential choice, record the option selected, alternatives rejected, supporting evidence, and conditions for reconsideration. Routine reversible decisions need less ceremony. The record should help the next person understand the choice, not create an approval process for every action.

<a id="part-two-en"></a>

## Part II. Turn decisions into dependable results

A sound direction still needs dependencies, ownership, and verification. Keep comparing the plan with actual state as the work proceeds.

<a id="delivery-en"></a>

### 4. Follow the work through to a result

Decision criteria: [Completion](principles.md#completion).

Break work into stages that retire an important uncertainty or make something usable. “Three modules implemented” reports activity. “An intended user can complete this operation” gives the next person something to build on.

#### Resolve dependencies before they become rework

Identify decisions, shared resources, and external dependencies that constrain later work. More implementation is often wasteful while an identity or interface agreement remains unsettled. Name who will advance each dependency; another team's cooperation is not an established fact until it has been agreed.

When scope changes, revisit acceptance, cost, and commitments. When work pauses or changes hands, preserve the current state, verified version, failed attempts, open questions, and next action. “Mostly done” is a poor substitute for that handoff.

#### Case: the push succeeded, but the change did not land

*A failure recorded in personal workflow rules, with identifying details removed.*

A change was pushed to a branch whose pull request had already merged. The command succeeded. The new commit did not reach the intended base branch.

The mistake was in the completion test: upload success had been treated as delivery. My resulting check is to confirm that the delivery path is still valid, then verify the commit at the destination I claim. A claim about a live feature needs deployment and behavior evidence as well.

This applies beyond code. Sending a message does not establish a decision; generating a report does not establish that its recipient can use it. Verify the state the next person depends on.

#### Separate acceptance from benefit

A test establishes behavior it exercised. Benefit needs evidence from use. Where an observation period is necessary, record technical delivery and outcome follow-up separately, with someone responsible for the latter. The implementation task need not remain open forever, but an expected benefit must not become an achieved result on release day.

If observations fail to support the objective, revisit the problem or approach. Completion includes the possibility of revising or withdrawing a change.

<a id="delegation-en"></a>

### 5. Divide work between people and AI

Decision criteria: [Authority and recovery](principles.md#authority).

Assign work according to the capability and authority it requires. Use deterministic tools for known transformations. Delegate independent investigation or implementation. Bring conflicting goals and resource commitments to someone entitled to decide them. Delegating execution to AI does not transfer accountability.

#### Give the recipient room to make good decisions

A useful brief establishes the desired result, its purpose, constraints, authorization, and completion evidence. Add relevant facts, failed attempts, and unresolved questions. The point of context is to preserve distinctions that affect choices, not to supply the longest possible prompt.

Let routine work continue within its agreed boundary. Escalate missing authority, a failed assumption, or a choice with materially different consequences. Existing authorization need not be renewed at every step, but permission to investigate does not imply permission to implement.

#### Case: integrate with a product without taking it over

*A scope correction in a personal AI conversation.*

While integrating with another maintainer's product, I asked for the authorized integration to be completed first and broader redesign to be discussed with the maintainer. The ability to edit code did not confer ownership of compatibility, maintenance, or the product's priorities.

I separate those outputs: a verified integration and a reasoned proposal for broader change. If the current design blocks integration, expose that conflict for a decision rather than quietly expanding the task.

#### Count coordination and repair in the cost

Parallel work pays when tasks are sufficiently independent and their outputs can be checked. Isolate files and state, agree interfaces, and assign responsibility for integration. Multiple workers maintaining conflicting versions of the same fact create coordination work.

Compare models through accepted results, rework, latency, spending, and human attention on representative tasks. Extra reasoning should add evidence or a plausible alternative. Repeated agreement is not independent confirmation. Set budgets and stopping conditions before the task consumes them.

<a id="safety-en"></a>

### 6. Bound the impact and plan recovery

Decision criteria: [Authority and recovery](principles.md#authority).

Find the actual affected resources and people before changing anything shared. Repository boundaries, organizational charts, and effective permissions do not necessarily line up. An internal label or a small audience says little about the consequence of failure.

#### Give shared state a clear owner

Each shared resource needs a maintenance responsibility and an update mechanism. Two tools enforcing different copies of the same configuration can undo each other's work. Record emergency changes and reconcile them with the maintained source.

Automation identities should have only the access the task needs. Keep credentials out of prompts and documents. Make the supported access path usable during incidents as well as routine work; an unusable safe path encourages workarounds. Agree stop conditions and recovery responsibility before high-impact changes.

#### Case: a permission change crossed repository boundaries

*An incident lesson in the existing practice notes, without implementation or organizational details.*

A permission reduction was checked against the current repository. Another repository relied on the same build identity and subsequently lost access.

The lesson is to trace effective identities and dependencies instead of inferring scope from the current directory. Before a similar change, identify consumers, verification, and recovery; where possible, narrow the initial change and observe dependent behavior. These are recommendations drawn from the case, not a reconstructed account of steps taken during it.

#### Choose risk in light of recovery

Restoring old code may not undo a data change. Plan data movement, traffic switching, and read/write compatibility separately. Recovery might require compensation or a forward repair rather than a rollback.

When a prototype becomes something people depend on, revisit maintenance, retention, release evidence, and incident handling. Retirement needs the same care: establish dependencies, notify users, retain required data, remove running resources, and verify the removal. A source deletion or status label does not complete that lifecycle.

These boundaries become the basis of communication: what changes, who must act, and who can respond when it goes wrong.

<a id="part-three-en"></a>

## Part III. Make the result sustainable for a team

A successful individual task can depend on a great deal of unwritten judgment. Sustaining the result means giving other people a way to participate, use it, and handle trouble without the author present.

<a id="communication-en"></a>

### 7. Write for the next decision or action

Decision criteria: [Enablement](principles.md#enablement).

Before writing, decide what the reader needs to do: understand a situation, choose an option, act on a change, or take over the work. That purpose determines the detail. The effort spent on an implementation does not entitle it to the same amount of space in every update.

#### Organize information around the reader's job

Lead a progress update with results and unresolved work, then evidence. Lead a proposal with the decision, alternatives, and costs. Lead a notice with impact, timing, required action, and a contact. Link implementation detail so readers do not have to reconstruct the whole project.

#### Case: one change, three explanations

*Hypothetical example of audience-specific communication.*

Suppose a team will change the entry point for its preview service. Users need to know whether they are affected, when it happens, what becomes of old links, what they must do, and where to ask for help.

The maintainer needs the version, dependencies, checks, operational signals, and recovery steps. A decision-maker needs the problem being solved, remaining risk, and tradeoff to accept.

These explanations share one set of facts. If the date is undecided, it stays undecided in all three. A neat notice is not a reason to invent a commitment.

#### Locate the disagreement before trying to settle it

Disputes about facts, goals, risk tolerance, and authority need different responses. Gather evidence for factual disputes. Ask for a tradeoff when goals conflict. Clarify responsibility when decision rights are missing. Another implementation cannot settle any of those by itself.

State your recommendation, why you hold it, and what would change your mind. Give declined proposals an explicit disposition rather than indefinite silence. Keep commitments conditional until dependencies are agreed, and update affected people early when a commitment is at risk.

For shared results, combine duplicate tickets and commits into one account. Distinguish leadership, contribution, and help from others. Make your work visible by describing its specific effect, not by claiming the team's entire result.

<a id="platform-en"></a>

### 8. Make the work possible for others

Decision criteria: [Enablement](principles.md#enablement).

A tool earns its place through the work its intended users can complete. Installation, a feature list, and a smooth author-led demo each establish only part of that. Watch where a user starts, where they get stuck, and whether they can recover.

#### Case: the migration was finished, but who could repeat it?

*A reflection in personal input history. Later adoption results have not been verified.*

I recorded a concern that I had performed migration work that should have involved the consuming teams. Completing it myself could solve the immediate problem without establishing that the platform made the work repeatable for others.

Whether taking over was appropriate depends on the objective. In an urgent recovery, direct intervention may be right. When the objective is repeatable onboarding, the user must eventually complete the path.

A better experiment would be to work through one representative example together, then let the user operate it while recording every maintainer intervention. Missing concepts need explanation. Reliable but tedious steps may warrant automation. A broken interface needs a product change. “More documentation” is not the answer to every obstacle.

Check the next attempt as well as the first success. Can the user diagnose a failure and get appropriate help without the same person filling the same gaps? This is a proposed way to test improvement, not a claim that the later rollout succeeded.

#### Design the path around the work

Users first need to discover the capability. Organize entry points by their tasks and link to inspectable sources. First use should test identity, dependencies, and environment, with failures that suggest an action. Repeated use needs a stable interface, a compatibility expectation, and someone responsible for support.

#### Case: getting an AI-generated artifact into team use

*A lesson drawn from a team's publishing-tool descriptions, not a reproduction of its implementation or measured adoption.*

An analysis completed in a private conversation still needs a place to be shared, appropriate reader access, feedback, revision, and a way to find the current version later. If the author assembles that path manually every time, each artifact creates the same coordination work.

The transferable design choice is to connect those actions. Readers need to recognize the content, judge whether it is current, and leave feedback. Authors need to see what feedback was addressed and who a revision affects.

Test the whole path with a real reader: open, understand, respond, and find it again. Generating or publishing a file proves less than successful collaboration. If existing tools already support the path, improve their entry points and conventions before building another system.

Shared capabilities bring shared costs. Standardize only where assumptions genuinely hold, and support legitimate differences. Distinguish personal experiments from capabilities the team commits to maintain. Know how users can leave a dependency before asking them to adopt it.

<a id="culture-en"></a>

### 9. Build culture into everyday work

Decision criteria: [Enablement](principles.md#enablement).

I learn more about a team's culture by watching a newcomer get stuck than by reading its stated values. Can they get help? Does a question receive an explanation? Can the person held responsible actually make the required decision?

#### Make autonomy workable

Independent work needs information, authority, and feedback. Assigning a goal without the means to pursue it turns responsibility into pressure. Requiring a lead to approve every choice turns that lead into a queue. Agree which decisions people can make, which require coordination, and where to take an exception.

#### Case: use a real task to introduce the work

*A hypothetical onboarding example, not a reported outcome.*

Give a newcomer a real change with limited impact, accessible background, a peer they can ask for help, and clear acceptance criteria. Let them propose the approach, implement it, and explain their verification. The peer supplies missing context and challenges risk where needed.

This exposes more than whether the newcomer can finish. It reveals missing entry points, undocumented decisions, stalled access requests, and slow feedback. Treat those as possible environment defects rather than attributing every delay to the person's ability.

Match the task and decision space to experience and risk. Learning does not justify unauthorized production exposure, and asking for help is not failure.

#### Reduce dependence on constant intervention

A lead can teach by demonstrating judgment, explaining tradeoffs, and working through difficult cases with others. Over time, transfer decisions people can reasonably own, not just execution steps. Ask whether the work survives a maintainer's absence rather than how many tasks were assigned.

Accessible decision records reduce repeated explanation. They do not justify unrestricted access to personnel matters, private conversations, or sensitive disagreements. People must also be able to report insufficient capacity. A delivery method that routinely depends on overtime needs revision.

<a id="part-four-en"></a>

## Part IV. Keep the method useful as conditions change

Repeatable work can still become obsolete. Quality controls, shared knowledge, and team routines need feedback. When output increases, watch whether the rest of the organization can absorb it.

<a id="learning-en"></a>

### 10. Manage quality and delivery capacity

Decision criteria: [Feedback](principles.md#feedback) · [Whole cost](principles.md#whole-cost).

Faster implementation can move the queue to review, integration, release, or product decisions. Measure the path from a need to an effective result, including rework, failure, and human effort. Starting more work may make every item finish later.

#### Make quality discussable

Quality criteria come from the intended use. With examples you are authorized to use, show what succeeds or fails and why: accuracy, comprehension, interaction, or another requirement. Replace a bare preference with its practical consequence so others can challenge the judgment.

For model evaluations, establish that the comparison is valid before selecting a winner. Use representative cases and consistent criteria, and record the actual inputs. Separate unsupported capabilities, execution failures, and poor output. Silently dropping failed runs makes the remaining results misleading. Keep cases where human judgment and automated scores disagree, then investigate the difference.

#### Case: a quality gate keeps blocking ordinary work

*Generalized analysis of team decision and change records. A changed mechanism does not establish a measured improvement.*

The collected material includes a decision to move from a restrictive mechanism toward observation and feedback, with related implementation changes. The useful lesson is to examine three things separately: the control objective, its detection signal, and the action taken on that signal.

Consider a check intended to discourage completion claims without verification. Recorded verification activity is evidence that something ran, not that it proved enough. Missing activity can also reflect incomplete logging. Treating either signal as a complete quality judgment can miss defects and block valid work.

Inspect real failures and false alarms before changing the rule. Is the standard wrong, the detection weak, or the response disproportionate? An advisory trial may help calibrate an appropriate rule, but it must not silently remove required security or data protection.

After changing the mechanism, compare missed failures, delay, and workarounds. Fewer gates or more green checks do not by themselves establish better quality.

Review findings deserve the same scrutiny. Check them against the current version and record whether they were fixed, declined, deferred, or superseded. A different reviewer or model can add perspective, but agreement does not establish independent evidence.

When downstream queues and repair work grow, reduce work in progress, address the constraint, and reserve capacity for recovery. Quality recovery belongs in the delivery plan, not perpetually outside working hours.

<a id="knowledge-en"></a>

### 11. Turn experience into usable knowledge

Decision criteria: [State and ownership](principles.md#state) · [Feedback](principles.md#feedback).

A retrospective does not owe the organization a new rule. First explain the failure and where it could reasonably have been prevented or detected. Missing knowledge may call for a note, a difficult interface for a tool change, and conflicting responsibilities for an ownership decision. A cheap, isolated exception may need only a record.

#### Let observations earn their way into shared practice

Make routine capture easy and require stronger grounds for a standing rule. A useful note tells the next reader what happened, under what conditions, and whether it is an observation, proposal, or accepted decision. Promote recurring, useful findings into guidance, tools, or checks; then look for a reduction in the original problem.

#### Case: written down, but unavailable to the reader

*Generalized from a team knowledge-maintenance record.*

A record described notes left in unmerged pull requests. Writers believed the information had been saved, but readers could not obtain it through the shared entry point. Search alone could not repair the mismatch.

The improvement to test is a write path that makes draft, pending review, and published states explicit. Routine observations need a low-friction entry point; common rules can retain appropriate review. Retrieval must also tell the reader whether it found a proposal or current guidance.

Related material noted that a written weekly cleanup ritual had not actually run. A maintenance process needs a trigger, someone who acts on it, and somewhere for the result to go. Repeated questions, a growing backlog, or a system change can supply the trigger.

#### Retire knowledge as deliberately as you publish it

Identify an authoritative source for each kind of fact and prefer references to independent copies. Work state, runtime state, and design decisions can remain in different systems. Written policy, implemented behavior, and observed effect are distinct; none should stand in for the others.

Give guidance a maintainer, a reason to revisit it, and a visible replacement when it expires. Keep standing instructions focused on recurring information that is difficult to discover. Tool commands belong with the tool's documentation. When models, responsibilities, or workflows change, remove obsolete rules rather than stacking exceptions on them.

Knowledge is useful when the next person can make a better decision or complete the work more reliably. Document counts, rule counts, and page views are clues, not that outcome.

<a id="transfer-en"></a>

### 12. Reapply the reasoning in a new setting

Decision criteria: [Feedback](principles.md#feedback).

In a new team, start with a recent delivery and a difficult failure. Trace how the objective was chosen, who decided, where people waited, and what made errors costly. Understand what the existing practice protects before proposing a replacement.

Separate principles that need continued testing, negotiable personal preferences, local organizational conventions, and one-time exceptions. A model assignment, branch name, or review cadence that worked once is not a universal rule.

#### Worked example: “Build us a knowledge assistant”

*A hypothetical scenario connecting the chapters; not an internal product description or reported outcome.*

Begin by observing what users fail to find and how they currently look for it. If the source material is stale, a chat interface may not help. Narrow the objective to finding current answers within an authorized collection, with sources the user can inspect.

Establish ownership, access, freshness, and existing search capabilities. Compare a better index, content maintenance, and a new assistant. Choose a trial that resolves an important uncertainty. Use authorized, de-identified examples to test retrieval and attribution; permission to test does not grant permission to write or share source material.

At delivery, check the answer, source version, and access boundary separately. Have an intended user find an answer, recognize stale information, and report it. A demo alone does not establish that path. Expansion also requires someone able to maintain the sources.

If stale content remains the obstacle, improve maintenance first. If repeated searches decrease, test additional situations. Stop the trial if it provides no benefit or creates excessive upkeep. Preserve the decision and its limits rather than turning every experiment into a permanent tool.

#### Use the method outside software

A report starts with the decision its reader must make. Research targets questions that could change a choice. A cross-team project needs agreed dependencies, commitments, and acceptance. Learning a new field can start with a small task that gives feedback, followed by practice aimed at the errors. These activities share a reasoning structure, not a mandatory ticket system.

A short working record is often enough: the problem and affected people, facts and unknowns, the choice and its reason, responsibility and authority, completion evidence, and what feedback would prompt a change. Keep only the detail needed to understand why the work proceeds as it does.

<a id="questions-en"></a>

#### What remains exploratory

Longer autonomous agent runs and agents that modify their own work environment need further evaluation. The experience here supports attention to context, authority, feedback, and recovery. It does not prove that a particular autonomous organization will work. Those proposals remain in the separate [exploratory guide](thinking/autonomous-delivery.md).

<a id="sources-en"></a>

## Sources and limits

This handbook synthesizes existing material. Conversations support accounts of requests and reflections; process documents describe conventions; commits establish changes. None alone proves adoption, benefit, or sole personal ownership. Incident examples inherited from earlier notes are attributed to those notes, not independently reproduced here.

- [AI collaboration](thinking/ai-collaboration.md) and [platform practice](thinking/platform-engineering.md) cover tasks, verification, shared state, and lifecycles.
- [Team practice](thinking/ai-native-teams.md) covers adoption, responsibility, culture, and quality.
- [Engineering taste](taste.md) and [personal conventions](thinking/working-defaults.md) describe preferences and exceptions, including attribution for the Ponytail decision method.
- [About me](aboutme.md) distinguishes work I led from work I contributed to; it does not establish every effect independently.

Internal code, designs, datasets, raw conversations, assets, and executable workflows are not part of the reusable material here. The shared edition excludes the source workspace's Git history. External sharing requires confirmation of disclosure rights for the specific material.

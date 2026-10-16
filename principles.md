# Principles

[中文](principles.zh.md) · [Home](README.md)

These are the principles I expect to carry across teams, tools, and roles. They
come from my experience, not a claim to have settled engineering. I hold them
with confidence and will revise them when their assumptions no longer hold.
The [handbook](handbook.md) shows how I use them together; specific tools and
organizational proposals belong in [thinking](thinking/README.md).

<a id="outcome"></a>

## 1. Start with the change that matters

Define whose situation should improve and what would establish that improvement.
An implementation is a means to that end. Compare it with improving what exists,
handling the need manually, or doing nothing.

Before committing, identify the uncertainty that could change the decision.
When that uncertainty dominates, the next useful result is evidence, not more
implementation. A bounded experiment can be a complete piece of work.

<a id="evidence"></a>

## 2. Match the evidence to the claim

Keep observations, explanations, decisions, and expectations distinct. Check
that evidence concerns the right target, version, identity, and time.

A passing test supports the behavior it exercised. A deployment establishes a
release state. Neither alone proves that people can use the result or benefit
from it. Report the strongest conclusion the evidence supports, including what
remains unknown. Verification effort should reflect the cost of being wrong.

<a id="completion"></a>

## 3. Follow the work through to an agreed result

Define completion at the level the recipient can rely on. Connect intermediate
steps to that result, make unfinished dependencies visible, and confirm the
handoff. “My command succeeded” is not enough if the requested result is still
unavailable.

Keep scope explicit. Finishing the agreed work does not mean expanding it
indefinitely. A canceled experiment, an evidence-backed decision not to build,
or a clear handoff can be the right conclusion.

<a id="authority"></a>

## 4. Align responsibility, authority, and recovery

The person or agent doing the work needs enough authority to carry its
responsibility, within an understood scope. Access to a tool or document does
not itself grant permission to use, change, or disclose everything it exposes.

Allow independent action within the agreed scope. Escalate when a decision would
change that scope or create consequences its owner has not accepted. Before a
high-impact change, know what can be restored, what needs compensation, and what
cannot be undone. More autonomy requires dependable controls, not more trust in
good intentions.

<a id="whole-cost"></a>

## 5. Optimize the whole cost, not a visible fragment

Count implementation, waiting, integration, operation, recovery, and human
attention. A local speedup can create a larger queue elsewhere. A short patch
can leave a long maintenance burden.

Choose complexity for a present need and explain what it buys. Preserve required
correctness, security, accessibility, and data protection when simplifying.
The simplest adequate solution depends on the actual constraints; it is not
always the fewest lines or the fewest components.

<a id="state"></a>

## 6. Make important state and ownership explicit

For each important fact or decision, know who owns it, where its current state
can be checked, and how conflicting updates are resolved. Different kinds of
facts can have different authoritative sources.

Draft, approved, implemented, and observed are different states. Keep those
distinctions visible where someone acts on them. Prefer references to independent
copies, and reconcile necessary copies deliberately. A name, label, or successful
write is not a substitute for checking the state it claims to represent.

<a id="enablement"></a>

## 7. Make the work usable by someone else

A shared capability includes the path to discover, use, diagnose, and maintain
it. Test that path with an intended user, without silently completing the hard
steps for them. Explain decisions well enough for a successor to adapt them.

Hands-on help is often the fastest way to learn where a system fails. Repeated
rescue is also a signal: improve the path, clarify responsibility, or acknowledge
that ongoing assistance is part of the service. Do not call a capability
self-service while hiding the maintainer's work.

<a id="feedback"></a>

## 8. Let feedback change the method

A practice earns its place by helping the work. Examine failures, false alarms,
waiting, and workarounds. A written rule, a new check, or a retrospective is an
intervention; its existence does not establish its effect.

Choose the response to fit the cause. Improve a tool, clarify a decision, add a
check, teach a skill, or accept a bounded exception. Keep the lesson available
where it will be used, and retire it when its assumptions change. Bring the
reasoning to a new environment, then test the practice there.

## When principles pull in different directions

They are not an algorithm that produces one correct answer. State the conflict,
the local constraints, the cost of error, and the evidence behind the choice.
For example, faster recovery may justify an extra component; a one-time migration
with accepted downtime may not need continuous replication. Explain what would
make you choose differently.

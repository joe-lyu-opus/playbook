# Taste

[中文](taste.zh.md) · [Home](README.md)

These are choices I tend to make when several approaches could work. They are
defaults with reasons, not tests of whether someone is a good engineer. The
[principles](principles.md) explain the more durable commitments;
[working defaults](thinking/working-defaults.md) covers tool-specific conventions.

## Start smaller

I prefer to reuse a working capability before introducing another one. My
usual sequence is: does this need to exist, does the codebase already do it,
does the standard library or platform cover it, can an installed dependency
help, and only then what code do we need? This decision ladder is adapted from
the Ponytail plugin's guidance.

I favor familiar technology and code a colleague can understand without a tour.
I usually extend an existing file unless it is already doing two jobs. An
interface, extra module, or new dependency earns its place by solving a current
problem, not by making the design look complete.

This is a preference for low maintenance cost, not a rule to minimize line
count. I will add structure when it makes ownership or change easier.

## Keep the number of things to remember low

I prefer fewer hand-maintained fields, states, and copies. If a value only
changes with a release, I usually make it a constant instead of building a
configuration surface around it. Existing configuration still takes precedence
over an invented second source.

When I accept a shortcut, I like a short note naming its limit and the condition
for replacing it. I want the next maintainer to see the tradeoff without having
to rediscover it.

## Give me the conclusion, then enough to judge it

Start with what changed or what decision is needed. Follow with the evidence,
tradeoff, and unresolved issue that matter. Use a table or diagram when it
clarifies a relationship; otherwise a short paragraph is usually better.

I prefer plain names to internal nicknames and familiar words to new jargon.
A metric should say what it measures. UI copy should sound natural in its own
language: “Change password” and “Couldn't save. Try again.”

For shared writing, I prefer separate English and Chinese editions with an
obvious language switch. Keep the claims aligned, not the sentence structure.

## Make the diff easy to review

I prefer focused changes that preserve surrounding conventions. Change the
configuration value that needs changing rather than reformatting an entire
file. Use an existing logger or configuration path unless there is a concrete
reason to change it.

A ticket should make the problem and “done when” easy to find. A PR description
should explain the current diff, including a change of direction. I like
imperative English titles. If a repository uses Conventional Commits, the
prefix should describe the effect, not the type of file edited.

For one logical change, I generally prefer a squash merge. When separate
commits carry useful, independent changes, keeping that structure can be better.
Repository policy decides the actual merge method.

## Show the disagreement

In a review, I want the relevant code or behavior and the reason a finding is
valid, partly valid, or mistaken. I prefer a short, specific explanation to
either automatic agreement or a generic dismissal.

For a genuinely subjective choice, show a few viable alternatives with their
tradeoffs. If a specification looks wrong when rendered, show what it produces
and propose an alternative for the owner to consider. Do not quietly substitute
my taste for an agreed design.

## Keep the interface quiet

I like restrained technical diagrams, clear typography, and status indicators
that do not compete for attention. Decorative styling should have a purpose.
These choices still have to meet the product's accessibility requirements and
design system.

For experienced users, I often prefer an open-ended flow over a long wizard.
For newcomers or tasks where order prevents mistakes, explicit guidance can be
the better interface. The preference follows the user, not the other way around.

## Use small instructions and lightweight reflection

I prefer short standing instructions that point to maintained guides.
Preferences, workflow, and facts the agent cannot discover belong there;
tool mechanics belong with the tool.

After meaningful work, I like a short reflection on what would improve the
next attempt. “Nothing to change” is an acceptable result. I do not want a
trivial task to generate a new ritual, rule, and document.

These preferences should make collaboration easier. If following one makes the
current work worse, explain the conflict and propose the better local choice.

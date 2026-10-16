# Working defaults

[中文](working-defaults.zh.md) · [Thinking](README.md)

Status: personal, context-dependent choices. [Taste](../taste.md) explains the
preferences behind them; [principles](../principles.md) owns the durable decision
criteria. These examples are not an installation guide or standing authorization.

## One task per managed worktree

For concurrent repository work, I prefer a separate worktree for each task,
managed through the development environment. I check for existing work before
creating another. The setup keeps file changes and task ownership easier to
trace; it does not isolate external credentials or services.

Use the host team's equivalent when it provides the same useful separation.
Non-code work and tasks that do not share mutable files may need no worktree.
Follow the current team's ticket policy rather than importing my former tracker.

## Branch names and merge units

Without an existing scheme, I like `{owner}-{mmdd}--{short-topic}`, such as
`alex-0418--fix-session-bug`. The owner and creation date help scan a branch list,
although the date is not a reliable measure of abandonment. Tool-generated names
or a repository convention take precedence.

My usual merge unit is one logical change. Squashing suits that unit; meaningful
independent commits can justify a different choice. The preference is described
in [taste](../taste.md), not enforced by this essay.

## A short agent-work brief in the PR

When the team wants to learn from agent work, I add the original request, material
human interventions, and a short lesson for the next attempt. Keep the ordinary
change summary and verification easy to find. Update the brief when the work
changes.

Do not include raw conversations or sensitive prompts. Skip the extra brief if
the team has no use for it or records the same information elsewhere. A useful
lesson may concern tooling or task design, not just better prompting.

## Applying backlog triage

For a backlog I am authorized to maintain, I prefer applying an agreed
classification in one pass. An inspection or recommendation request stays
read-only. Classification is not permission to invent dates, assign other
people, or make commitments.

When several authorized edits express the same uncertain classification, prefer
the one with fewer consequences. A label may suffice without changing project
ownership. The exact field order depends on the tracker and local policy.

## Infrastructure ownership by kind of change

In a Kubernetes setup, one arrangement I have used is Terraform for cloud
resources and Helm for workload releases. It can make infrastructure intent
reviewable while keeping routine application changes on a supported release
path. Change frequency is one consideration, not a complete ownership rule.

Keep an established GitOps or single-tool arrangement when it works. Release
rollback does not reverse every data change or external effect. Emergency manual
changes need the team's authorized path and reconciliation afterward; the
principle is clear ownership, not a universal prohibition on manual tools.

## Names that help inspection

In shared infrastructure, I like names that expose resource kind, instance,
and environment where those distinctions matter. Use the provider's correct
identity type and the team's established naming scheme. A name should help
review; actual permission and environment checks remain necessary.

Avoid a second naming convention just to match this document. Automate a naming
check only when the convention is stable and the check reduces real mistakes.

## Interfaces for different users

A shared service may benefit from both a typed SDK for engineers and a simpler
client for operational users. Build the second interface when there is a real
user path for it, not because every service needs two clients.

Both interfaces need appropriate authorization and visible consequences.
Reducing the skill required to operate something must not silently widen access.
If all callers are engineers, the SDK may be enough.

## Dependency policy and release independence

Choose shared or per-application lockfiles according to release independence and
dependency coupling. Separate resolution can reduce unrelated conflicts while
adding maintenance; shared resolution can simplify coordinated updates while
coupling releases.

Keep a working local convention unless observed friction justifies a change.
Validate the resulting installation in the release-build environment. A generated
file alone is not evidence of compatibility, and old command-level advice needs
checking against current tool behavior.

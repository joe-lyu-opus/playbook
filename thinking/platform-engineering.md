# Platform engineering methods

[中文](platform-engineering.zh.md) · [Thinking](README.md)

Status: conditional practice. The durable criteria live in
[principles](../principles.md); this essay examines their consequences for
platform work, where state, identity, and lifecycle details matter.

These methods concern access, delivery, temporary environments, credentials,
cost, developer experience and data changes. They retain the questions and
failure patterns from practice without reproducing an internal architecture or
incident history. Examples are generalized situations, not operational runbooks.
Check current product documentation before choosing commands or permissions.

## 1. Know who owns state and who can change it

When two systems manage the same resource, identify which owns each field and
how updates are reconciled. Otherwise, a console change can disappear on the
next deployment. One writer is a useful simple design; coordinated controllers
can also work when their responsibilities do not conflict.

Keep intended state reviewable where practical. A manual emergency change needs
an authorized path, an audit record and explicit reconciliation with maintained
configuration. Code is not automatically the truth about what is running.
Read both before concluding that a resource is missing or that a change is safe.

Before tightening or expanding an identity, examine its effective permissions
and every workload that can use it. A repository boundary may not be an access
boundary. An existing broad grant explains current behavior but is not a reason
to preserve excessive privilege. Scope identities and trust relationships to
the work they need to perform, including the untrusted code a build may execute.

For a state-changing command, find out whether it appends, merges or replaces.
Capture the relevant starting state and read back the result. A successful exit
does not establish that unrelated values survived. Adopting an existing resource
into a management tool also needs a plan: adding ownership metadata does not
guarantee a harmless update or zero downtime.

## 2. Make delivery evidence describe the artifact being delivered

A pipeline result must identify the revision and artifact it checked. A rerun
of an old job may still test the old revision. Inspect the actual job inputs
before interpreting a green result as verification of a later fix.

Distinguish missing, skipped, failed and passed checks. When a check is limited
to changed files, record the eligible scope and the scope actually inspected.
Zero eligible files can be a legitimate no-op; zero inspected files when work
was expected is a gap, not success. Preserve failed results even when a step is
intentionally non-blocking.

Use the repository's actual verification configuration. A local test command
can omit files or checks that CI includes. Declare job dependencies instead of
relying on a particular machine's incidental setup. Test the packaged runtime,
not only the source tree: dependency pruning and native build compatibility can
change what starts successfully.

Separate source merge, artifact creation, deployment selection and observed
runtime behavior. Verify only the states the task requires, but do not report
a later state from evidence of an earlier one. Keep unrelated formatting out
of a functional change when it expands review or deployment scope.

## 3. Design temporary environments from creation through removal

Try the first change of a new application, before any production deployment
exists. A preview that depends on production configuration may fail precisely
when it is needed most. Give it suitable isolated configuration and authorized
test data rather than borrowing production credentials.

Define readiness through the user's path, not merely the existence of resources.
A reviewer needs an authorized way to reach the environment; it need not be
public. Test creation, update, expiry, removal and recreation, including duplicate
or delayed events. Make status transitions consistent with the current operation
so a late callback cannot revive a removed environment.

An expiry-based cleanup process can simplify lifecycle management when delayed
deletion is acceptable. Immediate revocation or mandatory retention may need a
different mechanism. Removing source files or a branch does not itself remove
runtime resources, stored data or credentials. Verify the intended cleanup.

When copying configuration, distinguish values from metadata that grants control
over those values. Reusing another object's management metadata can give a
controller authority over a copy it was never meant to manage.

Fallback routing needs a safety decision. Falling back to a shared destination
may violate isolation even if it restores availability. Check allowed targets
and consumers, make fallback visible, and reject the request when no authorized
safe route exists.

## 4. Make credential handling a supported workflow

Prefer scoped automation identities and short-lived access where the environment
supports them. Applications should get required access through a maintained
mechanism. Keep credentials out of source, prompts and shared notes. “Keyless”
does not mean “unrestricted”: inspect what the workload identity can actually do.

Plan rotation from the consumer's point of view. A secret can change in storage
while an application continues using a cached value. Check how consumers reload,
how failures are reported, whether overlap is needed and how old access is
revoked. Do not preserve a hidden credential fallback that defeats revocation.

Give developers a supported authentication and diagnostic path. Expired access,
wrong identity, missing entitlement and an unavailable service are different
failures. A helper should explain which was observed without exposing secrets.

Test and migration data need an approved acquisition path with appropriate
minimization. A read-only production connection is still production access.
Prefer synthetic or approved sanitized data when it satisfies the task.

## 5. Evaluate central services as shared dependencies

A shared outbound service can concentrate authorization, usage attribution and
provider integration. It also becomes a dependency for its callers. Evaluate
availability, latency, maintenance responsibility and failure behavior before
centralizing. A small system may not need that additional component.

Keep distinct requirements separate: identifying the caller, authorizing an
operation, controlling network destinations, handling credentials and recording
usage. An application setting is not proof of network enforcement; successful
authentication is not proof of permission to access a particular resource.

If a control is mandatory, a fallback must not silently bypass it. Define how
work stops or degrades when the controlled path is unavailable. Any exceptional
access needs its own authorization and audit, rather than being disguised as
normal resilience.

Do not make a transport or proxy topology a universal rule. Its trust boundary,
compatibility, visibility into data and operational burden need their own review.

## 6. Make cost and observability useful to a decision

Record enough attribution to connect usage to the responsible workload, while
minimizing private data. Separate measured usage, estimated cost and settled
billing. Their freshness and coverage may differ; explain those differences
instead of presenting a precise-looking number as final.

Check the environment and workload labels on real observations. A metric can
arrive successfully yet be grouped under the wrong service. Make the relevant
source discoverable, and retain enough diagnostic evidence to investigate after
a failed workload has been removed.

Observe the delivery system too. Repeatedly stuck jobs, a missing required check
or an unavailable runner can block many teams at once. Alerts need a meaningful
action and an owner; a count of installed monitors does not establish coverage.

Compare a platform change against a baseline appropriate to its purpose: first
successful use, waiting time, repeated support, repair effort or cost per useful
result. More requests or merged changes can reflect more demand, not improvement.

## 7. Use adoption friction to choose platform work

Record the expected behavior, actual behavior, consequence and proposed repair.
Also record what worked without help. Otherwise a redesign can remove the path
users already depend on while fixing a more visible complaint.

Walk the path from a new consumer's starting point. Check documentation, identity,
dependencies, the first result and recovery from a common failure. A maintainer
silently completing a missing step hides work the next consumer will face.
Scaffolding should preserve existing user work and refuse an unintended overwrite.

Default templates encode assumptions. Check them against a different workload
before calling them general: a background worker may have different readiness,
shutdown and resource needs from a web process. Support legitimate differences
without making every consumer rebuild the platform.

Inspect existing consumers before calling a shared capability missing. Then
choose a supported extension, a separate capability or a consumer correction.
Share logic where its meaning is genuinely shared; test compatibility and avoid
making optional data mandatory without a reason.

## 8. Make operational work explicit and recoverable

Before reading or changing a system, identify the target environment, identity
and resource. Shared local defaults can change between sessions. An empty result
should prompt a target and visibility check before an attempt to “restore” data.

A control plane can supply useful business context, but may be delayed or wrong.
Understand which facts it owns and which it projects from another source.
Resolve discrepancies before using its status as a completion claim.

Provide a bounded, auditable path for one-off maintenance when it is needed.
Its code, inputs, identity, expected effect and recovery should be reviewable.
Running a command beside live traffic is not safe merely because it is convenient.
A particular job runner or deployment location is an implementation choice.

Probe from the environment whose behavior matters. A host, container and sandbox
can have different access paths. Explain what a diagnostic check sees before
generalizing its result. Keep support routing current so a failed path does not
depend on finding one particular engineer.

## 9. Separate a migration's stages and evidence

Define acceptable interruption, source-write behavior, compatibility and recovery
before selecting a migration pattern. A one-time internal operation and a customer
service with strict availability requirements justify different plans.
Parallel running is useful when outputs can be compared safely; it is not a
mandatory step or a license to duplicate external side effects.

Distinguish preparing access, loading data, validating it, switching users and
retiring the old path. A single entry point can coordinate those stages without
hiding their stop conditions. Check content and business invariants as well as
counts. A successful command and matching row totals can still conceal bad data.

Plan schema compatibility and backfill for existing records, including versions
that may coexist during deployment. Test production-relevant constraints in a
safe environment. Rolling back application code may not reverse a data change.
Recovery must be demonstrated at the level of the data risk.

Store stable references where later retrieval matters, rather than treating an
expiring presentation link as a durable identity. Record the transformation or
seed version when it helps distinguish stale data from current code behavior.

## 10. Check governance against its purpose

Route changes by actual risk and responsibility. Paths, labels and owner files
can implement that routing but can drift from reality. Shared configuration can
raise the risk of a seemingly local change. Automation identities need deliberate
permissions; making a bot exempt from all protections is not a setup shortcut.

Coordinate shared dependency policy with consumer compatibility, update tooling
and release cadence. One lockfile or many is a tradeoff between shared resolution,
independent changes and maintenance work, not a universal best practice.

Required configuration should be validated at the boundary where it becomes
necessary. A disabled optional feature can be legitimate; silently disabling a
security control is not. Preserve useful error details without exposing secrets.

After introducing a rule, check whether it catches the intended failure and what
friction it creates. Keep the objective, but change or remove mechanisms that no
longer serve it. A growing policy file is not evidence of a safer platform.

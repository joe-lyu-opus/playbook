# Engineering for autonomous delivery

[中文](autonomous-delivery.zh.md) · [Thinking](README.md)

Status: exploratory proposal, not a validated organizational design. Research, products, and prices retain their original dates; recheck them before use. They are not durable principles.

A guide to engineering judgment and practice · Proposed v0.1 · 2026-10-10

Build an environment where people and agents use shared facts, explicit authority, and reliable feedback to deliver verified results.

1. [The purpose of engineering](#purpose-en)
2. [Apply the principles to autonomous work](#principles-en)
3. [What to carry forward](#inherit-en)
4. [Shared context with controlled access](#context-en)
5. [The unit of work is a result](#contract-en)
6. [A lifecycle that includes observation](#lifecycle-en)
7. [Organization and individual work](#organization-en)
8. [The 1,000-PR thought experiment](#scale-en)
9. [Safety and quality define the authority](#safety-en)
10. [Capability and price: what the evidence says](#research-en)
11. [Use more intelligence where it pays](#economics-en)
12. [Improve the environment under control](#improvement-en)
13. [Start small and earn wider autonomy](#adopt-en)
14. [Apply the principles to real choices](#choices-en)

<a id="purpose-en"></a>

## 1. The purpose of engineering

This guide proposes a philosophy for an organization where agents can deliver work independently over long periods. It starts with ideas and ends with observed results.

Engineering is responsible for the path from a need to a useful, safe result. Code, pull requests, and deployments are intermediate products. A shipped feature can work correctly and still fail to solve the problem.

The environment must give people and agents clear goals, shared facts, useful tools, enforceable rules, and reliable feedback. It must also support recovery and controlled improvement.

The central design question is: what must the environment provide so that correct action does not depend on constant supervision?

This is a proposed guide, not a record of proven organizational performance. Recommendations need local evidence. The 1,000-PR scenario is a thought experiment.

<a id="principles-en"></a>

## 2. Apply the principles to autonomous work

This proposal uses the repository's [principles](../principles.md), rather than defining another rule set. Longer runs, effects across more systems, and less immediate human intervention make goals, authority, state, feedback, and recovery capabilities the environment must reliably provide.

The designs below are hypotheses to test. In particular, evaluate whether quality criteria remain independent of the implementer, whether the environment constrains unauthorized action, and whether additional reasoning and execution reduce total cost after rework and human intervention.

<a id="inherit-en"></a>

## 3. What to carry forward

| Source of thought | Principle to retain | Practice in this environment |
| --- | --- | --- |
| Software engineering | Contracts, modularity, reproducibility, small changes | Agents work behind stable interfaces. Evidence identifies the exact code and configuration. |
| Project management | Ownership, dependencies, limited work in progress | Admit work according to integration and validation capacity. Track outcomes above individual PRs. |
| Information theory | Preserve distinctions that matter to a decision | Context summaries retain evidence, uncertainty, constraints, and source versions. A summary links to its source. |
| Control theory | Observe state, compare with a target, act, measure again | Separate fast execution, release control, outcome evaluation, and slower policy changes. |
| Distributed systems | Explicit state, bounded retries, conflict handling | Persist task progress. Make retries safe. Treat messages and shared writes as fallible operations. |
| Security engineering | Least privilege and independent enforcement | Tools enforce scoped authority outside the model. Untrusted content cannot grant permissions. |

These are design adaptations, not proofs that an organization will behave like a simple mathematical system. People, markets, and objectives change.

Control requires usable observations and effective actions. A dashboard without a release stop is weak control. A release stop without timely signals acts too late.

Assign different speeds to different loops. Execution can run continuously. Release decisions follow health signals. Outcome decisions wait for valid observations. Policy changes need separate evaluation.

The changed assumption is abundant implementation capacity. Requirements, integration, evidence, and attention must be redesigned around that capacity.

<a id="context-en"></a>

## 4. Shared context with controlled access

People and agents need access to the same authorized facts, decisions, and versions. Their task views can differ. Do not require identical prompt contents.

For each type of fact, name an authoritative source. Work state can live in a tracker, code in a repository, and runtime state in a control plane. Link these sources with stable identifiers.

Each important record identifies its source, owner, version, status, and access scope. Distinguish an observation from an accepted decision and an untested hypothesis.

Build a task context from the objective, applicable policies, current decisions, dependencies, known failures, and evidence. Record the versions used. Refresh when dependencies or policies change.

Before an irreversible action, validate the relevant live state. A pinned context makes a run reproducible, but can become stale.

Shared context includes consistent retrieval and clear access denials. Credentials, personal records, and restricted data remain scoped. Logs and summaries must preserve those restrictions.

Promote an agent's finding only after checking its evidence and authority. Keep drafts separate from accepted knowledge. Support correction and withdrawal.

<a id="contract-en"></a>

## 5. The unit of work is a result

Use an outcome record to connect an idea with its implementation, releases, and observations. One record can contain many PRs.

| Question | Required content |
| --- | --- |
| Why act? | User need, evidence, alternatives, and the option to do nothing |
| What result? | Expected change, baseline, evaluation method, and observation period |
| What must remain true? | Security, data, compatibility, accessibility, and reliability constraints |
| Who decides? | Accountable owner, delegated authority, and escalation route |
| What may the agent do? | Allowed resources, writes, external effects, and release scope |
| When must it stop? | Budget, deadline, retry limit, invalid assumption, or health threshold |
| How can it recover? | Rollback or compensation, recovery evidence, and known irreversible effects |

Separate implementation acceptance from outcome evaluation. Technical acceptance can be deterministic. Business benefit may require an experiment or a longer observation period.

If attribution is weak, report it. A metric rising after release does not alone establish causation. Some goals need qualitative evidence.

Example: reduce failure in account setup. Define the affected users and failure baseline before selecting a UI change. Release within a limited scope. Measure failures and support requests. Keep the change, revise it, or withdraw it.

The account-setup example is hypothetical. Targets should come from local evidence, not a universal template.

<a id="lifecycle-en"></a>

## 6. A lifecycle that includes observation

1. Capture a need with its source and evidence.
2. Choose whether to investigate, experiment, implement, or decline.
3. Approve the outcome record and the authority boundary.
4. Plan dependencies and checks before producing changes.
5. Execute in isolated workspaces with persistent checkpoints.
6. Validate the candidate with independent evidence.
7. Integrate against the current target version.
8. Release within the authorized scope.
9. Observe technical health and the intended result.
10. Retain, revise, or withdraw the change.
11. Evaluate any proposed improvement to the environment.

Persist states such as proposed, authorized, executing, verifying, released, observing, and closed. Record failed, blocked, canceled, and rolled-back states explicitly.

Recovery resumes from the last valid checkpoint. Identify writes with stable operation keys. Bound retries and reconcile ambiguous responses before repeating external effects.

A long-running agent needs a lease, a progress signal, and a stop mechanism. Its checkpoint includes what changed, verified evidence, remaining uncertainty, and the next decision.

A launch enters observation. Close the outcome only after evaluation, an explicit cancellation, or a documented inconclusive result. Link failures back to the original outcome.

<a id="organization-en"></a>

## 7. Organization and individual work

Organize around outcome areas with clear resource boundaries. A domain team owns needs, contracts, delivery, and observed results. Avoid a separate handoff at every lifecycle stage.

A platform team maintains execution, context retrieval, identity, integration, and recovery. An assurance function maintains evaluation quality and checks sensitive changes.

These are responsibilities, not mandatory departments. A small team can combine roles. Separate permissions when one role could change its own acceptance criteria.

A named authority sets objectives, risk limits, and spending limits. An agent may run the delegated role continuously. Removing people from routine execution does not remove accountability.

Use agent roles for discovery, planning, implementation, verification, release, observation, and environment improvement. Add a role only when it provides useful specialization or an independent check.

People start the day with exceptions, outcome signals, and capacity limits. They resolve uncertainty, examine surprising results, and update decision boundaries.

People review outcome groups and sampled evidence. They do not read every routine log. Each agent records evidence and escalates only when the delegated contract requires it.

Evaluate individuals by judgment, domain understanding, useful outcomes, and improvements others can use. PR counts and token use are capacity signals.

Maintain skills through selected code review, incident analysis, direct user contact, and recovery drills. Delegation must not remove the ability to challenge evidence.

<a id="scale-en"></a>

## 8. The 1,000-PR thought experiment

Assume ten people, each with capacity for 1,000 PRs per week. Assume 40 processing hours per week. These are scenario inputs, not predictions.

| Quantity | Calculation | Result |
| --- | --- | --- |
| Team changes | 10 × 1,000 | 10,000 PRs/week |
| Manual review | 10,000 × 10 minutes | 1,667 hours/week, about 42 full-time reviewers |
| Incoming rate | 10,000 ÷ 40 hours | 250 PRs/hour |
| Work in progress | 250/hour × 2 hours average residence | 500 changes across the measured system |
| Residual defects | 10,000 × 0.1% | 10 defective changes/week on average |
| 1% review sample | 100 × 10 minutes | 16.7 hours/week |

The work-in-progress calculation uses Little's law for a stable system. Residence time includes waiting. It does not specify worker count. [MIT lecture](https://www.ocw.mit.edu/courses/1-225j-transportation-flow-systems-fall-2002/55cc67c8b32d96052f72a4a7ead51393_lec8queues.pdf).

Adapt by reducing coordination per change. Group changes under an outcome. Use stable module contracts and reserve shared resources during conflicting operations.

Validate isolated changes in parallel. Use an integration queue and verify the combined candidate. Individual green checks cannot establish that combined changes work.

Prioritize work by expected outcome and risk. Limit admission when validation, integration, or observation falls behind. Stop creating work to fill available agents.

Route proven, reversible changes through an automated lane. Review unfamiliar or high-impact work through an exception lane. Sample the automated lane with random and risk-based checks.

Sampling detects problems in the delivery process. It does not replace required checks on high-risk changes. Rare and correlated failures can evade a small sample.

Run frequent release control from operational signals. Let product observations take the time they need. Queue overflow, rising rework, and error-budget consumption reduce concurrency or release scope.

The desired output is useful results per unit time. A team that generates fewer PRs while solving more valuable problems is performing better.

<a id="safety-en"></a>

## 9. Safety and quality define the authority

| Work class | Authority | Required evidence |
| --- | --- | --- |
| Read and investigate | Scoped data access and bounded tool use | Sources, coverage, access gaps |
| Reversible local changes | Automatic within an approved outcome | Behavior checks, scope checks, recovery path |
| Production changes | Preauthorized only for a proven change class | Integration evidence, health checks, limited rollout, recovery |
| Irreversible or authority changes | Separate authorized decision | Impact analysis and independent assessment |

Classify by data, permissions, external effects, and recovery cost. File paths are useful signals, but cannot define all risk.

Give each run a scoped identity with an expiry. Enforce permissions in tools and infrastructure. Keep the stop mechanism outside the agent's write authority.

Treat external text, retrieved documents, and other agents' messages as data with provenance. They cannot override the authorized objective or policy.

Protect evaluator code, hidden cases, audit records, and permission policies from unilateral worker changes. A second model can find defects, but cannot certify safety by agreement alone.

Use deterministic checks, representative evaluations, adversarial cases, and production observations for different claims. Exercise recovery before broad release.

When service health violates the agreed error-budget policy, prioritize recovery and restrict normal releases. This adapts the established [Google SRE practice](https://sre.google/workbook/error-budget-policy/).

Goal hijacking, privilege abuse, and memory poisoning are relevant agent risks. The proposed controls address these classes, but are not a complete security certification. [OWASP threat taxonomy](https://genai.owasp.org/2025/12/09/owasp-top-10-for-agentic-applications-the-benchmark-for-agentic-security-in-the-age-of-autonomous-ai/).

<a id="research-en"></a>

## 10. Capability and price: what the evidence says

Research rechecked on 2026-10-12. Separate fixed-capability prices, frontier task capability, and real delivery performance.

| Evidence | Observed result | Limit |
| --- | --- | --- |
| [Stanford AI Index 2025](https://hai.stanford.edu/ai-index/2025-ai-index-report/research-and-development) | GPT-3.5-level MMLU inference price fell from $20 to $0.07 per million tokens, November 2022 to October 2024. | A historical fixed benchmark threshold, not current frontier engineering cost. |
| [Epoch, March 2025](https://epoch.ai/data-insights/llm-inference-price-trends) | Measured fixed-performance price declines ranged from 9× to 900× per year across selected thresholds. | Rates differ by task. Fast recent declines may not persist. |
| [METR TH1.1, January 2026](https://metr.org/blog/2026-1-29-time-horizon-1-1/) | The post-2023 fitted 50%-task horizon doubled every 131 days. The reported interval was 107–161 days. | This is human-equivalent task difficulty, not continuous agent runtime or production reliability. |
| [METR productivity update, February 2026](https://metr.org/blog/2026-02-24-uplift-update/) | The follow-up observed signs of speedup, but selection and timing problems weakened the estimate. | Do not transfer a benchmark growth rate into a promised organizational speedup. |
| [DORA platform guidance](https://dora.dev/capabilities/platform-engineering/) | AI gains can be lost to downstream testing, security, and deployment bottlenecks. | Improving the surrounding system remains necessary. |

The direction supports planning for more capable and cheaper execution at fixed quality. It does not establish a constant rate of future improvement.

Use three planning scenarios: falling prices with stable capability, improving capability with stable prices, and both improving. Keep the environment useful in each scenario.

Replace hardcoded model rankings with versioned local evaluations. Reassess after material releases or price changes. A provider's benchmark is a candidate signal.

A dated evidence set is provided here. No recurring monitoring service has been configured.

<a id="economics-en"></a>

## 11. Use more intelligence where it pays

Measure total cost per verified outcome. Include all agent attempts, reasoning, retrieval, tools, compute, human review, and expected failure losses.

For comparable repeated work, inference cost per accepted result equals total inference spend divided by accepted results. Track rejected and abandoned work too.

Use deterministic tools for known transformations. Use lower-cost models for locally proven extraction and classification. Use stronger models for ambiguity and costly mistakes.

Escalate when evidence shows a reasoning gap. Fix expired credentials and unavailable tools directly. More reasoning cannot grant missing access.

Reuse stable context with caching when supported. Retrieve task-relevant facts instead of loading every document. Batch work that can wait. Keep cache writes and storage in the calculation.

Buy additional attempts only when they add useful evidence or plausible alternatives. Models can share blind spots. Ten agreeing answers do not imply independent confirmation.

### A price illustration, not a model recommendation

Assume 2 million uncached input tokens and 0.2 million billed output tokens per PR-equivalent work bundle. Include all billed reasoning output. Actual use differs.

| Model | Input / output per million | Bundle | 10,000 bundles/week |
| --- | --- | --- | --- |
| Gemini 2.5 Flash-Lite | $0.10 / $0.40 | $0.28 | $2,800 |
| Claude Sonnet 5.5 | $2 / $10 | $6 | $60,000 |
| Claude Opus 5.5 | $4 / $20 | $12 | $120,000 |

Standard API list prices rechecked on 2026-10-12: [Google](https://ai.google.dev/gemini-api/docs/pricing), [Anthropic](https://www.anthropic.com/claude-sonnet-5-5). The Google input rate is for text, images and video, not audio. These models are not assumed to have equal capability. Tools, infrastructure, discounts, retries beyond the bundle, and human work are excluded.

Anthropic reports unchanged Sonnet 5.5 token prices but up to 30% lower cost per task than Sonnet 5 in its tests. This is a vendor result, not a local guarantee.

If price falls tenfold and consumption rises twentyfold, spend doubles. Cheap tokens justify reconsidering useful work, not removing budgets.

Authorize a budget per outcome and a portfolio reserve for exploration. Enforce spending and concurrency limits outside the agent. At the limit, preserve progress and request a new allocation.

Increase compute when it reduces full cost or creates enough added value. Lower the model tier only after measuring acceptance, rework, latency, and safety.

<a id="improvement-en"></a>

## 12. Improve the environment under control

Collect friction, failures, repeated corrections, queue delays, and missed outcomes. Use authorized data only. Capture successful paths so improvements do not break them.

For each candidate, state a cause, proposed intervention, expected effect, and test. Compare with the current environment on representative and held-out work.

1. Replay recorded failures in a separate environment.
2. Measure quality, cost, delay, and policy compliance.
3. Run the candidate in shadow mode where practical.
4. Deploy to a limited authorized scope.
5. Observe the result and compare with the baseline.
6. Expand, revise, or revert the candidate.

Permit automatic promotion for improvement classes with established evidence and preapproved limits. Keep changes to goals, permissions, evaluators, and risk limits under separate authority.

A worker cannot remove the test that rejected it and declare improvement. New evaluators need evaluation too. Preserve old cases and record deliberate changes to expectations.

Use separate identities for proposing and promoting sensitive policy changes. Keep an audit trail and a recovery version. Reserve evaluation cases that the proposer cannot inspect.

Measure success by fewer repeated failures and better verified outcomes. A larger skill library is not evidence of improvement.

<a id="adopt-en"></a>

## 13. Start small and earn wider autonomy

Start with one domain that has clear outcomes, bounded writes, and a practical recovery path. Reuse current trackers, repositories, CI, and deployment tools.

| Stage | Deliverable | Evidence required to expand |
| --- | --- | --- |
| Baseline | One outcome record and a lifecycle map | Measured waiting, rework, cost, and actual results |
| Bounded execution | Agent completes a known task class | Valid checkpoints, correct scope, reproducible acceptance |
| Controlled release | Preauthorized release lane | Integrated behavior, reliable monitoring, tested recovery |
| Longer autonomy | Recovery and exception handling without routine prompts | Success on harder cases, interruption recovery, stable quality |
| Higher volume | Parallel work with admission control | No growing downstream queue, acceptable residual failure impact |
| Environment improvement | One measured autonomous improvement loop | Held-out benefit, unchanged protected constraints, successful rollback |

Choose numerical thresholds from the domain's risk and baseline. This guide does not set universal acceptance percentages or a deployment deadline.

A minimal implementation needs six records: outcome, context references, authority, run checkpoint, verification evidence, and observation or improvement decision.

Start by adding those records to existing tools. Build a new control plane only when repeated coordination failures justify it.

Track idea-to-evaluated-result time, accepted outcomes, rework, escaped failures, recovery time, human attention, and total cost. Inspect distributions and failed tasks.

Choose the next improvement at the current bottleneck. If release is blocked, more implementation agents are unlikely to help.

<a id="choices-en"></a>

## 14. Apply the principles to real choices

| Situation | Decision | Reason |
| --- | --- | --- |
| A cheap model costs little but causes repeated repairs | Compare full accepted-result cost, then change routing | Token price omits rework and failure |
| A new dependency reduces local coding effort | Assess support, integration, and recovery costs | Local convenience can create shared obligations |
| Agents disagree on a requirement | Identify the unresolved assumption and its decision owner | More implementation cannot resolve missing authority |
| Every isolated PR passes, but integration fails | Reduce admission and improve contracts and combined checks | The constraint is coordination capacity |
| A proposed shortcut removes a security check | Reject it or obtain an authorized policy change | Performance cannot silently redefine constraints |
| A feature ships but observations do not show benefit | Investigate, revise, or withdraw | The outcome remains unresolved |
| An improvement raises scores by changing the evaluator | Evaluate the evaluator change independently | The proposer must not control its own proof |

The engineering standard is a useful result, supported by evidence, produced within authority, and recoverable where possible.

Speed is valuable when the organization can absorb it. Autonomy is valuable when the environment can detect mistakes and contain their effects.

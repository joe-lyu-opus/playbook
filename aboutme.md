# About me

[中文](aboutme.zh.md) · [Home](README.md)

I'm Joe. Since 2019, my work has moved from data engineering to enterprise data
platforms, then to AI application platforms and agent infrastructure. I've built
audience-data systems, streaming pipelines, query services, and data gateways,
led an internal application platform from its beginnings into use, and worked
on security remediation and product-system redesigns.

I've built for data developers, application engineers, and colleagues using AI
to create applications without an engineering background. I care about making
the underlying capabilities usable, diagnosable, and maintainable by those people.

## Work I've done

### Data engineering: audience data and real-time pipelines

I started in a mobility business, working on batch and streaming warehouses,
business metrics, and data governance. I led a redesign of a user-profile system
that let operations teams select audiences using combinations of attributes.
The work covered data synchronization, search, and caching, along with attribute
lifecycle management, quality monitoring, and access control.

I also built a streaming data pipeline with Kafka, Flink, and ClickHouse,
connecting event processing to business monitoring and alerts. Pre-aggregation
and materialized views helped improve query and storage efficiency. That work
connected producing data with serving it to people who needed to act on it.

### Enterprise platforms: discovery, APIs, and federated queries

I went on to lead core architecture and delivery work for enterprise cloud data
platforms, supporting both public-cloud and private deployments. I also led data
governance modules covering standards, modeling, metrics, quality, and lineage.
As a project lead, I worked on several core systems:

- Metadata collection and asset search: distributed collection and task
  scheduling across heterogeneous sources, so customers could inventory and
  find their data assets.
- A data-service gateway: exposing platform data through APIs, separating
  configuration management from request handling, and providing authentication,
  traffic controls, monitoring, and horizontal scaling of request processing.
- A federated query service: turning open-source Trino into a deliverable
  enterprise service, integrating platform permissions, extending function
  support, and handling dynamic source-configuration migration and failover.

The job included delivering these systems into customer environments, where
deployment constraints and integration with existing systems shaped the design.

### An internal platform for application delivery

At an AI startup, I led the creation of an internal application platform and
brought it into use. It served engineers as well as colleagues in product,
design, and marketing. The platform connected authentication, application
resource provisioning, builds, deployment, analytics, and auditing into a
self-service delivery path.

My work covered the underlying runtime environment, platform interfaces, and
delivery process. Application authors could use declarative configuration to
request platform resources and concentrate on the application. Colleagues
outside engineering also delivered applications through it. I helped define
the additional quality and access requirements for taking internal experiments
to external users.

### AI engineering: development environments and agent runtimes

I designed and implemented shared agent instructions and a way to distribute
reusable skills, with automated contract checks and clear limits on what
contributors could change in a shared codebase. I also organized working
knowledge into layers of context and memory for agents to use.

I led work on an agent runtime and control plane for isolated execution,
registration, task scheduling, and session-state persistence and recovery. I
also contributed to existing shared outbound-access and preview-environment
capabilities. These have distinct responsibilities: the runtime manages
execution, shared access handles external calls, and applications own their
task logic.

### Service governance and security remediation

I designed and helped roll out service metadata and lifecycle standards. The
work included a service catalog, infrastructure-as-code resource provisioning,
and shared asynchronous communication, including migration of existing
production workflows.

As a core engineer on security and compliance remediation, I worked on audit
logging, access reviews, credential management, service identities, environment
isolation, and sensitive-data handling during synchronization. This required
turning requirements into changes to running systems and everyday operations,
working with the people accountable for the remediation.

### Product reliability: scheduled publishing

I led a redesign of a multi-platform scheduled-publishing system for creators.
To address tasks disrupted by service releases or failures, I separated the
API from background workflow execution, moved scheduling to durable execution,
and added tracing and error classification.

I also worked on social-account connection flows. The changes improved the
reliability of retaining and executing scheduled tasks and made publishing
failures easier to locate and explain, alongside improvements to account
connection reliability.

## What I bring to a team

I've worked on underlying data processing, shared developer capabilities, and
systems whose failures directly affect users. When discussing a platform, I
consider the user's task, how the service runs, and the team's ability
to keep delivering and maintaining it.

Building a platform from scratch, making open-source capabilities deliverable,
and changing systems already carrying operational demands are familiar work for
me. I'm also refining how I collaborate: after helping finish one migration,
I want to know whether the consuming team can handle the next one independently.
This repository records the principles and preferences I've developed through
that work.

## Working with me

- Start with the problem, the constraints, and the decision you need. A proposed
  solution is welcome; so is evidence that we should not build it.
- Make progress concrete. Tell me what now works, what supports that claim, and
  what remains unresolved. Raise a material obstacle while there is still time
  to change course.
- Challenge my choices with examples and tradeoffs. My preferences are not a
  substitute for your team's context, and disagreement need not be a personal
  conflict.
- Within an agreed scope, I prefer initiative to repeated permission checks.
  Bring me the decisions that change the scope, risk, or commitment.
- Keep communication concise and natural. I prefer Chinese in direct
  conversation, English for code and review artifacts, and native-quality
  English and Chinese editions for shared write-ups.

## How to read this repository

[Principles](principles.md) explains what I expect to hold across environments.
[Taste](taste.md) explains choices I tend to make among reasonable alternatives.
The [handbook](handbook.md) puts them to work in cases. [Thinking](thinking/README.md)
contains more conditional practices and ideas I am still developing.

These notes are a starting point for collaboration. In a new team, I want to
understand what its current practices protect before proposing changes.

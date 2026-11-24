# Platform Success Metrics — Case Study

*Understanding developer needs beyond the number of features delivered*

## Context and my role

I worked as a Technical Business Analyst in an internal platform team supporting stream-aligned development teams. My focus was not only on how predictably we delivered, but also on whether the services we provided were discoverable, useful and reducing avoidable reliance on the platform team.

This case study separates **work I carried out** from **ideas I considered but did not implement**.

## 1. Support tickets: finding recurring friction

### What I measured

Support tickets already had categories. I reviewed them regularly, ensured tickets were categorised correctly and created an **eazyBI table of ticket counts by category, sprint and PI** to look for recurring patterns.

### What I observed

Several requests pointed to a gap between what the platform enabled and what users understood about their responsibilities:

- Some stream-aligned teams were unaware they should create or use the relevant pipeline to obtain production data, rather than asking the platform team to arrange access as before.
- Teams frequently asked the platform team for help with their own pipelines, despite pipeline operation belonging to the stream-aligned teams under the shared responsibility model.
- Questions about requesting databases, requesting AWS services and querying databases recurred.

### What I changed

- I updated FAQ answers for recurring questions and shared the relevant links, including the shared responsibility model, in Slack.
- I reorganised Confluence by archiving outdated pages, separating internal technical guidance from user-facing documentation and putting key information first.
- I also co-presented a project-wide technical huddle covering where to find information, when to contact the platform team and what to check before raising a ticket.

### What I could establish

I observed changes in support behaviour, but I did not quantify a reduction or establish that the documentation changes caused it.

## 2. Temporary production DB access: demonstrating self-service demand

### What I tracked

I frequently reviewed an existing dashboard of production DB access requests, usage frequency and access time. A previous PO had created the underlying Python script using the GitHub API; **I reviewed and communicated the metrics, rather than developing the script**.

During one go-live period, the dashboard recorded **around 400 access requests in a month**. I shared that chart with the team to make the value of self-service visible. Previously, stream-aligned teams had relied on platform-team support to arrange this access.

The number made the scale of demand tangible, but **400 requests does not mean 400 support tickets were avoided**. We did not establish a one-to-one correspondence or calculate validated time savings.

## 3. Developer feedback: checking the experience behind the numbers

After the temporary production DB access feature was fully released, I identified frequent users and interviewed them about ease of use, documentation, improvements and unresolved issues. I also invited wider feedback in the project Slack channel.

Feedback was generally positive: users found the capability straightforward and the documentation helpful. One PO, however, wanted to use it for analytical JOIN queries across databases—outside its intended purpose of troubleshooting production issues. We considered the opportunity but did not pursue it once we found limited demand beyond that user.

I shared the findings with the PO and team. This reinforced an important product lesson for me: **a real user need is worth understanding, but not every request justifies expanding a feature's scope**. These interviews were qualitative research, not a formal satisfaction score or representative survey.

## 4. Reliability and onboarding: other signs of platform success

The platform team completed a cluster migration with **no observed downtime**. To reduce risk, the team tested the migration approach in advance, moved non-production environments before production, interviewed teams about application dependencies, used monitoring dashboards and automated functionality checks, and involved QAs, tech leads, architects and other relevant colleagues.

This was a **team outcome**, not a metric programme I personally established. I include it because platform value also depends on maintaining reliable services during change.

I also adapted onboarding information for POs in stream-aligned teams, explaining what the platform team owned, how teams would interact with us and where to find help. I received positive informal feedback, but did not measure onboarding effectiveness.

## 5. Measurement ideas I considered but did not implement

While working with the team, I thought about how to move beyond reporting individual metrics toward evaluating whether changes were genuinely helping developers.

### Support tickets after feature releases

I considered comparing release dates with the number and categories of subsequent support tickets. This could highlight friction or unexpected issues after a launch. But zero tickets would not prove a successful release: users might be unaware of a feature, work around problems or simply not report them. Usage and direct feedback would be needed for context.

### Whether FAQs and technical huddles reduced recurring questions

I considered recording when FAQ updates and huddles took place, then comparing the number of tickets in the specific question categories before and after those interventions. This might help assess whether documentation and knowledge sharing made users more independent. I did not complete this analysis, and any interpretation would need to account for changes in the number of active teams, usage and other simultaneous improvements.

### Broader platform measures: DORA, developer experience and velocity

I was interested in using a broader perspective on platform success, including:

- **DORA metrics, viewed through a platform lens**: how reliably and quickly we released platform changes and recovered from failures, while recognising that application-team delivery outcomes were influenced by more than the platform alone.
- **Developer satisfaction and experience**: direct feedback on whether services, documentation and support were helping teams work effectively.
- **Velocity and friction**: the elapsed time to provision services, change configurations or complete common tasks, including time developers spent waiting for platform support.

The article **[Platform Team Metrics That Actually Matter: Beyond DORA](https://platformengineering.com/features/platform-team-metrics-that-actually-matter-beyond-dora/)** provides a useful framework for these areas. I reference it as supporting reading, **not as evidence that we implemented the measures it describes.**

### Support request lead time — a data-quality limitation I encountered

One metric I wanted to understand better was **support request lead time**: how long requests took from being raised to being resolved. However, ticket statuses were not consistently updated by support pairs, so the resulting timing data could not be relied upon as a complete picture of the process.

I reminded colleagues to update tickets and conducted a **support-process huddle** with identified improvements. This showed me that introducing a metric is not just about choosing a formula: we also need shared definitions and reliable practices for capturing the events being measured. I did not establish a validated lead-time baseline or claim a measured improvement.

## Reflection

My most valuable contribution was connecting signals to action: using support patterns to improve documentation and responsibility clarity, using feature usage to communicate the value of self-service, and talking with developers to understand what numerical charts could not explain.

I also became more careful about interpreting metrics. High usage is not necessarily high satisfaction; fewer tickets do not necessarily mean fewer problems; and elapsed-time metrics are only meaningful if workflow status data is maintained. These are lessons I would take into a Technical BA or Product Owner role when discussing platform outcomes with a team.

For a separate account of delivery predictability, see [Flow Metrics & Forecasting](../03-flow-metrics-forecasting/README.md). For earlier discovery research, see the [Vault → AWS Secrets Manager migration](../02-vault-to-aws-sm-migration/README.md).

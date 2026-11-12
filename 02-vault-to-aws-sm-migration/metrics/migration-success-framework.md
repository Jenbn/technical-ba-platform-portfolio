# Migration Success Framework — Vault to AWS Secrets Manager

## Purpose & Context

This document proposes a framework for evaluating the success of a migration from HashiCorp Vault to AWS Secrets Manager, considering **adoption, workflow performance, support demand, developer experience, and legacy retirement**.

While working in the Platform Team, I participated in discussions with our Product Owner, Tech Lead and a Platform Owner about adoption, onboarding & Vault retirement metrics. The remaining metrics and evaluation practices are retrospective proposals based on my experience in the team.

I was no longer part of the project when adoption began and cannot confirm which metrics were ultimately implemented.

The framework is organised into three areas:

- [Success Metrics](#proposed-success-metrics) — What to measure and why.
- [Migration Practices & Considerations](#migration-practices--considerations) — How onboarding, automation and legacy retirement were intended to work.
- [Feedback & Continuous Improvement](#feedback--continuous-improvement) — How to collect feedback and use findings to improve the platform.

---

## Proposed Success Metrics

### Adoption & Migration Progress

**Objective:** Track the adoption of AWS Secrets Manager and progress towards completing the migration.

| Metric | Measurement | Frequency | Lifecycle |
| --- | --- | --- | --- |
| Teams onboarded | Number of teams meeting the onboarding completion criteria | Per sprint / PI | During migration |
| Migration progress | Fully migrated teams / total in-scope teams × 100 | Per sprint / PI | During migration |
| Workflow usage | Number of executions of create/delete-secret workflows | Monthly | Ongoing |
| Workflow adoption | Number of distinct teams using each workflow | Monthly | Ongoing |

**Considerations:**

- *Onboarded* and *fully migrated* represent different milestones. See [Onboarding & Migration Completion Criteria](#onboarding--migration-completion-criteria).
- Onboarding and migration progress are temporary metrics that can be retired from regular reporting after migration completion and verification.
- Workflow usage and adoption remain relevant after migration, although secret creation and deletion may naturally become less frequent.

### Workflow Performance

**Objective:** Assess the reliability and efficiency of the predefined create/delete-secret workflows.

| Metric | Measurement | Frequency |
| --- | --- | --- |
| Workflow executions | Total executions per workflow | Monthly |
| Workflow errors | Number of failed executions per workflow | Monthly |
| Workflow failure rate | Failed executions / total executions × 100 | Monthly |
| Execution time | Median and 95th-percentile time from start to completion | Monthly |

Where possible, errors should be categorised (e.g. permissions, invalid input or technical failures) to identify recurring problems.

The workflows and responsibilities are described in [Automation-First Secret Management](#automation-first-secret-management).

### Support & Documentation

**Objective:** Identify recurring problems, documentation gaps, and opportunities to improve self-service.

| Metric | Measurement | Frequency |
| --- | --- | --- |
| Support tickets | Number of AWS Secrets Manager-related tickets, grouped by category | Per sprint / monthly |
| Bot-handled questions | Number of distinct questions handled by the support bot without ticket escalation | Monthly |
| Recurring issues | Most frequently reported problems or questions | Monthly |

**Support ticket categories:**

- **Documentation:** Missing, outdated or unclear information.
- **Open questions:** Requests requiring clarification or additional guidance.
- **Errors:** Technical failures or unexpected behaviour.

The support channel was primarily handled by a bot. Questions answered through the bot could reveal recurring topics and documentation gaps.

Questions escalated to a support ticket should be counted under support tickets instead of bot-handled questions to avoid double-counting.

A bot-generated response should not automatically be treated as a successfully resolved question unless supporting evidence is available.

**Measurement periods:**

- **During migration:** While teams are actively adopting AWS Secrets Manager.
- **Post-migration:** After the migration is complete and teams are using the new solution.

Support trends should be interpreted alongside the number of onboarded or active teams.

### Developer Experience

**Objective:** Understand user satisfaction, identify remaining pain points, and evaluate the experience of stream-aligned teams.

| Metric | Measurement | Frequency |
| --- | --- | --- |
| User satisfaction | Satisfaction rating from the survey (1–5) | During and after migration |
| Discoverability | User rating of how easy it is to locate secrets | During and after migration |
| Onboarding experience | User rating of the migration and onboarding process | During and after migration |
| Documentation usefulness | User rating of the available documentation | During and after migration |
| Recurring pain points | Themes identified through open-text feedback | During and after migration |

The survey methodology and proposed questions are described in [Developer Experience Survey](#developer-experience-survey).

These metrics should help assess whether the new solution addresses the needs identified during the original [user research](../discovery/research-findings.md).

### Vault Retirement Readiness

**Objective:** Assess whether Vault can be safely retired without disrupting stream-aligned teams.

| Metric | Measurement | Frequency |
| --- | --- | --- |
| Remaining Vault secrets | Number of secrets still present in Vault | Per sprint |
| Recently accessed secrets | Secrets with observed retrieval activity within the defined monitoring period | Per sprint |
| Teams with unresolved dependencies | Number of teams reporting active Vault dependencies | Per sprint |
| Migration exceptions | Number of unresolved blockers or approved exceptions | Per sprint |
| Retirement readiness | Completion of agreed technical and operational shutdown criteria | Before retirement |

A reduction in secret inventory or observed activity does not independently prove that Vault is no longer required.

The retirement approach and validation considerations are detailed in [Legacy Retirement Approach](#legacy-retirement-approach).

---

## Migration Practices & Considerations

### Onboarding & Migration Completion Criteria

Two milestones should be distinguished when evaluating migration progress.

#### Onboarded

A team is considered onboarded when:

- All current team members have the appropriate AWS Secrets Manager access for their roles.
- Authorised human users can read and manage secret values through the AWS UI.
- CI/CD workflows can create and delete secret structures without handling sensitive values.
- Applications and services can retrieve their authorised secrets.
- Required permissions and integrations have been validated.

#### Fully Migrated

A team is considered fully migrated when:

- All in-scope secrets and application dependencies have been migrated.
- Relevant integrations have been tested and validated.
- The team no longer depends on Vault for those workloads.
- Outstanding migration blockers have been resolved or explicitly accepted.

**Default onboarding:** AWS Secrets Manager was intended to become part of the standard AWS services made available to new teams through the Platform Team's existing bootstrap workflows.

These criteria provide the basis for the [adoption and migration progress metrics](#adoption--migration-progress).

### Automation-First Secret Management

The intended implementation separated **secret structure management from secret-value management**.

| Actor | Responsibility |
| --- | --- |
| CI/CD workflows | Create and delete secret structures (also referred to as *secret skeletons*) using predefined workflows |
| Authorised human users | Add, read and update secret values through the AWS Management Console |
| Applications and services | Retrieve authorised secret values during execution |
| Platform Team | Maintain shared capabilities, access patterns, and supporting workflows |

**Main objectives:**

- Standardise secret naming, ownership and configuration.
- Support reproducible and auditable secret provisioning.
- Reduce manual operations and encourage automation-first workflows.
- Avoid handling sensitive secret values through CI/CD inputs or logs, reducing the risk of accidental exposure.
- Use appropriate access controls and AWS Secrets Manager versioning capabilities.

In this project-specific design, CI/CD workflows managed the secret structures, while authorised human users managed the values.

The use of the AWS UI does not eliminate network transmission of secret values. Rather, the intended design reduced exposure through CI/CD pipelines and their execution logs.

The reliability and usage of these workflows would be evaluated through the [workflow metrics](#workflow-performance).

### Legacy Retirement Approach

The proposed approach included a **grace period of 2–4 sprints after all teams were fully migrated**, before retiring HashiCorp Vault.

**Key activities:**

1. **Inventory:** Identify remaining secrets and their associated owners or stream-aligned teams.
2. **Usage assessment:** Investigate recent secret access through available audit logs and relevant access history.
3. **Dependency verification:** Confirm that applications and CI/CD pipelines no longer depend on Vault.
4. **Communication:** Announce the planned retirement date and required actions to all stream-aligned teams.
5. **Exception handling:** Ask teams to report blockers or dependencies that could prevent them from meeting the deadline.
6. **Final validation:** Confirm that agreed retirement criteria are satisfied before shutting down the service.

An automated workflow to examine the Vault secret inventory and available access history was discussed as a potential solution.

**Important:** A secret's last retrieval may require analysis of retained audit logs; it is not necessarily available as a simple property in Vault. Low or absent observed usage should not be treated as definitive proof that a dependency no longer exists.

The grace period provides time for validation and exception handling, but the final retirement decision should depend on readiness rather than the calendar alone.

See [Vault Retirement Readiness](#vault-retirement-readiness) for the proposed measurements.

---

## Feedback & Continuous Improvement

### Developer Experience Survey

**Objective:** Collect qualitative and quantitative feedback on AWS Secrets Manager, its documentation, and the migration experience.

**Survey distribution:**

| | During migration | Post-migration |
| --- | --- | --- |
| Audience | Onboarded team members | All project members (200+) |
| Timing | During adoption | 1–2 months after migration completion |
| Response window | One month | One month (proposed) |
| Focus | Early friction and improvements | Overall experience and remaining concerns |

**Survey characteristics:**

- Collect team name, role and optionally name.
- Allow respondents to withhold identifying information where anonymity is requested.
- Consider indirect identification through small team/role combinations.
- Use consistent rating scales across survey waves.
- Provide *Not applicable* options for participants without direct experience.

**Proposed questions:**

| Question | Response type |
| --- | --- |
| How satisfied are you with AWS Secrets Manager? | 1–5 rating |
| How easy is it to find the secrets you need? | 1–5 rating / N/A |
| How easy was the migration process for your team? | 1–5 rating / N/A |
| How useful is the onboarding documentation? | 1–5 rating / Not used |
| Have you experienced recurring difficulties? | Open text |
| What worked particularly well? | Open text |
| What would you improve? | Open text |
| Is there anything else you would like to share with the Platform Team? | Open text |

The findings can be compared against the original user research themes, especially discoverability, ownership, permissions, integration and documentation.

Survey response rates and differences in respondent groups should be considered when comparing results.

### Retrospectives

#### During migration

Use regular sprint retrospectives to:

- Identify emerging issues and blockers.
- Discuss feedback from onboarded teams.
- Prioritise improvements that can be implemented during migration.
- Update documentation, workflows and support practices where needed.

#### Post-migration

Organise a dedicated retrospective with the Platform Team and representatives from stream-aligned teams.

Suggested discussion topics:

- What worked well during the migration?
- What were the main challenges?
- Which original user pain points were resolved or remained?
- How satisfied are teams with the new solution and documentation?
- What should be improved for future migrations?

Record agreed actions, owners and follow-up dates.

### Using Metrics to Support Decisions

The proposed framework should help the Platform Team answer:

- Are teams progressing from onboarding to full migration?
- Are workflows reliable and being used as expected?
- Which activities create the most support demand?
- Is the documentation enabling teams to work independently?
- How satisfied are stream-aligned teams with the solution, its features and documentation?
- Have the original user pain points been addressed?
- Is Vault ready for safe retirement?
- What should the Platform Team improve next?

Quantitative metrics should be combined with qualitative feedback and operational context to inform prioritisation and continuous improvement.

---

## Disclaimer

This framework combines different types of contributions:

- **Original project discussions:** Adoption, onboarding & Vault retirement metrics discussed with our Product Owner, Tech Lead and a Platform Owner.
- **Original project context:** The intended automation-first design, bootstrap workflows, grace period, and discussions around assessing remaining Vault usage.
- **Retrospective proposals:** Additional workflow, support, DevEx and retirement-readiness metrics, survey design, and continuous-improvement practices.

The retirement communication approach reflects recommendations I made during the project.

I was not part of the team when adoption began and cannot verify which metrics or activities were ultimately implemented.

No actual migration results or confidential project data are presented.

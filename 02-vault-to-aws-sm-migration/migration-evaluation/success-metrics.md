# Proposed Success Metrics

## Adoption & Migration Progress (Discussed during the project)

**Objective:** Track the adoption of AWS Secrets Manager and progress towards completing the migration.

| Metric | Measurement | Frequency | Lifecycle |
| --- | --- | --- | --- |
| Teams onboarded | Number of teams meeting the onboarding completion criteria | Per sprint / PI | During migration |
| Migration progress | Fully migrated teams / total in-scope teams × 100 | Per sprint / PI | During migration |
| Workflow usage | Number of executions of create/delete-secret workflows | Monthly | Ongoing |
| Workflow adoption | Number of distinct teams using each workflow | Monthly | Ongoing |

**Considerations:**

- *Onboarded* and *fully migrated* represent different milestones. See [Migration Practices](migration-practices.md).
- Onboarding and migration progress are temporary metrics that can be retired from regular reporting after migration completion and verification.
- Workflow usage and adoption remain relevant after migration, although secret creation and deletion may naturally become less frequent.

## Workflow Performance (Discussed during the project)

**Objective:** Assess the reliability and efficiency of the predefined create/delete-secret workflows.

| Metric | Measurement | Frequency |
| --- | --- | --- |
| Workflow executions | Total executions per workflow | Monthly |
| Workflow errors | Number of failed executions per workflow | Monthly |
| Workflow failure rate | Failed executions / total executions × 100 | Monthly |
| Execution time | Median and 95th-percentile time from start to completion | Monthly |

Where possible, errors should be categorised (e.g. permissions, invalid input or technical failures) to identify recurring problems.

The workflows and responsibilities are described in [Migration Practices](migration-practices.md).

## Support & Documentation (Retrospective Proposal)

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

## Developer Experience (Retrospective Proposal)

**Objective:** Understand user satisfaction, identify remaining pain points, and evaluate the experience of stream-aligned teams.

| Metric | Measurement | Frequency |
| --- | --- | --- |
| User satisfaction | Satisfaction rating from the survey (1–5) | During and after migration |
| Discoverability | User rating of how easy it is to locate secrets | During and after migration |
| Onboarding experience | User rating of the migration and onboarding process | During and after migration |
| Documentation usefulness | User rating of the available documentation | During and after migration |
| Recurring pain points | Themes identified through open-text feedback | During and after migration |

The survey methodology and proposed questions are described in [Feedback & Improvement](feedback-and-improvement.md).

These metrics should help assess whether the new solution addresses the needs identified during the original [user research](../discovery/research-findings.md).

## Vault Retirement Readiness (Discussed During the Project)

**Objective:** Assess whether Vault can be safely retired without disrupting stream-aligned teams.

| Metric | Measurement | Frequency |
| --- | --- | --- |
| Remaining Vault secrets | Number of secrets still present in Vault | Per sprint |
| Recently accessed secrets | Secrets with observed retrieval activity within the defined monitoring period | Per sprint |
| Teams with unresolved dependencies | Number of teams reporting active Vault dependencies | Per sprint |
| Migration exceptions | Number of unresolved blockers or approved exceptions | Per sprint |
| Retirement readiness | Completion of agreed technical and operational shutdown criteria | Before retirement |

A reduction in secret inventory or observed activity does not independently prove that Vault is no longer required.

The retirement approach and validation considerations are detailed in [Migration Practices](migration-practices.md).

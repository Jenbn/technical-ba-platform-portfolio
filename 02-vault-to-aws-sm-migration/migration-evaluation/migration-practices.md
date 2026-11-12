# Migration Practices & Considerations

## Onboarding & Migration Completion Criteria

Two milestones should be distinguished when evaluating migration progress.

### Onboarded

A team is considered onboarded when:

- All current team members have the appropriate AWS Secrets Manager access for their roles.
- Authorised human users can read and manage secret values through the AWS UI.
- CI/CD workflows can create and delete secret structures without handling sensitive values.
- Applications and services can retrieve their authorised secrets.
- Required permissions and integrations have been validated.

### Fully Migrated

A team is considered fully migrated when:

- All in-scope secrets and application dependencies have been migrated.
- Relevant integrations have been tested and validated.
- The team no longer depends on Vault for those workloads.
- Outstanding migration blockers have been resolved or explicitly accepted.

**Default onboarding:** AWS Secrets Manager was intended to become part of the standard AWS services made available to new teams through the Platform Team's existing bootstrap workflows.

These criteria provide the basis for the [adoption and migration progress metrics](success-metrics.md#adoption--migration-progress).

## Automation-First Secret Management

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

The reliability and usage of these workflows would be evaluated through the [workflow metrics](success-metrics.md#workflow-performance).

## Legacy Retirement Approach

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

See [Vault Retirement Readiness](success-metrics.md#vault-retirement-readiness) for the proposed measurements.

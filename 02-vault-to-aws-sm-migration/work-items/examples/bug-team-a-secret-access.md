# Bug — Incorrect Cross-Team Secret-Value Permissions in Pilot

*Status: Reconstructed portfolio example based on pilot testing; root cause not confirmed.*

## Title

Team A user denied access to own secrets but able to read and update Team B secret values

## Context

During the controlled Vault → AWS Secrets Manager pilot, a Tech Lead from **Team A** reported unexpected authorisation behaviour. Team A was one of **two stream-aligned pilot teams using different technology stacks**; the Platform Team also participated in testing. The pilot used **dummy secrets** to validate integrations and identify defects before releasing the functionality to all stream-aligned teams.

The Tech Lead created three dummy secret skeletons through the approved CI/CD workflow, with mandatory `team` and `type` tags, and signed in using their human identity in the AWS console.

The linked support request describes failed Team A access **and confirmed ability to retrieve and update Team B's dummy values**. In this illustrative workflow, the support pair could not resolve the issue during initial investigation, so a linked bug was raised for the Platform Team to follow-up.

- **Source:** [Team A support ticket](support-ticket-team-a-secret-access.md)
- **Feature:** Human-user IAM access for team-specific and shared secrets
- **Affected service:** AWS Secrets Manager / IAM tag-based access policies
- **Repository:** Internal IAM/infrastructure repository — link omitted
- **Environment:** Pilot / test; specific account and region omitted

## Expected Behaviour

- Team A human users can view metadata and manage values only for **authorised Team A team-specific secrets**.
- Shared-secret access follows the defined shared-secret policy.
- Team A human users **cannot retrieve or modify values of Team B's team-specific secrets**.
- Human users cannot create or delete secret skeletons; the authorised CI/CD workflow performs those operations.

## Actual Behaviour

- Team A's human-user identity receives **AccessDenied** for its own team-specific dummy secrets.
- Shared secrets are accessible in the console.
- The same Team A identity can **read Team B dummy secret values** and **update those values**, causing AWS Secrets Manager to create a new version.
- Whether the problem affects other teams or identities is not confirmed.

## Steps to Reproduce

1. Use an approved Team A human-user test identity in the pilot environment.
2. Create dummy test secret skeletons via the authorised workflow, including Team A-tagged secrets with `team: team-a` and `type: team-specific` (verify actual tag-key/value conventions).
3. Attempt to access Team A secrets and add a value through the AWS console. Record **AccessDenied**.
4. Under authorised pilot test conditions, retrieve the value of a **Team B dummy secret** using the same Team A identity.
5. Update the Team B dummy value and confirm that a new secret version is created.
6. Collect sanitised evidence such as access decisions and request IDs. Never include credential values in ticket comments or logs.

**Reproducibility:** Reported in pilot; broader scope requires verification.

## Technical Notes / Investigation — Root Cause Not Confirmed

- Compare IAM policy conditions and resource-tag matching with tags set by the secret-creation workflow.
- Verify the mapping between human identities, team roles and permitted secret resources.
- Review inherited permissions, policy attachments, permission boundaries, resource-based policies and applicable KMS authorisations.
- Inspect effective authorisation for `DescribeSecret`, `GetSecretValue` and `PutSecretValue` independently; reading or updating a value is materially different from merely listing secret metadata.
- Check any rule for `type: shared` is not inadvertently granting broader access to Team B team-specific secrets.
- Scope test execution to approved dummy data and authorised identities; involve the security owner as needed.

## Resources

- [Original support ticket](support-ticket-team-a-secret-access.md)
- [Research findings](../../discovery/research-findings.md)
- Sanitised pilot test evidence and policy evaluation: [omitted]
- Internal policy / infrastructure references: [omitted]

## Metadata

| Field | Value |
| --- | --- |
| Team | Platform Team |
| PI | [PI — omitted] |
| Sprint | Security triage first; schedule fix before rollout |
| Assignee(s) | [Unassigned] |
| Affected service | AWS Secrets Manager / IAM authorisation |
| Criticality | Security-sensitive pilot defect; priority requires prompt assessment |
| Source | [Team A pilot support ticket](support-ticket-team-a-secret-access.md) |
| Backlog status | Linked defect; **release blocker pending resolution and verification** |

## Bug Handling / Release Decision

The support pair's inability to resolve the issue during initial investigation can justify creating a distinct bug. However, **confirmed cross-team read and update permissions warrant security triage even in a pilot**. In this example, wider rollout should be blocked until appropriate access-control checks pass. The work may be tracked in the backlog, but it should not be treated as a routine medium/low defect simply because no real production secrets were involved.

If equivalent behaviour occurred after production rollout with real team secrets, it would require assessment under the organisation's security incident response process. This example does **not** claim that such a production incident occurred.

*Portfolio note: This is a reconstructed pilot defect, not a verified root-cause analysis or a production incident report.*

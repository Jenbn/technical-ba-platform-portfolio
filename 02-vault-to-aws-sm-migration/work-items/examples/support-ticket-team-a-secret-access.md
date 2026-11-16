# Support Ticket — Team A Cannot Access Its Own Secrets 

*Reconstructed portfolio example — pilot phase*

## Title

Team A Team A cannot manage its own secret values but can access Team B's secrets. 

## Description

As the Tech Lead of Team A, one of the stream-aligned teams participating in the AWS Secrets Manager pilot, I am testing secret access using my human-user account in the AWS Management Console.

I previously used the predefined CI/CD workflow to create three dummy secret skeletons, including the mandatory tags team and type (team-specific or shared).

## Expected behaviour

- I can read and update values of Team A's team-specific secrets.
- I can access authorised shared secrets.
- I cannot read or modify Team B's team-specific secret values.

## Observed behaviour

- I receive an AccessDenied message when trying to access Team A's test secrets.
- I can access shared secrets.
- I can read and update Team B's dummy secret values, creating new secret versions.

## Impacted Service & Repository

- **Service:** AWS Secrets Manager — human-user access permissions
- **Environment:** Pilot, using dummy secrets
- **Repository:** Internal repo — link omitted

## Frequency

Observed during pilot testing. Reproducibility across other users has not yet been verified.

## Criticality

**Security-sensitive pilot defect — requires prompt assessment.**

The issue was identified before the wider rollout, while the Platform Team and two stream-aligned teams were testing the solution using dummy secrets.

## Troubleshooting Already Attempted

- Confirmed that the correct Team A human-user account was used.
- Created three dummy secrets through the predefined workflow with the required tags.
- Attempted to access Team A's secrets through the AWS UI and received AccessDenied.
- Confirmed unexpected read and update access to Team B's dummy secrets.

## Steps to Reproduce

1. Log in to the AWS Management Console with an authorised Team A test account.
2. Open AWS Secrets Manager.
3. Attempt to access a Team A secret tagged team: team-a.
4. Observe the AccessDenied message.
5. Open a Team B dummy secret tagged team: team-b.
6. Observe that its value can be read and updated, creating a new version.

## Resources

- Screenshot of AccessDenied: [Attachment omitted]
- Workflow execution: [Internal link omitted]
- Related bug: Incorrect Cross-Team Secret Permissions
  
## Metadata

| Field | Value |
| --- | --- |
| Requesting team | Team A |
| Impacted service | AWS Secrets Manager |
| Category | Error / Access control |
| Criticality | Security-sensitive pilot defect |
| Status | Escalated to linked bug (illustrative) |
| Linked bug | [Bug — pilot access-control failure](bug-team-a-secret-access.md) |

## Support Outcome

The support pair was unable to resolve the issue during initial investigation. A separate bug ticket was created for further investigation and correction before wider rollout.

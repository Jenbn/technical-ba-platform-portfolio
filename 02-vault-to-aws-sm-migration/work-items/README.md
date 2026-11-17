# Work Item Examples — Vault to AWS Secrets Manager Migration

This folder contains reconstructed examples of work items from the Vault to AWS Secrets Manager migration, illustrating how we captured requirements, investigated technical questions, handled support requests, and tracked defects within the Platform Team.

## Examples

| Work Item | Description |
| --- | --- |
| [User Story — Human-User IAM Permissions](examples/human-secret-value-access.md) | Defines access permissions for managing secret values while restricting the creation and deletion of secret structures. |
| [Spike — Runtime Secret Updates](examples/spike-runtime-secret-updates.md) | Investigates possible approaches for consuming updated secrets in Kubernetes without redeploying services. |
| [Support Ticket — Team A Secret Access](examples/support-ticket-team-a-secret-access.md) | Documents an access-control issue reported by a stream-aligned team during pilot testing. |
| [Bug — Incorrect Cross-Team Permissions](examples/bug-team-a-secret-access.md) | Tracks the defect identified through the support ticket, including investigation and verification criteria. |

The support ticket and bug are linked to demonstrate how an issue reported during pilot testing could move from initial support investigation into the development backlog.

---

*Portfolio note: These examples have been reconstructed and anonymised for demonstration purposes. Internal links, confidential information and identifying details have been omitted. They are not verbatim Jira tickets.*

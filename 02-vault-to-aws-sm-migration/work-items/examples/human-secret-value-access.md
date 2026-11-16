# User Story — Manage Secret Values Through Role-Based IAM Permissions

*Status: Reconstructed portfolio example — proposed acceptance criteria, not a verified implementation.*

## Title

IAM Permissions for human users.

## Context

As part of the migration from HashiCorp Vault to AWS Secrets Manager, secret structure management and secret-value management were intended to have separate responsibilities.

Predefined CI/CD workflows would create and delete secret skeletons (the secret resource and its metadata), while authorised human users would manage sensitive values through the AWS Management Console. IAM permissions must reflect this separation, with appropriate access to team-specific and shared secrets.

This aims to support least-privilege access and reduce exposure of sensitive values in CI/CD pipelines and logs.

## Scope

### In scope

- Configure and validate IAM permissions for human identities to:
  - View metadata for secrets they are authorised to access.
  - View available secret versions and retrieve authorised secret values.
  - Add the initial value to an existing secret skeleton.
  - Update a value, creating a new secret version.
- Restrict write access to the appropriate team-specific.
- Verify that human users cannot create or delete secret skeletons through their assigned permissions.
- Validate the intended actions through the AWS Management Console.

### Out of scope

- Implementing the CI/CD create/delete-secret workflows.
- Changing the application/service permissions used for runtime secret retrieval.
- Designing secret naming conventions or ownership metadata.
- Implementing automated rotation or changes to KMS key management.

## Dependencies

- Existing secret skeletons provisioned by the CI/CD workflow; [link to related work item — omitted].
- Agreed IAM identity/role mapping and rules for team-specific versus shared secrets; [link to decision — omitted].
- Defined secret ownership and metadata conventions; [link to related work item — omitted].

## Goal

**As a** member of a stream-aligned team,  
**I want to** view and manage values and versions of secrets I am authorised to access,  
**so that** my team can maintain the credentials it needs without manually creating or deleting secret structures or exposing values through CI/CD workflows.  

## Acceptance Criteria

| AC | Given | When | Then |
| --- | --- | --- | --- |
| **AC1 — View secret metadata** | I am an authenticated user with access to a team-specific or shared secret | I open the secret in the AWS Secrets Manager UI | I can view its metadata, including its name, description and tags |
| **AC2 — Read secret values** | I am authorised to read a secret | I request its current value through the AWS UI | I can view the secret value |
| **AC3 — View secret versions** | I am authorised to access a secret and its version history | I navigate to the secret's versions | I can view the available versions and retrieve values from versions I am authorised to read |
| **AC4 — Add an initial secret value** | An authorised CI/CD workflow has created a secret skeleton without a value | I add the first secret value through the AWS UI | The value is stored successfully and a new secret version is created |
| **AC5 — Update secret values** | I have permission to manage a team-specific or shared secret | I update its value through the AWS UI | A new version is created and the updated value becomes the current version |
| **AC6 — Enforce team-specific access** | A secret belongs to a team I am not authorised to access | I attempt to view or modify its value | Access is denied |
| **AC7 — Prevent secret skeleton creation** | I am authenticated with the human-user IAM role | I attempt to create a new secret skeleton | The operation is denied |
| **AC8 — Prevent secret skeleton deletion** | I am authenticated with the human-user IAM role | I attempt to delete an existing secret | The operation is denied |

## Technical Notes

- [Relevant technical details or constraints agreed with the team; avoid prescribing a solution before refinement]

## Resources

[Original research findings](../discovery/research-findings.md)
[AWS — Secrets Manager IAM policy examples](https://docs.aws.amazon.com/secretsmanager/latest/userguide/auth-and-access_iam-policies.html)
[AWS — Actions, resources and condition keys](https://docs.aws.amazon.com/service-authorization/latest/reference/list_secretsmanager.html)
[AWS — PutSecretValue API](https://docs.aws.amazon.com/secretsmanager/latest/apireference/API_PutSecretValue.html)
[Internal feature and architecture references omitted for confidentiality]

## Metadata

| Field | Value |
| --- | --- |
| Team | Platform Team |
| PI | [PI — illustrative placeholder] |
| Sprint | [Sprint — illustrative placeholder] |
| Assignee(s) | [Unassigned] |
| Feature keyword | [Vault-to-AWS-SM — illustrative placeholder] |
| Feature link | [Internal link omitted] |
| Deadline (optional) | Not specified |
| Author | [Business Analyst — illustrative placeholder] |

*Portfolio note: The story reflects the intended responsibility model discussed in the migration case study. Its acceptance criteria and implementation considerations are reconstructed examples and were not verified against the original delivered backlog.*

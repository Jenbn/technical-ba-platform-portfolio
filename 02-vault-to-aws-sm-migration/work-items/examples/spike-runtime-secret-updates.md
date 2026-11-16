# Spike — Runtime Secret Updates for Kubernetes Workloads

*Status: Reconstructed portfolio example*

## Context

In the existing setup, updating a secret can require redeploying the consuming service before it uses the new value. This creates manual work and potential operational disruption.

The goal of this spike is to investigate how Kubernetes-hosted services could consume updated secrets from AWS Secrets Manager without requiring a redeployment or Pod restart.

The investigation should identify feasible approaches, their advantages and disadvantages, and any application or infrastructure changes needed.

## Scope

### In scope

- Understand the current secret-consumption mechanism and why redeployment is necessary.
- Investigate runtime secret-retrieval and refresh mechanisms compatible with Kubernetes and AWS Secrets Manager.
- Compare possible approaches based on security, maintainability, complexity, performance, reliability and cost.
- Identify whether a proof of concept is needed to validate the most promising approach.

### Out of scope

- Implementing the final production solution.
- Migrating all existing services to a new secret-consumption mechanism.
- Changing the agreed access-control model for creating and managing secrets.

## Acceptance Criteria / Expected Outputs

- [ ] Current limitations and reasons for service redeployment are documented.
- [ ] At least two feasible technical approaches are investigated.
- [ ] Pros, cons, dependencies and risks of each approach are documented.
- [ ] The difference between propagating updated secret values and applications actually reloading them is assessed.
- [ ] A recommendation or decision-ready shortlist is presented to the Platform Team.
- [ ] Follow-up work items and unresolved technical questions are identified.

## Time-box

**Proposed:** Two developer-days for investigation and documentation.

If further validation is required, a follow-up spike or proof of concept should be considered.

## Technical Notes

Potential approaches to investigate:

- **AWS Secrets Manager SDK/API:** Applications retrieve secret values directly, using an appropriate caching or refresh strategy.
- **Secrets Store CSI Driver:** Secrets are mounted as files in Kubernetes workloads, with supported mechanisms to refresh their contents.
- **External Secrets Operator:** Secrets are synchronised into Kubernetes Secrets, with an additional mechanism for applications to consume updated values.

The investigation should consider:

- Kubernetes compatibility and existing application architecture.
- How quickly updated values become available.
- Whether applications can reload secrets without restarting.
- IAM permissions and workload identities.
- Error handling, monitoring and availability.
- Operational complexity and maintenance costs.

## Resources

- [Kubernetes — Distribute Credentials Securely](https://kubernetes.io/docs/tasks/inject-data-application/distribute-credentials-secure/)
- [AWS Secrets Manager Integration with EKS](https://docs.aws.amazon.com/secretsmanager/latest/userguide/integrate_eks.html)
- [Secrets Store CSI Driver](https://secrets-store-csi-driver.sigs.k8s.io/)
- [External Secrets Operator](https://external-secrets.io/latest/introduction/faq/)

## Metadata

| Field | Value |
| --- | --- |
| Team | Platform Team |
| PI | [PI] |
| Sprint | [Sprint] |
| Assignee(s) | [Unassigned] |
| Feature Keyword | [Vault-to-AWS-SM] |
| Feature Link | [Internal link omitted] |
| Deadline | [Optional] |
| Author | [Author] |

*Portfolio note: This example illustrates how a technical investigation could be structured. The proposed technical alternatives have not been evaluated or selected as part of this example.*
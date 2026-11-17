# Technical Spikes — Pre-development Investigations

Several technical topics had to be explored before the team committed to implementation choices. We treated these as spikes, not as activities performed by stream-aligned teams in the story map.

| Investigation | Question to answer | Related story-map area | Expected output |
| --- | --- | --- | --- |
| AWS Secrets Manager metadata and search | What metadata and search functionality is available, and how can teams find secrets without knowing an exact path? | View Secrets / Manage Secrets | Feasible search approach, metadata/tag conventions and limitations |
| Runtime integration | How can Kubernetes workloads consume updated values without requiring a service redeployment, and what must applications do to refresh them? | Manage Secrets → Access / Update | Alternative approaches, trade-offs and dependencies |
| AWS Secrets Manager auditing | What is available through audit logs versus system/operational logs, and what can the team reliably observe? | Observability → View logs | Log-source comparison, visibility gaps and suggested follow-up work |
| Secret rotation | What does AWS Secrets Manager offer for rotation, and what custom approaches could be supported so teams can choose what fits their use cases? | Security / Manage Secrets / Monitoring | Options with pros and cons, integration and ownership implications |

## Relationship to the map

These investigations reduced technical uncertainty and informed subsequent development decisions. They can be linked to the relevant tasks or stories as dependencies without being inserted into the user journey itself.

For the portfolio, the [runtime integration spike example](../work-items/examples/spike-runtime-secret-updates.md) is a reconstructed work item.

*Portfolio note: These are investigation topics, not evidence of a particular technical solution being selected or delivered. Detailed findings and outcomes are intentionally not invented.*

# Story Mapping — Vault to AWS Secrets Manager Migration

This recreation illustrates how we used story mapping to turn discovery findings into a shared view of the migration and agree on an initial release.

## How we worked

**Before the workshop:** As the Technical BA, I prepared the user groups, big activities and narrative flow. I also brought findings from stakeholder interviews into the discussion: difficulty finding secrets, inconsistent secret structure, duplicated secrets, unclear ownership and runtime errors or disruption when secret values changed.

**During the workshop:** I asked the Platform Team to review the prepared activities and identify anything missing. We then worked together to break the flow into more specific tasks and capabilities.

**Release slicing:** The Tech Lead, Product Owner, Platform Owners and I agreed an initial Release 1 (MVP) and Release 2 split. We presented it back to the wider team for feedback and to identify omissions.

## Why we chose this MVP

The priority for **Release 1** was to make the core AWS Secrets Manager workflows available and migrate the Platform Team and selected pilot teams early. The pilot involved two stream-aligned teams with different technology stacks, testing with dummy secrets before broader rollout. This enabled earlier feedback on access permissions, workflows and integration. **Release 2** focused on additional automation, wider migration and Vault retirement.

The release split was a planning decision, not a claim that all mapped tasks were delivered exactly as originally drawn.

## Artefacts

- [Visual story map (PDF)](story-map.pdf) — a wide-format overview of the actors, activities, narrative flow and Release 1 / Release 2 tasks from the original workshop diagram
- [Technical spikes](technical-spikes.md) — investigation work tracked separately from user activities
  
*Portfolio note: Reconstructed and anonymised from a workshop artefact. It is not a verbatim Mural board. Interview findings have been made explicit here even though they were not shown on the exported source diagram. No confidential links or credentials are included.*

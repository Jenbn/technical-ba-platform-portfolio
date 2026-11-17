# Bug Template

*Used to record defects that require separate tracking. During development of a new feature, defects found within the active work were normally fixed by the development pair rather than automatically creating a separate bug ticket.*

## Title

[Short description of the incorrect behaviour]

## Context

[How and when the defect was discovered; affected feature, repository, service, and environment.]

## Expected Behaviour

[What should happen?]

## Actual Behaviour

[What happens instead? Include observable effects, not assumptions about the root cause.]

## Steps to Reproduce

1. [Starting conditions or test data — no secrets]
2. [Action]
3. [Action]
4. [Observed result]
**Reproducibility: [Always / intermittent / unknown]**

## Resources

- [Sanitised screenshot, screen recording, logs, relevant links]

## Metadata

| Field | Value |
| --- | --- |
| Team | [Team] |
| PI | [PI] |
| Sprint | [Sprint] |
| Assignee(s) | [Name(s) / unassigned] |
| Affected service | [Service] |
| Criticality | [Critical / Medium / Low] |

## How Our Team Handled Bugs

**During development:** Bugs discovered while a feature was being developed were normally addressed by the development pair as part of that work.

**After release / after the pair finished its work:** The team assessed the defect and prioritised it based on production impact:

| Criticality | Project practice |
| --- | --- |
| Critical production bug | Core functionality unavailable or users unable to use the affected service; prioritise immediate investigation and fix |
| Medium production bug | Limited team impact without loss of core functionality; PO assesses and places it among the next backlog candidates |
| Low-priority bug | Limited impact; add to backlog for a future sprint |

*These are a description of the team's working agreements, not a universal incident-severity standard. Criticality should be assessed using real user and service impact, and re-evaluated if circumstances change.*

# Flow Metrics & Forecasting

*A Technical Business Analyst portfolio case study on using delivery data to support planning and continuous improvement.*

## What's in this repository?

This project has two connected but distinct parts:

1. **What I did in a real platform team:** I used sprint delivery, throughput, time-in-status and cycle-time information to understand delivery patterns, facilitate conversations and help the team improve planning and workflow.
2. **What I explored afterwards:** I built an analytical workbook with synthetic work-item data, visualisations and two Monte Carlo forecasting simulations. This was a retrospective learning exercise; I did not use Monte Carlo forecasting in the original project.

**Team Aqueduct is a fictional team name**. The workbook is not an export of my former team's Jira or eazyBI records. It models delivery situations inspired by my experience, but its individual records, dates and forecast results are invented.

## Repository contents

- [Case study](case-study.md) — What I observed, discussed and changed with the team; how the metrics supported planning; and the retrospective Monte Carlo exercise.
- Analysis workbook - Synthetic dataset, flow metrics, sprint delivery analysis, and two retrospective Monte Carlo simulations:
  - [Explore the analysis in Google Sheets](https://docs.google.com/spreadsheets/d/1PH6bDGx60KW_-77tscZUf3W54xKOBAM4CkPxAl1xB3I/edit?usp=sharing)
  - [Download the Excel workbook](data/team_aqueduct_metrics.xlsx)

## Workbook guide

| Tabs | What to look for |
| --- | --- |
| `Work_Items`, `Sprints`, `Sprint_Assignments`, `Status_History` | The underlying synthetic work-item, sprint, assignment and status-transition records. |
| `Sprint_Delivery` | Planned vs. completed work, scope changes, spillovers and the comparison across PIs. |
| `Throughput`, `Throughput_By_PI` | Completed item counts per sprint, PI totals and comparisons of regular sprints. |
| `Cycle_Time`, `Cycle_Time_By_PI`, `Cycle_Time_By_Type` | Working-day cycle time and distributions by PI or work-item type. |
| `Time_In_Status`, `Time_Per_Work_Item` | Time spent in workflow statuses, including summaries and per-item durations. |
| `Monte_Carlo_How_Many` | Live simulation of how many items might be completed in one PI. |
| `Monte_Carlo_Snapshot` | Fixed results from a recorded *How Many?* simulation run. |
| `Monte_Carlo_When` | Simulation of how many sprints are needed to complete a 60-item backlog. |

**Suggested reading path:** Read the [case study](case-study.md) first, then open the workbook to explore the associated tables, calculations and charts.

## Modelling context

- **Timeframe:** Four Program Increments (PIs), each with six two-week sprints.
- **Sprint cadence:** Sprints 1–5 are regular development sprints; Sprint 6 has one week for carryover/closure and one for innovation.
- **Forecasting:** Monte Carlo samples regular sprints and Sprint 6 separately to reflect their different capacities.
- **Cycle time:** Calculated in working days, excluding weekends but not public holidays.
- **Interpretation:** Item counts do not reflect equal effort, value or complexity. A work item that spills over more than once may contribute multiple spillover occurrences.

## AI use and limitations

- **AI assistance:** Used to generate and adjust synthetic records, and to help develop and troubleshoot Google Sheets formulas and Monte Carlo simulations.
- **My contribution:** I selected the analytical questions, built and reviewed the analyses, and interpreted the results. The real project practices and decisions in the [case study](case-study.md) are based on my experience.
- **Not real project data:** The fictional dataset does not verify the historical outcomes described in the case study.
- **Forecast limitations:** Monte Carlo results are illustrative, based on a small synthetic sample. They assume comparable future conditions and do not fully account for dependencies, changing scope or differences in item complexity. They are not validated delivery probabilities.

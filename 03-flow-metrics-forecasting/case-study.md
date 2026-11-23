# From Flow Metrics to Better Planning

*Technical Business Analysis | Platform teams | Delivery predictability | Retrospective forecasting*

## About this case study

This is a reflection on **two different pieces of work**. During my time in a platform team, I used delivery and flow metrics to challenge assumptions, bring evidence into planning discussions and help us improve our workflow. Later, as a **retrospective portfolio exercise**, I explored those same metrics and built Monte Carlo simulations in Google Sheets.

The accompanying [workbook](data/team_aqueduct_metrics.xlsx) contains **synthetic** records for a fictional team called **Team Aqueduct**. The charts show the synthetic exercise, **not historical data from my employer**. The [README](README.md) explains the dataset, how I used AI assistance, and the modelling limitations.

## 1. Sprint delivery and spillovers — making commitments more realistic

**What the metric means.** Sprint delivery compares the number of items planned at sprint start with the number completed, added and removed. A *spillover* is a piece of work that remains unfinished and carries into a later sprint. Repeated carryovers can be counted as repeated occurrences.

**See in the workbook:** `Sprint_Delivery`

**What I did.** We were frequently having **five spillovers**. I created an **eazyBI** view of sprint delivery and throughput across previous PIs to see how many stories we actually completed. I shared this with our PO, and we used the observed delivery range as a reference when discussing what was reasonable to commit to. It helped us move beyond planning based on primarily story-point totals.

**What changed.** After applying this historical-data-informed approach to planning, we observed spillovers decreasing from approximately **five to two per sprint**. I see this as a meaningful team outcome, not proof that any single change caused the reduction.

**What it tells a PO or BA.** Sprint delivery makes overcommitment and scope movement visible. It creates space to ask *why* items are carried over. For comparisons in the synthetic workbook, Sprint 6 is different from regular sprints because it includes innovation time.

## 2. Throughput — grounding forecasts in completed work

**What the metric means.** Throughput is the number of work items completed over a defined period, such as a sprint. It measures **item count**, not effort or delivered business value.

**See in the workbook:** `Throughput` for sprint-level counts and `Throughput_By_PI` for PI-level totals and averages, including a comparison based on regular Sprints 1–5.

**What I did.** Story points were expected in the project, and we had been using them for forecasting. After reading articles and *When Will It Be Done?*, I wanted to explain why a story-point estimate cannot fully capture the time work spends waiting for reviews, feedback, sign-offs or external teams. I organised a **knowledge-sharing session** to discuss that with colleagues.

I did **not** advocate removing points altogether. They remained a useful way to discuss relative complexity and uncertainty, and the project expected them. With the Tech Lead, I developed a **Fibonacci-based reference table**, with an explanation and a representative story for each point value. Meanwhile, throughput offered the PO and me a more tangible historical baseline for planning.

**What it tells a PO or BA.** Recent, comparable throughput can support conversations about a realistic **range** of future output. It needs context: item mix, holidays, staffing, dependencies and the team's definition of *done*. It should not become a target to maximise by splitting work arbitrarily.

## 3. Time in status — finding waiting time and handoff bottlenecks

**What the metric means.** Time in status measures how long a work item stays in a workflow state, including waiting time. If it visits a state multiple times, those durations can be combined. A long duration does not mean someone worked actively for that entire time.

**See in the workbook:** `Time_In_Status` for status-duration distributions and `Time_Per_Work_Item` for the duration breakdown of individual items. The analysis uses working days.

**What I did.** I noticed that items were spending substantial time around **QA and ready-for-sign-off**. I brought this to the PO, Tech Lead and team for discussion. The team proposed **dedicated desk-check and sign-off slots twice per week**. I additionally proposed a **first-in, first-out (FIFO)** default for these queues, after noticing that newer requests were sometimes prioritised simply because their owners pushed for review first. Legitimate urgent exceptions still needed consideration.

I also encouraged the team to **keep workflow statuses accurate**, because an item that has moved on in reality but not in Jira creates misleading data.

**What it tells a PO or BA.** Time in status helps distinguish development effort from queues and handoffs. It prompts interventions that can be tested later—for instance, whether planned review slots actually reduce waiting and whether queues are handled more transparently.

## 4. Cycle time — investigating outliers and shortening feedback loops

**What the metric means.** Cycle time measures elapsed time from a defined start point to completion. In this workbook it runs from first **in development** to **done**, counted using working days (weekends excluded; public holidays not excluded). Median and 85th-percentile views show the typical experience and the longer tail.

**See in the workbook:** `Cycle_Time`, `Cycle_Time_By_PI`, `Cycle_Time_By_Type`.

**What I did.** The PO and I identified specific items with unusually long cycle times and took them back to the team to understand their contexts. A recurring example was changes requiring feedback from **stream-aligned teams**, such as a **Java 11 to Java 17** transition. Validation in testing and production environments extended the time until an item could be closed.

We agreed to separate **testing-environment work** from **production-environment work** into two items. That made progress and dependencies more visible. We allowed a short feedback period—typically **one or two working days**—and asked teams to open support tickets for issues reported afterwards, rather than leaving an original story open indefinitely. This was a workflow arrangement, **not a claim that production changes become safe after two days**. We also worked on making stories smaller, delivering useful increments sooner, and ensuring spikes had a limited investigation scope.

**What it tells a PO or BA.** Looking at actual outliers can reveal recurring dependency patterns and opportunities to slice work differently. A long cycle time is a question to investigate, not evidence that someone performed poorly. I would pair these observations with quality and operational outcomes before judging the effectiveness of a change.

## 5. Monte Carlo — a retrospective forecasting exercise

**What I had done at the time:** I had worked with throughput and percentiles but **had not used Monte Carlo simulations in the original project**. I built the following examples later, with AI assistance, to learn how a BA or PO might communicate uncertainty more clearly.

### Why use Monte Carlo?

Historical throughput tells us how much work has been completed in comparable periods. But using just an average hides variation. A **Monte Carlo simulation** repeatedly samples historical outcomes to construct a distribution of possible future results, which supports two planning questions:

- **How Many?** How many items might be completed within a fixed timebox?
- **When?** How many sprints might be needed to finish a fixed number of items?

The outputs are **model-based probabilities, not promises**. They are most useful as a starting point for discussions about scope, capacity and risk.

### Data and assumptions

I used the synthetic Team Aqueduct workbook: **four PIs**, each with **six two-week sprints**. Sprints **1–5** are regular development sprints; Sprint **6** includes one week for carryover and one innovation week. I therefore separated the history into **20 regular-sprint throughput values** and **four Sprint 6 values**, then sampled from the appropriate pool for each future sprint. Each model runs **1,000 simulations**.

This is a small dataset, particularly for Sprint 6. The model assumes broadly comparable future capacity and work mix, and does not explicitly simulate new scope, dependencies or correlated delays.

### Example A — How Many? One PI

**Question:** How many work items might be completed in one six-sprint PI?

**See in the workbook:** `Monte_Carlo_How_Many` for the live model and chart; `Monte_Carlo_Snapshot` for a fixed example and recorded forecast figures.

From the **snapshot**:

| Target minimum-delivery probability | At least this many completed items | Observed share of 1,000 simulations |
|---|---:|---:|
| 50% | 54 | 51.4% |
| 70% | 52 | 72.1% |
| 85% | 50 | 87.5% |
| 95% | 47 | 96.3% |

**Interpretation.** In this model run, **87.5%** of simulated PIs finished **at least 50 items**, compared with **51.4%** that finished **at least 54**. That illustrates why a PO might frame 50 as a more cautious planning threshold and 54 as a higher-risk scope—while still discussing the nature and value of the work.

Note that the live `Monte_Carlo_How_Many` tab recalculates and may show different probabilities from the saved snapshot.

### Example B — When? A backlog of 60 items

**Question:** How many sprints might be required to complete **60 work items**?

**See in the workbook:** `Monte_Carlo_When`

The workbook's recorded results show:

| By the end of | Simulations completed |
|---|---:|
| Sprint 5 | 0.6% |
| Sprint 6 (one PI) | 2.9% |
| Sprint 7 | 85.1% |
| Sprint 8 | 99.9% |
| Sprint 9 | 100% |

**Interpretation.** Completing 60 items in a single six-sprint PI appears unlikely under the model. A deadline at **Sprint 7** corresponds to approximately **85%** simulated likelihood, while Sprint 8 offers a more conservative forecast. Even **100% of the sampled outcomes** does not guarantee completion on a real project.

### How I would use this in practice

I would first check that the throughput history reflects the team's current capacity and definition of done. Then I would use the two forecasts in PI planning or roadmap conversations to compare possible scopes and dates, **make uncertainty explicit**, and ask what conditions would invalidate the forecast. I would rerun the model when staffing, scope or team workflow changed, and compare later forecasts with actual delivery to assess whether the assumptions were useful.

I would also preserve **fixed simulation snapshots** before quoting exact probabilities, because random sampling functions recalculate. The *How Many?* figures above use the stored snapshot; the *When?* figures come from the workbook's displayed simulation and may change when recalculated. They are **not** results of one joined, fully calibrated forecast.

---

## What I learned

The most valuable part of flow metrics was **not the charts themselves**. It was how the data helped me ask better questions, collaborate with the PO and Tech Lead, and bring practical experiments to the team. The reduction in spillovers is an observation from my professional experience, not a result proven by the fictional dataset.

The retrospective Monte Carlo exercise helped me take the next step: instead of presenting a single number as a prediction, I can now explain the **likelihood and assumptions behind different planning options**.

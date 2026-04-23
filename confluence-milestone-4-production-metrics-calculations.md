# Milestone 4 — Production dashboard: how metrics are calculated

**Published in Confluence (TROY):** https://nubank.atlassian.net/wiki/spaces/TROY/pages/265069822173/Milestone+4+Production+dashboard+how+metrics+are+calculated  
**Parent:** [Beta - Metrics](https://nubank.atlassian.net/wiki/spaces/TROY/pages/264701673940/Beta+-+Metrics)

**Related:** [Milestone 3 — Outcome & beta monitoring hub](https://nubank.atlassian.net/wiki/spaces/TROY/pages/265069264929/Milestone+3+Outcome+beta+monitoring+hub)

---

## Alignment with parent (Beta - Metrics)

This page supports **Milestone 4 — Must Have Metrics**:

- **Goal:** Ensure critical metrics are reliable and visible first.
- **Must-have list:** Finalize the subset essential for operations, product, and leadership.
- **Implementation:** For each must-have metric, implement and validate source of truth, **calculation**, and monitoring; confirm accuracy, timeliness, and accessibility.
- **Outcome:** All must-have metrics defined, implemented, validated, and monitored in the hub.

This document states **how each Production-dashboard metric is intended to be calculated** and **how the current [Beta Metrics Dashboard](https://jacqueponce.github.io/beta-timeline/beta-testing-metrics-dashboard.html) actually behaves** (including gaps).

---

## Scope

Applies to the **Production** tab of the metrics dashboard: **North Star** KPIs, **Go / No-Go Gates**, **scenario table** (including **Health**), **progress bar**, **bug tracker**, and **Must-Have Metrics** summary — unless noted otherwise.

---

## North Star KPIs (Production)

| KPI | Intended meaning | Current implementation |
| --- | --- | --- |
| **Scenarios Done** (e.g. 0/32) | Count of scenarios whose Jira work is **Done** | **Static HTML** — not recomputed from Jira when statuses change |
| **Completion %** (e.g. 0%) | Derived from scenarios done / total (32) | **Static HTML** |
| **Open Bugs** | Count of open defects (by severity as designed) | **Static HTML** |

---

## Go / No-Go Gates (top section)

### Scenario Coverage (e.g. 0/32)

- **Calculation (intended):** Count scenarios where Jira **status = Done**.
- **Gate:** **29/32** required (threshold documented on the hub / parent metrics page).
- **Current implementation:** Value is **hardcoded** in static HTML; **not** dynamically computed from Jira.

### Evidence Complete (e.g. 0/32)

- **Calculation (intended):** Count scenarios that have **evidence signed off** (per program definition — typically linked to Jira fields, attachments, or a checklist).
- **Gate:** **32/32** signed off required.
- **Current implementation:** **Hardcoded**; **not** linked to a live data source.

### Bug Resolution (e.g. 0 P1, 0 P2 open)

- **Calculation (intended):** Count **open** bugs with priority **P1** and **P2**; gate **green** when **zero** P1/P2 open.
- **Current implementation:** **Hardcoded**.

### Reconciliation (e.g. Manual / 0 deviations)

- **Calculation (intended):** **Manual** assessment of ledger / operational **deviations** (per reconciliation process).
- **Current implementation:** **Hardcoded** (placeholder for manual status).

### System Automation (e.g. Manual / All flows auto)

- **Calculation (intended):** **Manual** assessment of how much of the critical path runs under **system automation** vs manual intervention.
- **Current implementation:** **Hardcoded** (placeholder for manual status).

---

## Other Production sections (static today)

| Area | Notes |
| --- | --- |
| **Progress bar** (scenario progress) | **Static** — does not auto-update from Jira. |
| **Bug tracker** (table / counts by priority) | **Static** — not fed live from Jira. |
| **Must-Have Metrics** summary block | **Static** — mirrors gates / scenarios; not auto-synced. |

---

## Health column (scenario table) — **dynamic**

The **Health** column is the **only** metric on the Production dashboard that is **computed in the browser** from live row inputs and dates.

**Inputs**

- **Jira status** from each scenario row (e.g. Backlog, In Progress, Done).
- **Timeline window** from **`PRD_DATES`**: from **first `open_bill`** through **last `due_date`** for that scenario.
- **Today’s date** (browser / client “today”).

**Rules (`computeHealth()` logic)**

1. Status **Done** → **DONE** (green).
2. **Today after end date** and status **not** Done → **DELAY** (red).
3. Status **Backlog** / **Not Started** and **today after start date** → **DELAY** (red).
4. Status **Backlog** / **Not Started** and **today before start date** → **ON TRACK** (yellow).
5. Status **In Progress** and **today before end date** → **ON TRACK** (yellow).

*(Implementations may add edge cases; this reflects the documented behavior.)*

**Injection:** `injectHealth('prod-table', PRD_DATES)` applies the above per row after load.

---

## Summary: static vs dynamic

| Dynamic? | Metric / area |
| --- | --- |
| **Yes** | **Health** column only (`computeHealth` + `PRD_DATES` + status + today). |
| **No** | North Star KPIs (scenarios done, %, open bugs); **all** Go/No-Go gate numbers; progress bar; bug tracker; Must-Have Metrics block — **static / hardcoded HTML** until wired to Jira (or another source of truth) and rebuilt (e.g. `build_dashboard.py`). |

---

## Milestone 4 gap (for implementation)

To meet M4’s **outcome** (“accurate, timely, accessible” in the hub), the Production dashboard still needs:

1. **Source of truth** for each gate and north-star KPI (Jira API, export, or pipeline).
2. **Automated or repeatable refresh** so counts match Jira / evidence / bugs at publish time.
3. **Validation** that thresholds (29/32, 32/32 evidence, zero P1/P2) match the signed definitions on **Beta - Metrics**.

Until then, treat **gates and headline numbers as documentation snapshots**, not live monitors — except **Health**, which is live relative to embedded dates and row status.

---

## References

- Parent: [Beta - Metrics](https://nubank.atlassian.net/wiki/spaces/TROY/pages/264701673940/Beta+-+Metrics)
- [Beta Metrics Dashboard](https://jacqueponce.github.io/beta-timeline/beta-testing-metrics-dashboard.html)
- Repo: `beta-testing-metrics-dashboard.html`, `computeHealth()` / `injectHealth()`, `PRD_DATES` (production table)

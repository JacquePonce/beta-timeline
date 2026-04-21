# Milestone 3 — Outcome & beta monitoring hub

**Published in Confluence (TROY):** https://nubank.atlassian.net/wiki/spaces/TROY/pages/265069264929/Milestone+3+Outcome+beta+monitoring+hub  
**Parent:** [Beta - Metrics](https://nubank.atlassian.net/wiki/spaces/TROY/pages/264701673940/Beta+-+Metrics)

Source copy below matches the page body; edit in Confluence for canonical version.

---

## Alignment with parent (Beta - Metrics)

This page implements **Milestone 3 — Tools + Monitoring Hub** from the parent page:

- **Goal:** Centralize tooling and visibility.
- **Tools:** Choose and standardize how we monitor metrics, define visualization, and share updates.
- **Monitoring hub:** A single place where teams can see which metrics exist, their definitions, owners, and links to dashboards/alerts.
- **Outcome:** Agreed tool stack and a central **monitoring hub** for discovery, definitions, and access to monitoring.

---

## Purpose

Record how we satisfy that milestone for **Troy CC US Beta**: the **canonical monitoring hub** URL, what “done” looks like for M3 in this program, and how **Staging** vs **Production** views differ on the hub.

---

## Outcome of M3 (this program)

By the end of M3 for beta E2E, the program should be able to show:

1. **North star is visible** — Progress toward *100% successful execution of critical path flows without manual intervention* is tracked on the hub (not only in decks).
2. **Production readiness signals** — The Production tab surfaces scenario coverage, evidence sign-off, and operational gates (bugs, reconciliation, automation) per definitions on the parent page.
3. **One monitoring hub** — Day-to-day monitoring uses the dashboard below; Confluence (**Beta - Metrics**) remains the definitions source of truth.
4. **Staging vs production traceability** — The same 32 scenarios use separate Jira backing for staging vs production so pre-prod and prod readiness stay clear.

---

## Monitoring hub (canonical URL)

**Troy CC US Beta — Metrics Dashboard**  
https://jacqueponce.github.io/beta-timeline/beta-testing-metrics-dashboard.html

- Use the **Metrics Definitions** link on the dashboard back to this space.
- The dashboard is a Jira snapshot; rebuild with `build_dashboard.py` before publishing updates (see `troy-beta-dashboard` in the repo).

---

## Staging vs Production dashboards

The hub is **one URL** with two tabs. Same **32 scenarios** and **north star**; differences:

| Dimension | **Staging** tab | **Production** tab |
|-----------|-----------------|---------------------|
| **Role** | Pre-production execution vs **staging** Jira initiative | Production beta vs **production** Jira initiative (same scenario IDs, different tickets) |
| **North star KPIs** | Scenarios done + completion % | Same + **open bugs** in the north star row |
| **Gates** | Scenario coverage + Evidence complete | Adds **Bug resolution**, **Reconciliation**, **System automation** (go/no-go bar) |
| **Timeline** | Staging window only | Staging + production beta + F&F milestone |
| **Tab label** | **LIVE** (active pre-prod burn-down) | **WIP** (prod monitoring maturing) |

**Summary:** Staging answers “have we proven flows in a safe environment?” Production answers “are we green to run in prod with customers under our operational bar?”

---

## References

- Parent: [Beta - Metrics](https://nubank.atlassian.net/wiki/spaces/TROY/pages/264701673940/Beta+-+Metrics)
- [CC Beta Release Milestone Plan](https://nubank.atlassian.net/wiki/spaces/TROY/pages/264681685202)
- [Beta Metrics Dashboard](https://jacqueponce.github.io/beta-timeline/beta-testing-metrics-dashboard.html)

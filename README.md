# Revenue Cycle Intelligence Dashboard (Denials + A/R + Payer Mix)

A decision-support Power BI dashboard that helps healthcare leaders understand **why claims are getting denied, how A/R is aging, and where revenue cycle performance can be prioritized for follow-up.**

This project is built to be **executive-readable** and **analyst-reproducible**.

---

## What this enables
Leaders can use this dashboard to:

- Track denial rate trends and identify top denial drivers
- See denial patterns by payer, provider, location, and category
- Monitor A/R aging and estimate where cash is “stuck”
- Evaluate net collections and time-to-payment patterns
- Prioritize operational follow-up (appeals, resubmissions, root cause fixes)

---

## Data source

This project uses:
- **Synthetic claims + denial + payment data** generated to mirror common RCM workflows, OR

No patient-identifiable data is used.

---

## Dashboard pages 

1) **Executive Summary**
   - Denial Rate, Net Collection Rate, Avg Days to Pay, Total Paid, Total Allowed
   - Top Denial Reasons
   - Denials by Payer
2) **Denials Deep Dive**
   - Denials by reason/category
   - Denials by payer + provider + location
   - Appeals/resubmissions outcomes (if modeled)
3) **A/R & Cashflow**
   - A/R aging buckets
   - Time to payment distribution
   - Paid trend over time
4) **Payer Mix & Performance**
   - Payer mix (allowed vs paid)
   - Net collection rate by payer
   - High-impact payer/denial combinations

---

## Core metrics (definitions)

- **Denial Rate** = Denied Claims / Total Submitted Claims
- **Net Collection Rate** = Total Paid / Total Allowed
- **Avg Days to Pay** = Avg(Payment Date - Service Date)
- **A/R Aging** = Days outstanding grouped into buckets (0–30, 31–60, 61–90, 91–120, 121+)

Full field definitions are in `data-dictionary`.

---

## Repo contents

- `/data_dictionary.md` : field definitions and grain
- `/powerbi/measures.md` : DAX measures and logic
- `/screenshots/` : dashboard preview images
- `/deliverables/` : executive summary + PDF export
- `/docs/assumptions_limitations.md` : responsible use + limitations
- `/docs/walkthrough_script.md` : a short script for demos / Loom walkthrough

---

## Responsible use + limitations
This dashboard supports **operational prioritization**, not clinical judgment.
- Patterns do not imply fault or misconduct
- Synthetic/public data may not reflect a specific organization’s policies/contracts
- Results should be validated against source systems when used in real settings

See `/docs/assumptions_limitations.md`.

---

## Contact
Christopher Fontes  
[GitHub](https://github.com/ovochris56)
[LinkedIn](https://www.linkedin.com/in/christopher-fontes/)

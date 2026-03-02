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

## Responsible use + limitations
This dashboard supports **operational prioritization**, not clinical judgment.
- Patterns do not imply fault or misconduct
- Synthetic/public data may not reflect a specific organization’s policies/contracts
- Results should be validated against source systems when used in real settings

---

📊 In-Depth Analysis & Actionable Insights

Analysis of the revenue cycle performance data indicates that financial outcomes are being driven less by claim volume and more by operational workflow efficiency across the billing lifecycle. With approximately $27.45M billed and $14.97M collected (54.5% collection rate) alongside a 16.8% denial rate across 8,394 denied claims, there is clear evidence of revenue friction occurring prior to reimbursement realization. Denials are heavily concentrated among a small subset of payers, with Medicaid, UnitedHealthcare, and Blue Cross Blue Shield accounting for the largest share of rejected claims, suggesting payer-specific administrative or documentation challenges rather than uniform systemic failure. At the same time, denial categories are dominated by coding, eligibility, and authorization issues, which are largely controllable front-end processes rather than downstream payer adjudication factors. This indicates that improvements in intake verification, documentation completeness, and coding accuracy could reduce denial incidence more effectively than expanding back-end appeals capacity alone.

Outcome analysis further reveals that a majority of denied claims are not appealed, while a substantial portion remains pending, highlighting potential inefficiencies in denial management prioritization and follow-up workflows. This creates a risk of preventable revenue leakage, particularly if claims with high reimbursement potential are not systematically escalated. Variability in monthly resubmission volumes suggests reactive operational behavior rather than a stabilized denial prevention strategy, which may contribute to workload spikes and delayed cash realization. Additionally, A/R aging patterns imply that older claims are accumulating in higher aging buckets, increasing the probability of write-offs and administrative cost per dollar recovered.

From an operational standpoint, the highest-impact interventions would likely include implementing real-time eligibility verification tools at registration, strengthening coding education and audit feedback loops, and developing payer-specific denial dashboards to identify recurring root causes. Establishing automated rules for appeal prioritization based on claim value and denial reason could improve recovery rates while controlling labor costs. Organizations may also benefit from predictive modeling to flag high-risk claims prior to submission, enabling proactive correction rather than reactive resubmission. Overall, the analysis suggests that targeted process optimization, particularly at the front end of the revenue cycle, offers the greatest opportunity to improve net collections, reduce administrative burden, and accelerate cash flow without requiring increased claim volume.

Recommended Operational Actions
-   	Implement front-end eligibility verification automation
-		Strengthen coding audit and feedback programs
-		Develop payer-specific denial monitoring dashboards
-		Prioritize appeals based on financial value and probability of recovery
-		Introduce predictive flags for high-risk claims before submission
-		Standardize denial follow-up workflows to reduce variability
-		Focus A/R reduction efforts on the highest aging buckets first
-- Denials table (simplified)
CREATE TABLE dbo.Denials (
    DenialID        nvarchar(50) NOT NULL PRIMARY KEY,
    ClaimID         nvarchar(50) NOT NULL,
    DenialDate      date         NOT NULL,
    DenialCategory  nvarchar(50) NOT NULL,
    DenialReason    nvarchar(50) NULL,
    AppealedFlag    bit          NOT NULL,
    ResubmittedFlag bit          NOT NULL,
    Outcome         nvarchar(50) NOT NULL
);

-- 

SQL Snippets

-- View: Denials by payer (total claims, denied claims, and denial rate)
CREATE VIEW dbo.v_Denials_By_Payer AS
SELECT
    c.PayerCanonical,
    COUNT(DISTINCT c.ClaimID) AS TotalClaims,
    COUNT(DISTINCT d.ClaimID) AS DeniedClaims,
    CAST(COUNT(DISTINCT d.ClaimID) AS FLOAT) 
        / NULLIF(COUNT(DISTINCT c.ClaimID), 0) AS DenialRate
FROM dbo.Claims c
LEFT JOIN dbo.Denials d
    ON d.ClaimID = c.ClaimID
GROUP BY c.PayerCanonical;

---

## Contact
Christopher Fontes  
[GitHub](https://github.com/ovochris56)
[LinkedIn](https://www.linkedin.com/in/christopher-fontes/)

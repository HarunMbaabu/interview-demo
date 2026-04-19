# Slide 1 — Title + Objective
**MoPhones Credit Portfolio Review (2025)**

Objective: Assess portfolio health, quantify credit–experience tradeoffs, and define actions to improve repayment while protecting customer trust.

---

# Slide 2 — Business Context
- MoPhones funds smartphone access via installment credit.
- Value driver = scale + repayment discipline + low credit losses.
- Strategic tension: stricter collections can improve cash recovery but harm NPS and long-term retention/referrals.

---

# Slide 3 — Data Overview
- Credit snapshots combined: **50,714 account-snapshot records** across 4 snapshot files.
- NPS survey responses: **4,129**.
- Matched credit↔NPS on latest snapshot: **3,574 linked accounts**.

---

# Slide 4 — Key Assumptions
- `DATE` used as snapshot date.
- Default proxy = `days_past_due >= 90` OR status in {FPD, FMD, PAR 30, Write Off}.
- Requested DOB/income fields were not present in provided extracts.
- `CUSTOMER_AGE` interpreted as **account age in days**; used as proxy segmentation.

---

# Slide 5 — Portfolio Metrics Overview
**Selected executive KPIs**
1. PAR30+ rate
2. Default rate
3. Repayment rate (`total_paid / total_due_today`)
4. Average DPD
5. Active:Closed account ratio

Why these: jointly capture risk incidence, loss pressure, cash performance, and book quality mix.

---

# Slide 6 — Trends Over Time (2025)
- PAR30+: **35.4% → 39.0%** (Jan to Sep snapshots)
- Default: **35.3% → 39.2%**
- Repayment rate: **75.3% → 71.5%**
- Avg DPD: **71.9 → 119.2 days**
- Active:Closed ratio: **0.97 → 0.56**

**Message:** Portfolio deterioration is persistent, not episodic.

---

# Slide 7 — Segment Risk Insight
Latest snapshot (2025-09-30) by account-age proxy:
- **12m+ accounts:** default **52.8%**
- 6–12m: **44.3%**
- 3–6m: **28.7%**
- 0–3m: **11.0%**

**High-risk segment:** 12m+ accounts with severe late-stage delinquency concentration.

---

# Slide 8 — Credit vs NPS Insight
Matched sample:
- Current/near-current (DPD < 30): average NPS **7.06**
- Delinquent (DPD ≥ 30): average NPS **5.20**

**Insight:** Credit stress and customer dissatisfaction move together; repayment friction is visible in sentiment.

---

# Slide 9 — Key Tension Identified
- Harder collections can protect short-term recoveries.
- But sustained delinquency pressure is paired with lower NPS, risking churn and weaker referrals.

**Executive implication:** optimize for **lifetime portfolio quality**, not only monthly recoveries.

---

# Slide 10 — Recommendations (1–2 Strong Actions)
1. **Two-lane collections strategy**
   - <30 DPD: digital reminders, self-serve promise-to-pay, light restructuring.
   - 30+ DPD: risk-tiered agent escalation for high expected recovery cohorts.
2. **Credit policy refresh for mature-book risk**
   - Tighten affordability/approval and repricing triggers for profiles over-indexing in 12m+ delinquency.

---

# Slide 11 — Data Limitations
- Missing DOB, income, and contract duration in available extracts (blocks requested age/income bands).
- No payment transaction-level table (limits consistency/cure analytics).
- Status definitions are not fully standardized across status fields.

---

# Slide 12 — Final Takeaway
MoPhones is showing worsening credit health through 2025, and delinquency is strongly associated with poorer customer experience.

**What to do now (next 90 days):**
- Act on segmented collections + underwriting recalibration.
- Upgrade data foundations (payment-level fact table + standardized status dictionary).

Outcome target: lower PAR/default trajectory **without sacrificing customer trust**.

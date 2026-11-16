# INTERNATIONAL CYBERSECURITY AND DIGITAL FORENSICS ACADEMY

## GRC103 | Module 4 Risk Monitoring and Reporting | Lab 2

**Full Name:** Venesha Adhiambo Ochieng  
**Registration Number:** C11/26/CGRCE/17566

**Email Address:** c11.cgrce2617566@icdfa.edu.ng  
**Cohort / Batch:** Cohort11

**Date Submitted:** 16th November 2026

## Task 1 Build the Monitoring Dashboard

Each rate = numerator ÷ denominator (shown to 1 decimal place), classified on unrounded values; N/A with an explanation if a denominator is zero (none was). Thresholds: coverage Green ≥98%, Amber ≥95%; timely review ≥95% / ≥85%; restore 100% / ≥90%; overdue ≤10% / ≤20% (lower is better); unauthorised changes 0 / 1–2 / ≥3. **March: all five indicators Red.**

| **Indicator** | **Jan** | **Feb** | **Mar** |
|--------------|---------|---------|---------|
| Monitoring coverage | 98.0% | 95.0% | 90.0% |
| Timely alert review | 95.0% | 80.0% | 70.0% |
| Restore success | 100.0% | 90.0% | 80.0% |
| Overdue high-risk actions | 10.0% | 25.0% | 40.0% |
| Unauthorised changes (count) | 1 | 3 | 5 |

![Task 1](Task%201.png)

Counts (unauthorised changes 1, 3, 5) are charted separately in the spreadsheet so percentages and counts are not mixed. Live formulas are in the workbook.

## Task 2 Interpret the Results

### 1. Monitoring blind spots

Coverage **98.0% → 95.0% → 90.0% (108 of 120)**; **12 endpoints unmonitored** (Jan 2, Feb 5).

*Consequence:* activity on those hosts raises no alert.

*Possible cause (unverified):* new endpoints added without enrolment.

### 2. Late alert review

Timely review **95.0% → 80.0% → 70.0% (28 of 40)**; **12 critical alerts** missed 24 hours; alerts doubled **20 → 40**.

*Consequence:* a real incident could be contained late.

*Possible cause (unverified):* capacity or noisy rules.

Alerts are not all incidents.

### 3. Restore failures

Success **100% → 90.0% → 80.0% (8 of 10)**.

*Consequence:* recovery after ransomware or failure may not work.

*Cause:* not yet diagnosed.

### Why the count misleads

Monitored endpoints rose **95 → 108 (+13)** but eligible endpoints rose **100 → 120 (+20)**, so the gap grew **5 → 12** and coverage fell.

Judge coverage by the rate and the gap.

### Also Red

- Overdue actions **40.0% (6 of 15)**
- Unauthorised changes **5 (up from 1)**

They rose as coverage fell; correlation is not proof of cause.

---

# Task 3 Update the Risk Register

| ID | Asset / Process | Risk Statement | March Evidence | L×I = Score | Owner | Review |
|----|----------------|----------------|----------------|------------|--------|--------|
| **R1** | Endpoint monitoring (Wazuh agent coverage) | If eligible endpoints are not actively monitored, malicious activity or unauthorised changes on them may go undetected, delaying response and weakening assurance. | Coverage 90.0% (108/120), Red; gap of 12 endpoints (Jan 2, Feb 5). Eligible endpoints +20 vs monitored +13 since Feb. Unauthorised changes 5 (Red). | **4×4 = 16 High** | Endpoint Security Manager | RD + 30 days |
| **R2** | Critical alert triage (SOC review process) | If critical alerts are not reviewed within 24 hours, genuine incidents may be contained late, increasing damage and recovery cost. | Timely review 70.0% (28/40), Red; 12 critical alerts missed the 24h target (Jan 1, Feb 6). Alert volume doubled from 20 to 40. | **4×4 = 16 High** | SOC / Security Operations Manager | RD + 30 days |
| **R3** | Backup and restoration process | If backups cannot be restored reliably, the business may be unable to recover data or services within needed timeframes after an incident or failure. | Restore success 80.0% (8/10), Red; 2 failed tests (Jan 0, Feb 1). Trend 100% > 90% > 80%. | **3×5 = 15 High** | IT Operations / Backup Manager | RD + 30 days |
| **R4** | Risk treatment action tracking | If high-risk treatment actions stay overdue, known risks remain untreated and management cannot rely on the risk register. | Overdue rate 40.0% (6/15), Red; 6 overdue (Jan 1, Feb 3). Due actions rose 10 > 12 > 15. | **4×3 = 12 High** | GRC Manager | RD + 30 days |

**Ratings:** R1 L4 (gap widening, 12 unmonitored now) × I4 (blind spots hide intrusions). R2 L4 (30% of critical alerts already late) × I4. R3 L3 (8 of 10 restores still pass) × I5 (failed recovery is the most severe outcome). R4 L4 (overdue doubled) × I3 (indirect harm).

**All High, so all escalated to the Head of Operations; Red indicators go to their owners within 1 working day.**

---

# Task 4 Prepare an Action and Assurance Plan

| Risk | Owner | Short-term Containment | Longer-term Improvement | Outcome Test for Closure |
|--------|--------|----------------------|------------------------|--------------------------|
| **R1** | Endpoint Security Manager | **By 5 WD of RD (23 Nov 2026):** Reconcile asset inventory with Wazuh, identify the 12 unmonitored endpoints, enrol them or restrict network access until enrolled. | **By 60 days of RD (15 Jan 2027):** Automate onboarding so new endpoints cannot join the network without an agent; weekly inventory-to-monitoring reconciliation. | Reconciliation report shows every eligible endpoint with a verified recent agent heartbeat; next month-end coverage ≥98% (≥118 of 120). Closure also needs a test event from a sampled enrolled endpoint appearing in the console. |
| **R2** | SOC / Security Operations Manager | **By 1 WD of RD (17 Nov 2026):** Review all critical alerts older than 24h and record outcomes; for 30 days add a temporary triage rota. | **By 60 days of RD (15 Jan 2027):** Tune or retire noisy rules, agree capacity or automation for the doubled alert volume, document an escalation path for ageing alerts. | Next month-end timely review ≥95%, and an audit of a sample of 10 closed critical alerts confirms the review was real, not just a status change. |
| **R3** | IT Operations / Backup Manager | **By 3 WD of RD (19 Nov 2026):** Diagnose the 2 failed restores, fix the cause and re-run both tests. | **By 45 days of RD (31 Dec 2026):** Define restore objectives (RTO/RPO), widen test scope to critical systems, and document the restore runbook. | Both failed restores re-run successfully with data integrity verified by a second person; next month-end restore success 10/10 (100%). |
| **R4** | GRC Manager | **By 5 WD of RD (23 Nov 2026):** Confirm owner and revised date for each of the 6 overdue actions; escalate any that cannot be met. | **By 60 days of RD (15 Jan 2027):** Add automated due-date reminders and a rule that actions 14 days overdue go to the Head of Operations. | Next month-end overdue rate ≤10%, and no high-risk action more than 30 days overdue. Closure is evidence that the risk is reduced, not just that a ticket was closed. |

---

# Task 5 Write the Management Report

**To:** Head of Operations  
**From:** GRC Analyst, Northbridge Services  
**Period:** March  
**Data:** fictional; three monthly observations cannot establish a reliable long-term trend or forecast.

## March status: all five indicators are Red

| Indicator | Jan | Feb | Mar |
|-----------|-----|-----|-----|
| Monitoring coverage | 98.0% | 95.0% | 90.0% |
| Timely alert review | 95.0% | 80.0% | 70.0% |
| Restore success | 100.0% | 90.0% | 80.0% |
| Overdue high-risk actions | 10.0% | 25.0% | 40.0% |
| Unauthorised changes (count) | 1 | 3 | 5 |

![Task 5](Task%205.png)

Unauthorised changes are counts and are not plotted on the percentage chart. Statuses use unrounded values against classroom thresholds.

## Decisions and Resources Requested

- **Approve** a temporary 30-day triage rota for critical alerts (R2).
- **Approve** endpoint onboarding effort, and agree that unenrolled endpoints may be network-restricted until monitored (R1).
- **Endorse** a restore re-test window and the widened test scope (R3).
- **Mandate** a rule that high-risk actions 14 days overdue come to you (R4).

## Three Priority Concerns

### 1. Monitoring blind spots

Coverage fell **98.0% → 95.0% → 90.0% (108 of 120)**. **12 endpoints are unmonitored** (Jan 2, Feb 5); about 10 more must be enrolled to reach the **98% Green level (118).**

*Consequence:* intrusions or unauthorised changes on those hosts would raise no alert.

*Observation:* eligible endpoints rose by 20 but monitored only by 13, so the monitored count rose while the rate fell.

*Possible cause (unverified):* new endpoints added without onboarding.

### 2. Late alert review

Timely review fell **95.0% → 80.0% → 70.0% (28 of 40)**; **12 critical alerts** missed the 24-hour target. Alert volume doubled (**20 → 40**).

*Consequence:* a real incident could be contained late.

*Possible cause (unverified):* review capacity did not keep pace with volume or noisy rules.

Alerts are not all incidents, and “not reviewed in 24h” does not mean never reviewed.

### 3. Restore failures

Success fell **100% → 90.0% → 80.0% (8 of 10 tests).**

*Consequence:* recovery from ransomware or failure may not work when needed.

*Possible cause:* not yet diagnosed.

Also Red: overdue actions **40.0% (6 of 15, risk R4)** and unauthorised changes **(5, up from 1)**. These rose as coverage fell, but correlation does not prove causation.

## Owners and Next Review

**R1** Endpoint Security Manager  
**R2** SOC Manager  
**R3** IT Operations/Backup Manager  
**R4** GRC Manager

Red indicators are escalated to these owners within 1 working day; all four risks score High (**R1 16, R2 16, R3 15, R4 12**). Actions are proposed, not complete (see action plan).

**Next review:** RD + 30 days (16 Dec 2026) using the next month-end figures as a fresh reporting period; interim check on containment actions at RD + 5 WD (23 Nov 2026).

Success means:
- Coverage ≥98%
- Timely review ≥95%
- Restore 10/10
- Overdue ≤10%

**Excel workbook:**  
<https://icdfaacademy-my.sharepoint.com/:x:/g/personal/c11_cgrce2617566_icdfa_edu_ng/IQDI5bpIF1ToRZSxdHLWFlkFAcTaR-eEWGFUqkqA_s_F9i4?e=MVNOKX>

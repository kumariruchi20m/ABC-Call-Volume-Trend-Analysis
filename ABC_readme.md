# 📞 Inbound Call Volume Trend & Manpower Capacity Planning
### Customer Experience (CX) Analytics Case Study — ABC Insurance

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Excel](https://img.shields.io/badge/Microsoft_Excel-Office_365-217346?logo=microsoft-excel&logoColor=white)](https://www.microsoft.com/excel)
[![Status](https://img.shields.io/badge/Status-Completed-success)](#)

An analytical customer experience (CX) and workforce management study analyzing **117,989 inbound calls** over a 23-day period for **ABC Insurance Company**. This project evaluates hourly volume trends, caller handling durations, and builds an optimized capacity model to reduce call abandonment from **~30% down to under 10%** across both day and night shifts.

---

## 📌 Table of Contents
* [Executive Summary](#-executive-summary)
* [Dataset Hygiene & Overview](#-dataset-hygiene--overview)
* [Hourly Trend Analysis](#-hourly-trend-analysis)
  * [Task 1: Call Duration Distribution](#task-1-call-duration-distribution)
  * [Task 2: Call Volume & Traffic Distribution](#task-2-call-volume--traffic-distribution)
* [Workforce & Manpower Planning](#-workforce--manpower-planning)
  * [Productivity Baseline & Assumptions](#productivity-baseline--assumptions)
  * [Task 3: Day Shift Sizing (9:00 AM – 9:00 PM)](#task-3-day-shift-sizing-900-am--900-pm)
  * [Task 4: 24/7 Night Shift Sizing (9:00 PM – 9:00 AM)](#task-4-247-night-shift-sizing-900-pm--900-am)
  * [Total Headcount Summary](#total-headcount-summary)
* [Key Business Insights & Recommendations](#-key-business-insights--recommendations)
* [Repository Layout](#-repository-layout)
* [Tools & Methodology](#-tools--methodology)

---

## 🚀 Executive Summary

* **Total Calls Evaluated:** 117,988 logged interactions over 23 days (~5,130 calls/day during operating hours).
* **Current Operational Performance:**
  * **Answered:** 70% (~3,585 calls/day)
  * **Abandoned:** 29% (~1,496 calls/day)
  * **Transferred:** 1% (~49 calls/day)
* **Average Call Duration:** 198.62 seconds (~3.31 minutes).
* **Peak Call Volume Window:** 10:00 AM – 1:00 PM (accounting for over 34% of total daily calls).
* **Target Objective:** Lower abandonment rate from **~30% to $\le 10\%$** (requiring an answered rate $\ge 90\%$).
* **Staffing Conclusion:**
  * **Day Shift (9 AM – 9 PM):** Requires **57 on-seat agents**
  * **Night Shift (9 PM – 9 AM):** Requires **17 on-seat agents**
  * **Total Minimum On-Floor Requirement:** **74 agents** for 24/7 coverage.

---

## 🗂 Dataset Hygiene & Overview

The underlying dataset contains operational telemetry for inbound calls:

| Parameter | Value | Notes |
| :--- | :--- | :--- |
| **Total Rows** | 117,989 | Inbound caller records |
| **Total Columns** | 13 | Including timestamp, status, agent ID, duration, and queue time |
| **Operational Window** | 23 Days | Full operational cycle |
| **Blank Cells** | 47,877 | Due to unassigned queues and dropped calls |
| **Missing Agent Data** | 34,198 `#N/A` | Corresponding directly to dropped/abandoned calls prior to agent pickup |

---

## 📈 Hourly Trend Analysis

### Task 1: Call Duration Distribution
Evaluated the average duration (in seconds) of answered calls across each 1-hour operating window:

| Time Bucket | Average Call Seconds (s) | Duration (Minutes) |
| :--- | :---: | :---: |
| **09:00 – 10:00** | 199.07 | 3.32 min |
| **10:00 – 11:00** | 203.33 | 3.39 min |
| **11:00 – 12:00** | 199.26 | 3.32 min |
| **12:00 – 13:00** | 192.89 | 3.21 min |
| **13:00 – 14:00** | 194.74 | 3.25 min |
| **14:00 – 15:00** | 193.68 | 3.23 min |
| **15:00 – 16:00** | 198.89 | 3.31 min |
| **16:00 – 17:00** | 200.87 | 3.35 min |
| **17:00 – 18:00** | 200.25 | 3.34 min |
| **18:00 – 19:00** | 202.55 | 3.38 min |
| **19:00 – 20:00** | 203.41 | 3.39 min |
| **20:00 – 21:00** | 202.85 | 3.38 min |
| **Grand Total Average** | **198.62** | **3.31 min** |

*Observation: Call duration remains remarkably stable across the entire 12-hour span, fluctuating within a narrow band between 192.89s and 203.41s.*

---

### Task 2: Call Volume & Traffic Distribution
Aggregated incoming call arrivals across queue timestamps:

| Time Bucket | Incoming Call Count | Share of Daytime Traffic |
| :--- | :---: | :---: |
| **09:00 – 10:00** | 9,588 | 8.1% |
| **10:00 – 11:00** | 13,313 | 11.3% |
| **11:00 – 12:00** *(Peak)* | **14,626** | **12.4%** |
| **12:00 – 13:00** | 12,652 | 10.7% |
| **13:00 – 14:00** | 11,561 | 9.8% |
| **14:00 – 15:00** | 10,561 | 9.0% |
| **15:00 – 16:00** | 9,159 | 7.8% |
| **16:00 – 17:00** | 8,788 | 7.4% |
| **17:00 – 18:00** | 8,534 | 7.2% |
| **18:00 – 19:00** | 7,238 | 6.1% |
| **19:00 – 20:00** | 6,463 | 5.5% |
| **20:00 – 21:00** | 5,505 | 4.7% |
| **Total Inbound Calls** | **117,988** | **100.0%** |

*Observation: Demand is front-loaded; call traffic peaks before noon and gradually declines toward the evening.*

---

## 👥 Workforce & Manpower Planning

### Productivity Baseline & Assumptions
* **Working Hours per Shift:** 9.0 hours total
* **Breaks & Lunch:** 1.5 hours $\rightarrow$ **7.5 net logged hours**
* **Agent Occupancy / Effective Talk Time:** 60% of logged time
  $$\text{Productive Talk Time per Agent} = 7.5\text{ hrs} \times 0.60 = 4.5\text{ hours/day}$$
* **Monthly Schedule:** 6 work days/week, 4 unplanned leaves/month (30-day base).

---

### Task 3: Day Shift Sizing (9:00 AM – 9:00 PM)
* Current daily incoming calls: **5,130 calls/day**
* Target service level: Answer $\ge 90\%$ ($5,130 \times 0.90 = 4,617\text{ calls}$)
* Total agent talk time needed:
  $$\text{Hours Needed} = \frac{5,130 \times 198.62\text{ s} \times 0.90}{3,600\text{ s/hr}} = 254.73\text{ productive hours}$$
* On-seat agent headcount:
  $$\text{Agents Required} = \frac{254.73\text{ hrs}}{4.5\text{ hrs/agent}} = 56.6 \rightarrow \mathbf{57\text{ agents}}$$

---

### Task 4: 24/7 Night Shift Sizing (9:00 PM – 9:00 AM)
* Expected night volume: 30 calls per 100 daytime calls (30% ratio)
  $$\text{Night Call Volume} = 5,130 \times 0.30 = 1,539\text{ calls/night}$$
* Total agent talk time needed to achieve $\ge 90\%$ answer rate:
  $$\text{Hours Needed} = \frac{1,539 \times 198.62\text{ s} \times 0.90}{3,600\text{ s/hr}} \approx 76.4\text{ productive hours}$$
* On-seat agent headcount:
  $$\text{Agents Required} = \frac{76.4\text{ hrs}}{4.5\text{ hrs/agent}} = 16.9 \rightarrow \mathbf{17\text{ agents}}$$

---

### Total Headcount Summary

| Shift Window | Daily Inbound Volume | Productive Hours Needed | Recommended On-Seat Staffing |
| :--- | :---: | :---: | :---: |
| **Day Shift (9 AM – 9 PM)** | 5,130 calls | 254.73 hrs | **57 Agents** |
| **Night Shift (9 PM – 9 AM)** | 1,539 calls | 76.00 hrs | **17 Agents** |
| **Combined 24/7 Floor Sizing** | **6,669 calls** | **330.73 hrs** | **74 Agents** |

> **Workforce Management (WFM) Note:** 74 represents the **on-seat (net)** requirement. To account for scheduled weekly offs (6-day work weeks) and unplanned shrinkage (~4 leaves/month), the **rostered (gross) headcount** should incorporate an additional ~20–25% buffer (~89–93 total agents on payroll).

---

## 💡 Key Business Insights & Recommendations

1. **Staggered Shift Scheduling:** 34.4% of total daytime calls occur between 10:00 AM and 1:00 PM. Allocating fixed 57 agents uniformly creates overstaffing in the evening (8–9 PM has only 5,505 calls) and understaffing during midday peak hours. Introducing split or staggered shifts (e.g., 10 AM – 7 PM) will balance occupancy.
2. **Automated Call-Backs & Intelligent Routing:** Since ~29% of calls are currently abandoned, introducing an automated Interactive Voice Response (IVR) queue callback feature when estimated wait times exceed 90 seconds will retain customer satisfaction without overburdening agents.
3. **Night Support Launch:** Operating 17 agents overnight eliminates the current 100% after-hours drop-off, providing continuous claim reporting support for insurance policyholders.

---

## 📁 Repository Layout

```text
├── README.md                          # Project overview & executive summary
├── data/
│   ├── raw/                           # Raw inbound logs (anonymized)
│   └── processed/
│       ├── hourly_call_duration.csv   # Aggregated duration by time bucket
│       └── hourly_call_volume.csv     # Call volume distribution
├── models/
│   └── manpower_capacity_model.xlsx   # Excel workbook containing pivot models & formulas
├── reports/
│   └── cx_manpower_presentation.pdf   # Slide deck / visual report
└── LICENSE                            # MIT License
```

---

## 🛠 Tools & Methodology
* **Software:** Microsoft Excel (Office 365)
* **Techniques:** Pivot Tables, Data Aggregation, Capacity Modeling, Descriptive Statistics, Workforce Sizing Calculations.

---

## 📜 License
This project is open-source and available under the [MIT License](LICENSE).
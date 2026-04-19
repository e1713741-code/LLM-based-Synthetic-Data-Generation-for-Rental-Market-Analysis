# LLM-based-Synthetic-Data-Generation-for-Rental-Market-Analysis
# RA Work Log — 19 April 2026

**Project:** LLM-Based Synthetic Data Generation for Rental Market Analysis
**Supervisor:**  Prof. Bingsheng He
**Affiliation:** NUS School of Computing

---

## Task Background

Following the project meeting on 9 April, I conducted a data quality audit on the Singapore CCR (Core Central Region) condominium rental price dataset. The objective was to assess the distribution of real versus linearly interpolated data points across the time series, establishing a quantitative baseline for the next phase of data imputation optimization — transitioning from linear interpolation to LLM-based generation.

---

## Dataset Overview

| Metric | Value |
|--------|-------|
| Condo Projects | 961 |
| Monthly Timesteps | 315 (Nov 1999 – Jan 2026) |
| Feature Columns | 346 |
| Source | URA (Urban Redevelopment Authority) |
| Region | CCR (Core Central Region) |

Each timestep file contains one row per project with geographic coordinates, macroeconomic indicators, amenity features, rental price, and a `y_mask` validity label.

> **Labeling convention:** `y_mask=1` → real rental price; `y_mask=0` with `rent>0` → linearly interpolated (invalid); `y_mask=0` with `rent=0` → no data.

---

## Task 1 — Projects with Data Emerging After 2021

**Definition:** Identify projects that have real data (`y_mask=1`) from 2021 onward, but either had no real data before 2021, or had a gap of more than 24 months between their last real entry and January 2021.

### Result: **75 projects** met the criteria

- **61 projects** had zero real rental records before 2021, with first real data points appearing between 2022 and 2025
- **14 projects** had real records before 2021 but with extended gaps exceeding 24 months (ranging from 35 to 216 months)
- Most extreme case: **TANJONG PAGAR CONSERVATION AREA** — last real record in April 2003, a gap of 216 months (18 years), with data not reappearing until May 2024

---

## Task 2 — Projects That Disappeared After 2021

**Definition:** Identify projects with real rental records before 2021 that experienced 60+ consecutive months (5 years) without any real data after 2021.

### Result: **69 projects** completely vanished post-2021

- All **69 projects** had exactly zero real data points after January 2021 — none showed even occasional valid records
- Last real records for these projects ranged from **2006 to 2020**
- Representative cases: QUEEN ASTRID PARK (last record Mar 2017), PARK HOUSE (Jan 2019), MONTCLAIR @ WHITLEY (Aug 2020)

---

## Task 3 — Data Quality Breakdown for Task 1 Projects

**Definition:** For the 75 projects identified in Task 1, count data points with `y_mask=1` (real price) vs. `rent>0` with `y_mask=0` (interpolated price) across all 315 timesteps.

### Result: 75 projects × 315 timesteps = **23,625 total data points**

| Category | Count | Percentage |
|----------|------:|:----------:|
| ✅ Real price (`y_mask=1`) | 1,225 | 5.2% |
| ⚠️ Interpolated (`rent>0`, `y_mask=0`) | 3,346 | 14.2% |
| ❌ No data (`rent=0`, `y_mask=0`) | 19,054 | 80.7% |

```
Real ██░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░  5.2%
Interp ██████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ 14.2%
No data ████████████████████████████████████████░░ 80.7%
```

**Key findings:**
- These projects are extremely data-sparse: on average only **16.3 real data points** per project (1,225 ÷ 75), covering roughly 5% of timesteps
- Highest interpolation density: **CROWN CENTRE** — 285/315 timesteps interpolated (90.5%), with only 9 real data points
- Interpolated data outnumbers real data by a factor of **2.7×** within this subset

---

## Deliverables

| File | Description |
|------|-------------|
| `analysis_v2.py` | Complete analysis script — data ingestion, restructuring, all 3 tasks, CSV export |
| `task1_results.csv` | 75 projects — emerging data after 2021 |
| `task2_results.csv` | 69 projects — disappeared after 2021 |
| `task3_results.csv` | 75 projects — real vs. interpolated breakdown |

---

## Technical Approach

- Read and restructured **315 timestep CSV files** using Python and Pandas, transforming the data from a per-timestep layout into a per-project time series view suitable for longitudinal analysis
- Classified data validity using combined conditions on the `y_mask` and `rent_per_sqft` fields to distinguish real, interpolated, and missing data
- Implemented a **consecutive-gap scanner** across each project's time series to detect maximum durations of missing real data, enabling identification of emerging and disappearing projects

---

## Next Steps

→ Await feedback from Cici on whether the statistical results and task definitions align with expectations

→ Use these statistics as a quantitative baseline for the next phase: optimizing data imputation from linear interpolation to LLM-based synthetic generation

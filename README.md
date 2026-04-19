# LLM-based-Synthetic-Data-Generation-for-Rental-Market-Analysis
# RA Work Log

## Date
19 April 2026

## Project
LLM-Based Synthetic Data Generation for Rental Market Analysis

## Task Background
Following the project meeting on 9 April, I conducted a data quality audit on the Singapore CCR (Core Central Region) condominium rental price dataset. The goal was to assess the distribution of real vs. linearly interpolated data across the time series, providing a baseline for subsequent data imputation optimization.

## Dataset Overview
- Source: URA (Urban Redevelopment Authority) private residential rental data, preprocessed and split by monthly timesteps
- Temporal coverage: November 1999 to January 2026, totaling 315 monthly timestep files
- Spatial scope: CCR (Core Central Region), covering 961 condominium projects
- Each timestep file contains 961 rows (one per project) × 346 feature columns (geographic, macroeconomic indicators, amenity features, rental price, and y_mask label)
- Labeling convention: y_mask=1 indicates real rental price; y_mask=0 indicates linearly interpolated or missing data

## Completed Tasks

### Task 1: Identify Projects with Data Emerging After 2021
**Definition**: Projects that have real data (y_mask=1) from 2021 onward, but either had no real data before 2021, or had a gap of more than 24 months between their last real data entry and January 2021.

**Results**: 75 projects met the criteria.
- 61 projects had zero real rental records before 2021, with first real data points appearing between 2022 and 2025
- 14 projects had real records before 2021 but with extended gaps exceeding 24 months (ranging from 35 to 216 months)
- Most extreme case: TANJONG PAGAR CONSERVATION AREA — last real record in April 2003, a gap of 216 months (18 years), with real data not reappearing until May 2024

### Task 2: Identify Projects That Disappeared After 2021
**Definition**: Projects that had real rental records before 2021, but experienced 60 or more consecutive months (5 years) without any real data after 2021.

**Results**: 69 projects met the criteria.
- All 69 projects had zero real data points after 2021 (total_valid_after_2021 = 0), meaning they completely vanished from the dataset
- The last real records for these projects ranged from 2006 to 2020
- Representative cases: QUEEN ASTRID PARK (last record March 2017), PARK HOUSE (last record January 2019), MONTCLAIR @ WHITLEY (last record August 2020)

### Task 3: Data Quality Breakdown for Task 1 Projects
**Definition**: For the 75 projects identified in Task 1, count the number of data points with y_mask=1 (real price) vs. rent>0 with y_mask=0 (interpolated price).

**Results**: 75 projects × 315 timesteps = 23,625 total data points
- Real price (y_mask=1): 1,225 (5.2%)
- Interpolated price (rent>0, y_mask=0): 3,346 (14.2%)
- No data (rent=0, y_mask=0): 19,054 (80.7%)
- These projects are extremely data-sparse: on average, each project has only 16.3 real data points (1,225 ÷ 75), covering roughly 5% of the 315 timesteps
- Highest interpolation density: CROWN CENTRE — 285 out of 315 timesteps are interpolated (90.5%), with only 9 real data points

## Deliverables
- `analysis_v2.py`: Complete analysis script covering data ingestion, restructuring, all three statistical tasks, and CSV export
- `task1_results.csv`: Detailed results for Task 1 (75 projects)
- `task2_results.csv`: Detailed results for Task 2 (69 projects)
- `task3_results.csv`: Detailed results for Task 3 (75 projects)

## Technical Approach
- Read and restructured 315 timestep CSV files using Python and Pandas, transforming the data from a per-timestep layout into a per-project time series view for analysis
- Classified data validity based on combined conditions of the y_mask field and rent_per_sqft field
- Scanned each project's time series for consecutive missing-data segments to compute maximum gap durations

## Next Steps
- Await feedback from Cici on whether the results align with expectations
- Use these statistics as a baseline reference for the next phase: optimizing data imputation (from linear interpolation to LLM-based generation)

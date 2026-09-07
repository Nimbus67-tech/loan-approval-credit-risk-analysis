# Loan Approval & Credit Risk Analysis
 
**Final Data Analytics Capstone Project**
**Author:** Yogesh Kumar Mourya
 
---
 
## Project Overview
 
This project applies end-to-end data analytics skills — data cleaning, exploratory data analysis, visualization, and interactive dashboarding — to a Finance/Banking dataset of loan applications. The goal is to understand what drives loan approval decisions and loan default risk, and to turn those findings into actionable business recommendations.
 
## Problem Statement
 
Lending institutions need to balance two competing goals: approving enough loans to generate revenue, while minimizing the risk of default. This project analyzes a loan applications dataset to answer:
- What factors are most strongly associated with loan default?
- Are approval decisions consistent with actual risk levels?
- Which loan purposes, regions, or applicant profiles represent the best and worst risk-adjusted opportunities?
## Dataset Description
 
- **File:** `data/loan_applications_raw.csv` (raw) / `data/loan_applications_cleaned.csv` (cleaned)
- **Size:** 3,215 raw records (3,200 after cleaning), 16 columns
- **Domain:** Finance / Banking — loan applications
- **Fields:** applicant demographics (age, gender, marital status, education, employment type), financials (annual income, credit score, existing loans), loan details (amount, term, purpose), application metadata (region, date), and outcomes (approval status, default flag)
- Full field-by-field definitions: see [`data/data_dictionary.md`](data/data_dictionary.md)
## Tools Used
 
- **Python** (pandas, numpy) — data cleaning and analysis
- **Jupyter Notebook** — EDA workflow and documentation
- **Matplotlib / Seaborn** — static visualizations
- **Power BI Desktop** — interactive dashboard
- **Git & GitHub** — version control and project hosting
## Data Cleaning Process
 
Performed in [`notebooks/loan_analysis_EDA.ipynb`](notebooks/loan_analysis_EDA.ipynb):
1. Removed 15 exact duplicate rows
2. Standardized inconsistent categorical text (e.g. `"male"`, `"M"`, `"Male"` → `Male`)
3. Corrected impossible values (negative ages, a 999-month loan term) by converting to missing, then imputing
4. Imputed missing values — median for numeric fields, mode for categorical fields
5. Preserved `default_flag` as structurally missing for rejected applications (a rejected loan can't default)
6. Corrected data types (dates, integers)
## Exploratory Data Analysis (EDA)
 
Full analysis in the same notebook. Key steps: descriptive statistics, a correlation matrix across numeric fields, IQR-based outlier detection on income and loan amount, and breakdown of approval/default rates by purpose, region, and credit band.
 
**Headline finding:** annual income and loan amount are strongly correlated (r ≈ 0.89), but credit score — not income — is the strongest predictor of default.
 
## Visualizations
 
Six charts in [`visuals/`](visuals/):
1. Distribution of Loan Amounts
2. Default Rate by Credit Score Band
3. Approval Rate by Loan Purpose
4. Correlation Heatmap
5. Annual Income vs Default Status (boxplot)
6. Approval Rate by Region (bonus)
## Power BI Dashboard
 
Interactive dashboard in [`Dashboard/`](Dashboard/) (`loan_dashboard.pbix`), built on the cleaned dataset. Includes:
- **3 KPI cards:** Total Applications, Approval Rate, Default Rate
- **4 visuals:** Approval Rate by Loan Purpose, Applications Over Time, Applications by Region, Default Rate by Credit Band (matrix)
- **4 slicers:** Region, Loan Purpose, Credit Band, Approval Status
See a static preview: [`dashboard/dashboard_screenshot.png`](Dashboard/dashboard_screenshot.png)
 
## Key Insights
 
1. Credit score is the strongest predictor of default risk — far more than income (default rate falls from 16.4% in "Poor" credit to 7.1% in "Excellent").
2. The bank's overall approval rate (~41%) is conservative relative to its actual risk exposure.
3. Loan purpose meaningfully affects approval odds: Business (43.3%) and Debt Consolidation (42.4%) approve most; Personal loans (37.2%) approve least.
4. Income and loan amount are tightly coupled (r ≈ 0.89), concentrating risk among high-income outlier applicants.
5. Regional approval rates are broadly balanced — geography isn't a major risk driver in this dataset.
Full write-up: [`business_insights.md`](business_insights)
 
## Business Recommendations
 
1. **Shift underwriting weight toward credit score over income** for "Good" or better bands, to responsibly expand approval volume without materially increasing default risk.
2. **Re-evaluate Personal loan underwriting criteria** — its lower approval rate isn't clearly justified by higher risk in this dataset, suggesting qualified applicants may be getting filtered out unnecessarily.
## Conclusion
 
This analysis shows that credit score, not income, should anchor loan risk decisions, and that current approval patterns by loan purpose may not be fully risk-justified. The accompanying Power BI dashboard makes these patterns explorable in real time, and the two recommendations above are directly actionable using metrics already tracked on the dashboard (Approval Rate, Default Rate), making it straightforward to monitor the impact of any policy changes going forward.
 
---
 
## Repository Structure
 
```
├── data/
│   ├── loan_applications_raw.csv
│   ├── loan_applications_cleaned.csv
│   └── data_dictionary.md
├── notebooks/
│   └── loan_analysis_EDA.ipynb
├── visuals/
│   └── chart1-6_*.png
├── dashboard/
│   ├── loan_dashboard.pbix
│   └── dashboard_screenshot.png
├── business_insights.md
└── README.md
```

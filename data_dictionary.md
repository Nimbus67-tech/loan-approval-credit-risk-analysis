# Data Dictionary — Loan Applications Dataset

**File:** `loan_applications_raw.csv`
**Rows:** 3,215 (includes 15 intentional duplicate rows)
**Domain:** Finance / Banking — Loan Approval & Credit Risk

| Column | Type | Description | Known Data Issues |
|---|---|---|---|
| application_id | string | Unique loan application ID (e.g. LN100670) | None |
| age | int | Applicant age in years | 3 records have an invalid value (-1) |
| gender | string | Applicant gender | Inconsistent casing/format: "Male", "male", "M", etc. |
| marital_status | string | Single / Married / Divorced / Widowed | ~1.5% missing |
| education | string | Graduate / Not Graduate / Post Graduate | None |
| employment_type | string | Salaried / Self-Employed / Business Owner | ~8% missing; inconsistent casing + trailing space ("Salaried ") |
| annual_income | float | Applicant's annual income (currency units) | ~3% missing; contains genuine high-income outliers |
| credit_score | int | Credit score (300–850 scale) | ~2% missing |
| existing_loans_count | int | Number of existing loans held | None |
| loan_amount | float | Requested loan amount | None |
| loan_term_months | int | Loan term in months | 3 records have an invalid value (999) |
| loan_purpose | string | Home Improvement / Debt Consolidation / Auto / Education / Medical / Business / Personal | None |
| region | string | North / South / East / West / Central | ~1% missing |
| application_date | date | Date the application was submitted (2023–2024) | None |
| approval_status | string | Approved / Rejected | None |
| default_flag | float (0/1/NaN) | Whether an approved loan later defaulted; NaN for rejected applications (not applicable) | Intentionally NaN for all rejected loans |

## Known Data Quality Issues to Address in Task 3 (Data Prep)
1. **Missing values** in `marital_status`, `employment_type`, `annual_income`, `credit_score`, `region`.
2. **Duplicate rows** — 15 exact duplicates injected.
3. **Inconsistent categorical formatting** — `gender` and `employment_type` have mixed casing and stray whitespace.
4. **Invalid/impossible values** — negative `age`, and a `loan_term_months` value of 999.
5. **Outliers** — a small number of very high `annual_income` values (up to ~₹950,000) representing legitimate but extreme high-net-worth applicants — worth flagging in EDA (Task 4), not necessarily removing.
6. **Structural note** — `default_flag` is only meaningful for `approval_status == "Approved"`; rejected applications never had a loan disbursed, so default risk doesn't apply to them.

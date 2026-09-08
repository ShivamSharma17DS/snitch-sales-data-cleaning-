# Retail Sales Data Cleaning (Snitch Dataset)

## Overview
A data cleaning project tackling a genuinely messy retail sales dataset 
with multiple compounding data quality issues — inconsistent naming, 
impossible numeric values, and extensive missing data — resolved through 
systematic investigation rather than blind fixes.

## Dataset
- 2,500 retail sales records
- Columns: City, Segment, Product Category, Units Sold, Unit Price, 
  Discount %, Sales Amount, Profit
- Multiple columns with 50%+ missing values

## Key Data Quality Findings

### 1. City Naming Inconsistencies
Found the same cities represented multiple ways due to case differences 
and spelling errors — e.g., "Bangalore," "bengaluru," and "Banglore" all 
referring to the same city; "Hyderabad," "Hyd," and "hyderbad" for 
another. Standardized casing first, then merged spelling variants using 
a mapping dictionary. Required two verification passes to catch a 
variant missed on the first pass — a reminder that cleaning is 
iterative, not one-shot.

### 2. Impossible Discount Values
Discovered `Discount_%` values exceeding 100% (up to 130%) — a logical 
impossibility. Investigated the distribution of invalid values before 
deciding on a fix: converted invalid values to null rather than 
arbitrarily capping them, preserving honesty about what was actually 
unknown. Documented that this pushed overall missingness in the column 
to 74%, severely limiting its reliability for analysis.

### 3. Negative Units Sold
Found 283 rows with negative `Units_Sold`. Tested the hypothesis that 
these represented product returns by checking whether `Profit` was 
correspondingly negative — only 27% were, disproving the returns theory 
and confirming these were data entry/generation errors rather than 
meaningful signals. Nulled and mean-imputed accordingly.

### 4. Negative Sales Amounts
Applied the same null-and-impute approach to 70 rows with negative 
`Sales_Amount`, after confirming these were inconsistent with any valid 
business scenario.

## Tools Used
Python, pandas

## Key Skills Demonstrated
- Iterative cleaning (catching missed inconsistencies on re-verification)
- Hypothesis testing before assuming a cause (returns vs. data error)
- Transparent handling of high-missingness columns rather than 
  disguising the problem
- Correct use of `.fillna()` vs. direct assignment (avoiding accidental 
  column overwrites)

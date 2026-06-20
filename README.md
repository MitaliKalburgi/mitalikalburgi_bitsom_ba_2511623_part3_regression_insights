# Part 3: Regression-Based Business Insights & Model Interpretation

## Business Problem Summary
Leadership wants a clearer read on what's actually moving monthly sales across stores before committing budget to any specific lever — marketing, inventory, staffing, discounting, or store/region focus. Rather than guessing or going on anecdote, this analysis uses regression to check which factors show a real, measurable relationship with monthly sales, and how strong that relationship is. The end goal is a recommendation leadership can act on, with the usual caveat that regression shows association, not proof of cause.

## Task 1: Understanding the Dataset

Dataset: `data/business_regression_data.xlsx`, sheet `store_performance` — 320 rows of monthly store-level data, one row per store per month (4 months of data across multiple stores). A `data_dictionary` sheet is included in the same file with column definitions.

### Dependent Variable
- **monthly_sales** — the figure we're trying to explain.

### Independent Variables Considered
- marketing_spend
- footfall
- avg_discount_pct
- staff_count
- inventory_availability_pct
- competitor_distance_km
- holiday_flag
- customer_rating
- region (categorical)
- store_type (categorical)

### Numerical Variables
marketing_spend, footfall, avg_discount_pct, staff_count, inventory_availability_pct, competitor_distance_km, customer_rating, monthly_sales, monthly_profit.

holiday_flag is stored as 0/1 but functions as a category flag rather than a true continuous number.

### Categorical Variables
- **region**: East, North, South, West
- **store_type**: Mall, High Street, Residential, Airport

### Variables Needing Cleaning/Transformation
- **competitor_distance_km** — 6 rows missing this value. Needs a decision on how to handle before regression (row removal vs. imputation — documented in the cleaned data sheet).
- **customer_rating** — 8 rows missing this value. Same treatment needed.
- **region** and **store_type** — both text categories, not usable directly in a regression equation. Converted to dummy (0/1) variables in Task 3.

### Variables Not Useful for This Regression
- **store_id** — identifier only, no business meaning as a predictor.
- **month** — only 4 months of data here, not enough to draw a reliable trend/seasonality conclusion, so it's left out of the regression rather than forced in.
- **monthly_profit** — this is a downstream outcome of sales, not a driver of it. Including it as a predictor of monthly_sales would be circular logic, so it's excluded from the independent variable list.

### Missing Value Treatment (Cleaned Data sheet)
- **competitor_distance_km**: 6 missing values. Distribution is right-skewed with two clear outlier stores (~19km and ~22km from nearest competitor), so mean would overstate a "typical" value. Missing values filled with the **median (3.365)** instead.
- **customer_rating**: 8 missing values. Distribution is symmetric with no outliers (mean ≈ median ≈ 3.9), so missing values filled with the **mean (3.92)**.
- Supporting calculations (mean, median, std dev, min/max, and box plots used to make this decision) are kept on the **Cleaned Data** sheet, columns P–R, for reference.

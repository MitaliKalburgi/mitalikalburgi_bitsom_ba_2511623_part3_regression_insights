# Part 3: Regression-Based Business Insights & Model Interpretation

## Business Problem Summary
Leadership wants a clearer read on what's actually moving monthly sales across stores before committing budget to any specific lever — marketing, inventory, staffing, discounting, or store/region focus. Rather than guessing or going on anecdote, this analysis uses regression to check which factors show a real, measurable relationship with monthly sales, and how strong that relationship is. The end goal is a recommendation leadership can act on, with the usual caveat that regression shows association, not proof of cause.

## Dataset Description
Dataset: `data/business_regression_data.xlsx`, sheet `store_performance` — 320 rows of monthly store-level data, one row per store per month (4 months of data, January–April 2025, across multiple stores). A `data_dictionary` sheet is included in the same file with column definitions.

### Dependent Variable
- **monthly_sales** — the figure we're trying to explain.

### Independent Variables Considered
marketing_spend, footfall, avg_discount_pct, staff_count, inventory_availability_pct, competitor_distance_km, holiday_flag, customer_rating, region (categorical), store_type (categorical)

### Numerical Variables
marketing_spend, footfall, avg_discount_pct, staff_count, inventory_availability_pct, competitor_distance_km, customer_rating, monthly_sales, monthly_profit. (holiday_flag is stored as 0/1 but functions as a category flag rather than a true continuous number.)

### Categorical Variables
- **region**: East, North, South, West
- **store_type**: Mall, High Street, Residential, Airport

### Variables Needing Cleaning/Transformation
- **competitor_distance_km** — 6 rows missing this value.
- **customer_rating** — 8 rows missing this value.
- **region** and **store_type** — text categories, converted to dummy (0/1) variables before regression.

### Variables Not Useful for This Regression
- **store_id** — identifier only, no business meaning as a predictor.
- **month** — only 4 months of data, not enough to draw a reliable trend/seasonality conclusion, so left out of the regression.
- **monthly_profit** — a downstream outcome of sales, not a driver of it; including it as a predictor would be circular logic.

### Missing Value Treatment
- **competitor_distance_km**: Distribution is right-skewed with two clear outlier stores (~19km and ~22km from nearest competitor), so mean would overstate a "typical" value. Filled with the **median (3.365)** instead.
- **customer_rating**: Distribution is symmetric with no outliers (mean ≈ median ≈ 3.9). Filled with the **mean (3.92)**.
- Supporting calculations (mean, median, std dev, min/max, box plots) are kept on the **Cleaned Dataset** sheet for reference.

## Dummy Variable Approach
**region** and **store_type** each had 4 categories, so each was converted into 3 dummy (0/1) columns rather than 4, to avoid the dummy variable trap (perfect redundancy). One category per variable was left out as the reference:
- **region** — reference category: **East**
- **store_type** — reference category: **Mall**

Full explanation and formula logic is in `outputs/model_equations.md`.

## Regression Approach
Two stages of regression were used:
1. **Simple linear regression** — four individual numerical variables (marketing_spend, footfall, avg_discount_pct, inventory_availability_pct) tested against monthly_sales one at a time, to understand each factor's standalone relationship with sales.
2. **Multiple linear regression** — the variables that showed real signal (footfall, marketing_spend, inventory_availability_pct, avg_discount_pct) combined with dummy-encoded store_type, to capture how multiple business factors act together rather than in isolation.

All regressions were run using Excel's Data Analysis ToolPak, with residuals captured for further analysis.

## Model Comparison Summary
Five models were compared: four simple regressions and one multiple regression. The multiple regression model substantially outperformed every simple model, explaining 82.1% of the variation in monthly sales (R² = 0.821) compared to footfall's 73.6% as the next-best single predictor. Marketing spend, footfall, and inventory availability were consistently significant across models; average discount percentage was never statistically significant. Full comparison details are in `analysis/model_comparison.md` and `outputs/regression_summary.xlsx`.

## Final Model Selected
The **multiple regression model** was selected, using footfall, marketing_spend, avg_discount_pct, and inventory_availability_pct, plus store_type (dummy-encoded), as predictors of monthly_sales. It was chosen because it explains substantially more sales variation than any single-variable model and better reflects how multiple business factors influence sales simultaneously in a real retail environment. Full equation and coefficient breakdown is in `outputs/model_equations.md`.

## Business Recommendation
Leadership should prioritize initiatives that increase footfall and maintain strong inventory availability, with marketing spend as a smaller but genuine supporting lever. No reliable sales benefit was found from discounting in this analysis, so discounting strategy should not be expanded purely to drive sales volume. Residential stores and West region performance show notable unexplained variability (per residual analysis) and warrant closer operational review. Full recommendation and reasoning is in `outputs/final_recommendation.md`.

## Assumptions and Limitations
- Missing values were imputed (median for competitor_distance_km, mean for customer_rating) rather than removing rows, based on each variable's distribution.
- The dataset covers only 4 months per store, limiting confidence in any seasonal or trend-based conclusions.
- Regression models show statistical association, not proof of causation.
- The multiple regression model explains 82% of sales variation; the remaining 18% reflects factors not captured in this dataset.
- Region was not included in the final regression model (store_type was used instead), though residual analysis suggested region-level patterns (West region) may be worth a separate, closer look.

## Screenshots Included
- `screenshots/simple_regression_output.png` — simple regression output (Footfall vs Monthly Sales)
- `screenshots/multiple_regression_output.png` — multiple regression output (combined model)
- `screenshots/residuals_preview.png` — predicted values and residuals table
- `screenshots/model_comparison_preview.png` — model comparison table
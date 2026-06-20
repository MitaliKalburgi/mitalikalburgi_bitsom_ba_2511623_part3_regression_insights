# Model Equations & Variable Documentation

## Dummy Variable Approach

Two categorical variables required dummy encoding before they could be used in regression: **region** and **store_type**. Both had 4 categories each, so each was converted into 3 dummy (0/1) columns rather than 4 — using all 4 would create perfect redundancy (the dummy variable trap), since if a row is 0 across three categories, the fourth is already implied. One category per variable was deliberately left out to serve as the **reference category**, and every dummy coefficient in the regression is interpreted relative to that baseline.

### Region (reference category: East)
| Dummy column | = 1 when region is... |
|---|---|
| dummy_region_north | North |
| dummy_region_south | South |
| dummy_region_west | West |

A row with all three columns equal to 0 represents **East** — the reference region. East was chosen as the reference simply as a baseline convention; it carries no special statistical significance, and the choice doesn't affect model fit or significance, only how the coefficients read.

### Store Type (reference category: Mall)
| Dummy column | = 1 when store_type is... |
|---|---|
| dummy_store_type_HighStreet | High Street |
| dummy_store_type_Residential | Residential |
| dummy_store_type_Airport | Airport |

A row with all three columns equal to 0 represents **Mall** — the reference store type, chosen as a baseline for the same reason as above.

### Formula logic used (Excel)
Each dummy column uses a simple conditional check against the original category column, e.g.:
=IF(region_cell="North",1,0)
=IF(store_type_cell="High Street",1,0)

The formula was entered once in the first data row, then filled down across all 320 records (Excel automatically adjusts the row reference for each row as it fills).

## Simple Regression Equations

**1. Marketing Spend → Monthly Sales**

**monthly_sales = 560,777.35 + 2.13 × marketing_spend**

For every additional rupee spent on marketing, predicted monthly sales increase by about ₹2.13, holding nothing else constant. R² = 0.167, meaning marketing spend alone explains about 17% of the variation in sales across stores. Statistically significant (p < 0.001).

**2. Footfall → Monthly Sales**

**monthly_sales = 446,410.58 + 35.68 × footfall**

Each additional visitor is associated with about ₹35.68 more in monthly sales. R² = 0.736 — by far the strongest single predictor in this dataset. Statistically significant (p < 0.001).

**3. Average Discount % → Monthly Sales**

**monthly_sales = 697,835.63 − 138,730.45 × avg_discount_pct**

The negative coefficient suggests higher discounting is associated with lower sales, but this relationship is **not statistically significant** (p = 0.104), so it can't be relied upon as a real effect — it may simply be noise in this dataset.

**4. Inventory Availability % → Monthly Sales**

**monthly_sales = 484,814.26 + 2,217.83 × inventory_availability_pct**

Each one-point increase in inventory availability is associated with about ₹2,217.83 more in monthly sales. Statistically significant, though only just (p = 0.041), and explains very little variation alone (R² = 0.013).

## Multiple Regression Equation

**monthly_sales = 148,347.11**

. 1.17 × marketing_spend 
. 33.66 × footfall − 58,920.81 × avg_discount_pct
. 3,001.20 × inventory_availability_pct − 11,433.46 × dummy_store_type_HighStreet − 28,009.31 × dummy_store_type_Residential
. 10,472.25 × dummy_store_type_Airport

R² = 0.821 — this model explains about 82% of the variation in monthly sales across stores, a substantial improvement over any single-variable model.

## Explanation of Each Coefficient (Multiple Regression)

- **Intercept (148,347.11):** The baseline predicted monthly sales for a Mall store (the reference store type) when every other variable is zero. Not meaningful on its own in business terms — it's a mathematical anchor point, not a realistic store scenario.
- **marketing_spend (1.17, p < 0.001, significant):** Holding everything else constant, every extra rupee of marketing spend is associated with about ₹1.17 more in monthly sales. A real, modest, positive return.
- **footfall (33.66, p < 0.001, significant):** The strongest driver in the model. Each additional visitor is associated with about ₹33.66 more in monthly sales, holding other factors constant.
- **avg_discount_pct (−58,920.81, p = 0.110, not significant):** No reliable evidence that discounting increases or decreases sales once other factors are accounted for. The negative direction hints discounting doesn't drive volume the way it might be assumed to, but this isn't statistically confirmed.
- **inventory_availability_pct (3,001.20, p < 0.001, significant):** Each one-point increase in inventory availability is associated with about ₹3,001 more in monthly sales. Notably stronger and more reliable in this combined model than it appeared alone.
- **dummy_store_type_HighStreet (−11,433.46, p = 0.083, borderline not significant):** High Street stores show somewhat lower sales than Mall stores, but the evidence isn't quite strong enough to be confident this is a real difference.
- **dummy_store_type_Residential (−28,009.31, p < 0.001, significant):** Residential stores sell meaningfully less than Mall stores, holding other factors constant — the clearest, most confident store-type finding in this model.
- **dummy_store_type_Airport (10,472.25, p = 0.287, not significant):** Airport stores appear to sell more than Mall stores, but this isn't statistically reliable given the data available.

## Final Model Selected

The **multiple regression model** is selected as the final model for this analysis.

## Reason for Selecting the Final Model

The multiple regression model explains substantially more of the variation in monthly sales (R² = 0.821) than any individual simple regression model — more than double the next-best single predictor, footfall (R² = 0.736). It also captures how several real business levers (marketing spend, footfall, inventory availability, store type) act together rather than in isolation, which better reflects how a retail business actually operates: no single factor drives sales alone. This makes the multiple regression model the most useful and realistic basis for a business recommendation, while the simple regression models remain useful for understanding each factor's standalone relationship with sales.
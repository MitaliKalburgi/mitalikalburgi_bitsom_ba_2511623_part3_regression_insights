# Model Comparison

This document compares all regression models built for this analysis: four simple regressions (one variable at a time) and one multiple regression (combined predictors).

## Model 1: Marketing Spend → Monthly Sales
- **Variables:** Dependent: monthly_sales | Independent: marketing_spend
- **R-squared:** 0.167 (marketing_spend alone explains ~16.7% of sales variation)
- **Significant variables:** marketing_spend (p = 2.48E-14, highly significant)
- **Business usefulness:** Confirms marketing spend has a real, positive effect on sales, but on its own it's a weak predictor — not enough to plan budget decisions around in isolation.
- **Limitations:** Ignores every other factor influencing sales (footfall, inventory, store type, etc.), so it overstates how much marketing spend alone "explains" sales performance.

## Model 2: Footfall → Monthly Sales
- **Variables:** Dependent: monthly_sales | Independent: footfall
- **R-squared:** 0.736 (footfall alone explains ~73.6% of sales variation)
- **Significant variables:** footfall (p = 4.75E-94, highly significant)
- **Business usefulness:** By far the strongest single-variable model. Footfall is clearly the dominant driver of sales on its own, which is a genuinely useful, actionable insight.
- **Limitations:** Doesn't explain *why* footfall varies store to store, and doesn't capture how marketing, inventory, or store type might also matter alongside footfall.

## Model 3: Average Discount % → Monthly Sales
- **Variables:** Dependent: monthly_sales | Independent: avg_discount_pct
- **R-squared:** 0.008 (essentially no explanatory power alone)
- **Significant variables:** None — avg_discount_pct is not statistically significant (p = 0.104)
- **Business usefulness:** No evidence from this model that discounting drives sales. The coefficient is even negative, hinting discounting may coincide with weaker-performing stores rather than causing stronger sales — but this can't be confirmed with the data available.
- **Limitations:** A non-significant result doesn't prove discounting has zero effect — it may interact with other variables, or its effect may be too small to detect on its own.

## Model 4: Inventory Availability % → Monthly Sales
- **Variables:** Dependent: monthly_sales | Independent: inventory_availability_pct
- **R-squared:** 0.013 (very weak alone)
- **Significant variables:** inventory_availability_pct (p = 0.041, just barely significant)
- **Business usefulness:** Weak evidence alone, but the relationship is technically real and positive — worth testing further in combination with other variables, which we did in Model 5.
- **Limitations:** Such low R-squared means this model is not reliable for prediction or decision-making on its own.

## Model 5: Multiple Regression (Combined Model)
- **Variables:** Dependent: monthly_sales | Independent: footfall, marketing_spend, avg_discount_pct, inventory_availability_pct, dummy_store_type_HighStreet, dummy_store_type_Residential, dummy_store_type_Airport
- **R-squared:** 0.821 (the combined model explains ~82.1% of sales variation — substantially stronger than any single-variable model)
- **Significant variables:** footfall (p = 1.12E-102), marketing_spend (p = 1.36E-17), inventory_availability_pct (p = 4.72E-10), dummy_store_type_Residential (p = 4.43E-05)
- **Not significant:** avg_discount_pct (p = 0.110), dummy_store_type_HighStreet (p = 0.083, borderline), dummy_store_type_Airport (p = 0.287)
- **Business usefulness:** This is the most complete and useful model for decision-making. It confirms footfall and marketing spend as real drivers, reveals that inventory availability matters more than it appeared alone, and shows Residential stores significantly underperform Mall stores (the reference category) even after accounting for other factors.
- **Limitations:** Discounting still shows no proven effect on sales even combined with other variables. High Street and Airport store types don't show a statistically confident difference from Mall stores — the data isn't conclusive enough to act on those specific comparisons. As with all regression here, this shows association, not proof of causation.

## Overall Comparison Summary
| Model | R-squared | Verdict |
|---|---|---|
| Marketing Spend (simple) | 0.167 | Weak alone, but real effect |
| Footfall (simple) | 0.736 | Strong single predictor |
| Avg Discount % (simple) | 0.008 | Not useful — not significant |
| Inventory Availability % (simple) | 0.013 | Weak alone, real but minor effect |
| **Multiple Regression (combined)** | **0.821** | **Best model — most explanatory power, most business-actionable** |

The multiple regression model is selected as the final model for this analysis, since it captures the combined, simultaneous effect of multiple real business levers and explains substantially more of the variation in sales than any single-variable model.
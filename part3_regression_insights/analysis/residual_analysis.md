# Residual Analysis — Multiple Regression Model

This analysis uses the final multiple regression model (footfall, marketing_spend, avg_discount_pct, inventory_availability_pct, and store_type dummies) to evaluate where the model's predictions diverge most from actual store performance.

## Method
Predicted monthly sales were calculated for all 320 store-month records using the multiple regression model. Residuals were calculated as:
**Residual = Actual Monthly Sales − Predicted Monthly Sales**

A positive residual means the store sold more than the model expected (under-prediction). A negative residual means the store sold less than the model expected (over-prediction).

## Top 5 Largest Positive Residuals (Model Under-Predicted)
| Store | Month | Region | Store Type | Actual | Predicted | Residual |
|---|---|---|---|---|---|---|
| STR-1030 | Feb-2025 | West | Residential | 820,519.04 | 714,619.59 | +105,899.45 |
| STR-1073 | Mar-2025 | East | Residential | 813,316.71 | 713,693.30 | +99,623.41 |
| STR-1032 | Jan-2025 | South | High Street | 914,544.17 | 815,772.73 | +98,771.44 |
| STR-1050 | Apr-2025 | North | Residential | 735,786.64 | 638,540.15 | +97,246.49 |
| STR-1028 | Apr-2025 | East | Mall | 713,611.16 | 618,465.84 | +95,145.32 |

## Top 5 Largest Negative Residuals (Model Over-Predicted)
| Store | Month | Region | Store Type | Actual | Predicted | Residual |
|---|---|---|---|---|---|---|
| STR-1017 | Mar-2025 | West | High Street | 685,379.08 | 844,620.31 | -159,241.23 |
| STR-1023 | Feb-2025 | South | Mall | 627,171.90 | 755,437.16 | -128,265.26 |
| STR-1012 | Jan-2025 | West | Residential | 595,467.60 | 716,546.49 | -121,078.89 |
| STR-1007 | Feb-2025 | West | Mall | 800,451.94 | 900,272.48 | -99,820.54 |
| STR-1009 | Jan-2025 | North | Residential | 641,865.03 | 740,315.35 | -98,450.32 |

## Business Interpretation

**Under-predicted stores (positive residuals):** These stores are outperforming what the model expects based on footfall, marketing spend, discounting, inventory availability, and store type alone. This suggests there's a real, positive factor driving their sales that isn't captured by the current model — possibly store-specific factors like local management quality, a particularly loyal customer base, a recent local event, or competitive dynamics not reflected in competitor_distance_km alone. From a business standpoint, these stores may be worth a closer qualitative look — there may be a replicable practice happening there that other stores could learn from.

**Over-predicted stores (negative residuals):** These stores are underperforming relative to what the model expects given their inputs. This could point to local execution issues, a temporary disruption (renovation, staffing gap, local competition), or simply that store-specific factors are working against them in ways the model can't see. These are reasonable candidates for a more detailed operational review.

## Pattern by Store Type and Region
Residential stores appear frequently in both the largest positive and largest negative residual lists, suggesting high variability within that store type — Residential performance seems to depend heavily on store-specific factors not captured by the model, more so than other store types.

The West region appears three times among the five largest negative residuals (STR-1017, STR-1012, STR-1007), which may suggest the model tends to over-predict for West region stores specifically. With only 5 data points in this list, this should be treated as a pattern worth monitoring rather than a confirmed conclusion — it would be worth re-checking once more months of data are available.

## Limitations
This residual analysis is based on only 4 months of data per store, which limits how confidently we can generalize "store type" or "region" patterns. Some of the largest residuals may simply reflect one unusual month for an otherwise typical store, rather than a persistent pattern. A longer time window would give a more reliable read on which stores or regions are consistently over- or under-performing relative to the model.
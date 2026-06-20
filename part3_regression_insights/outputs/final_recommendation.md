# Final Recommendation — Regression-Based Sales Insights

## Summary
This analysis examined what factors are most strongly associated with monthly store sales across the retail chain, using both simple and multiple regression models on 320 store-month records. The final multiple regression model explains about 82% of the variation in monthly sales (R² = 0.821), combining footfall, marketing spend, average discount percentage, inventory availability, and store type.

## 1. Factors Most Strongly Associated with Monthly Sales

- **Footfall** is the single strongest driver of sales, both alone (R² = 0.736) and within the combined model (coefficient = 33.66, p < 0.001). More visitors reliably means more sales.
- **Marketing spend** has a real, statistically significant positive relationship with sales (coefficient = 1.17, p < 0.001), though its standalone explanatory power is modest.
- **Inventory availability** showed a weak relationship alone but a clear, statistically significant one in the combined model (coefficient = 3,001.20, p < 0.001) — having products in stock matters more than it first appeared.
- **Store type** matters: Residential stores sell significantly less than Mall stores, holding other factors constant (coefficient = −28,009.31, p < 0.001) — the clearest store-type finding in the analysis.


## Residual Patterns Worth Flagging

Beyond the regression coefficients themselves, the residual analysis (see `analysis/residual_analysis.md`) surfaced two patterns leadership should be aware of:

- **Residential stores show high variability** — they appear frequently among both the largest under-predictions and largest over-predictions, suggesting sales at Residential stores depend heavily on store-specific factors (local management, neighborhood dynamics, nearby footfall sources) that aren't captured by the broad variables in this model. This is in addition to the direct regression finding that Residential stores sell significantly less than Mall stores on average.
- **West region stores appeared 3 of 5 times among the largest over-predictions** (the model expected more sales than these stores actually delivered). With only 5 data points in that list, this is a pattern worth monitoring rather than a confirmed regional effect — but it may be worth a closer look at West region operations specifically, especially since region itself wasn't included as a variable in the final regression model (store_type was used instead).


## 2. Variables Leadership Should Focus On

Leadership should prioritize **footfall-driving initiatives**, **marketing spend**, and **inventory availability**, since these three show consistent, statistically reliable relationships with sales across both simple and multiple regression models. Of these, footfall has by far the largest impact, so anything that reliably increases store visits (location strategy, local promotions, partnerships, store visibility) deserves serious attention. Leadership should also treat **Residential stores and West region performance** as areas for closer operational review — not because regression proved a strong relationship, but because residual analysis flagged unusual variability there that the model doesn't explain.

## 3. Variables That Should Not Be Over-Interpreted

- **Average discount percentage** showed no statistically significant relationship with sales in either the simple or multiple regression model (p = 0.104 and p = 0.110 respectively). The negative coefficient might suggest discounting doesn't drive volume the way it's sometimes assumed to — but this is not proven, and leadership should not change discounting strategy based on this analysis alone.
- **High Street and Airport store types** did not show statistically significant differences from Mall stores in the combined model (p = 0.083 and p = 0.287). Any "Airport stores sell more" narrative should not be treated as confirmed — the data isn't strong enough to support that conclusion confidently.

## 4. Recommended Business Action

Based on this analysis, the most defensible near-term action is to **prioritize investments that increase footfall and maintain strong inventory availability**, while treating marketing spend as a smaller but genuine lever. Discounting strategy should not be expanded purely to drive sales volume, since no reliable sales benefit was found in this data — if discounting continues, it should be justified on other grounds (clearing stock, customer loyalty, competitive necessity) rather than as a sales-growth lever.

Residential stores warrant a closer operational review, since they significantly underperform Mall stores even after accounting for marketing spend, footfall, and inventory — something specific to that store type or its typical locations may be holding sales back.

## 5. Risks and Limitations Leadership Should Keep in Mind

- This dataset covers only **4 months** of data per store — seasonal effects, one-off events, or short-term anomalies could be influencing results in ways a longer time window would reveal or rule out.
- The model explains 82% of sales variation, meaning **18% remains unexplained** — other factors (local competition, management quality, weather, regional economic conditions) are likely at play but aren't captured here.
- Residual analysis showed substantial store-to-store variation even within the same store type, especially Residential stores — meaning store-level execution may matter as much as the broad factors tested here.
- The avg_discount_pct and some store_type findings were not statistically significant — absence of evidence is not the same as evidence of no effect; a larger dataset might reveal relationships this analysis couldn't detect.

## 6. Why Regression Shows Association, Not Causation

Regression identifies statistical relationships between variables — it tells us that stores with higher footfall, marketing spend, or inventory availability *tend to* have higher sales, but it cannot prove that changing one of these factors *causes* sales to change. For example, it's possible that successful stores attract more footfall and justify more marketing spend, rather than (or in addition to) footfall and marketing spend causing the success. Confirming causation would require controlled experiments (e.g., increasing marketing spend at a sample of stores and comparing results to similar stores left unchanged) rather than just analyzing existing historical data. This recommendation should be treated as a strong, evidence-based starting point for decision-making, not a guarantee of results.
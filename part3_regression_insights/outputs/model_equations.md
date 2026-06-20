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
# Residual Analysis — Part 3: Regression Analysis

**Student:** Rohit Kadam
**Student ID:** 2511727
**Final Model Used:** MR1 — Multiple Linear Regression

---

## Residual Calculation Method

**Formula:**
```
Residual = Actual Monthly Sales − Predicted Monthly Sales (MR1)
```

- A **positive residual** means the model **under-predicted** — the store performed better than expected
- A **negative residual** means the model **over-predicted** — the store performed worse than expected
- Full predicted values and residuals for all 320 records are in `analysis/regression_workbook.xlsx` — sheet `predictions_residuals`

**Overall Residual Statistics:**
- Mean residual: 0.00 (expected for OLS regression)
- Standard deviation: 42,440.94
- Maximum residual: +111,365.91
- Minimum residual: -174,526.50

---

## Top 5 Records — Largest Positive Residuals (Model Under-Predicted)

| Rank | Store ID | Month | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|---|---|---|
| 1 | STR-1028 | Apr 2025 | East | Mall | 713,611.16 | 602,245.25 | +111,365.91 |
| 2 | STR-1026 | Apr 2025 | East | Mall | 625,514.04 | 518,426.74 | +107,087.30 |
| 3 | STR-1030 | Feb 2025 | West | Residential | 820,519.04 | 718,053.94 | +102,465.10 |
| 4 | STR-1051 | Feb 2025 | East | Airport | 787,715.51 | 685,998.16 | +101,717.35 |
| 5 | STR-1073 | Mar 2025 | East | Residential | 813,316.71 | 712,371.83 | +100,944.88 |

### Business Interpretation — Positive Residuals

These stores consistently outperformed what the model predicted based on their footfall, marketing spend, staff count, and other measured variables. The model does not fully capture whatever is driving their above-average performance.

Possible business reasons:
- These stores may have run local promotions or events not captured in the dataset
- They may benefit from stronger brand loyalty or repeat customer behaviour in their area
- STR-1028 and STR-1026 are both East region Mall stores in April — a local festival or seasonal event may have driven unusually high traffic that April
- STR-1030 is a West Residential store that outperformed despite Residential stores generally being lower-performing than Airport stores in the model

**Leadership should investigate** what these stores are doing differently — their practices may be worth replicating across similar store types.

---

## Top 5 Records — Largest Negative Residuals (Model Over-Predicted)

| Rank | Store ID | Month | Region | Store Type | Actual Sales | Predicted Sales | Residual |
|---|---|---|---|---|---|---|---|
| 1 | STR-1017 | Mar 2025 | West | High Street | 685,379.08 | 859,905.58 | -174,526.50 |
| 2 | STR-1012 | Jan 2025 | West | Residential | 595,467.60 | 727,161.43 | -131,693.83 |
| 3 | STR-1023 | Feb 2025 | South | Mall | 627,171.90 | 750,028.67 | -122,856.77 |
| 4 | STR-1007 | Feb 2025 | West | Mall | 800,451.94 | 911,326.53 | -110,874.59 |
| 5 | STR-1077 | Feb 2025 | South | Residential | 538,376.00 | 631,758.74 | -93,382.74 |

### Business Interpretation — Negative Residuals

These stores significantly underperformed what the model expected given their input variables. Despite having footfall, marketing spend, and staffing levels that should produce higher sales, their actual sales were much lower.

Possible business reasons:
- STR-1017 (West, High Street, Mar 2025) has the largest negative residual at -174,527. A local competitor opening, road closure, or operational disruption in March could explain this unexpected shortfall
- STR-1012 and STR-1077 are Residential stores underperforming in January and February — these may be affected by post-holiday spending slowdowns not captured in the holiday_flag variable (which only flags holiday months, not post-holiday contractions)
- STR-1023 and STR-1007 are Mall stores underperforming — possible local mall-level issues such as anchor tenant closures or mall renovation works

**Leadership should investigate** the root cause for each of these stores. The model predicted they should perform well — their underperformance signals a store-specific problem worth addressing.

---

## Discussion — Model Under-Prediction and Over-Prediction Patterns

**By Store Type (mean residual ~ 0 for all types):**
The model is well-calibrated across store types on average — no systematic bias by store type. However, the largest individual residuals (both positive and negative) are concentrated in Mall and Residential store types, suggesting higher variability in these formats that the model's dummy variables alone cannot fully capture.

**By Region (mean residual ~ 0 for all regions):**
No systematic regional over- or under-prediction on average. However, the largest negative residuals cluster in West region stores, and the largest positive residuals in East region stores — suggesting the West region may have more unexplained variability in certain months.

**Key Conclusion:**
The model does not systematically under- or over-predict any specific store type or region. The large residuals are driven by individual store-month events rather than a structural model bias. This indicates MR1 is reasonably well-specified, but store-level idiosyncratic factors (local events, competitor activity, operational disruptions) account for the remaining unexplained 16.73% of sales variation.

---

*Full residual data for all 320 records available in: analysis/regression_workbook.xlsx — sheet: predictions_residuals*
*Screenshot evidence: screenshots/residuals_preview.png*

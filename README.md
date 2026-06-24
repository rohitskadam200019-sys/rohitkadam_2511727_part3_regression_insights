# Part 3: Regression-Based Business Insights & Model Interpretation

**Student:** Rohit Kadam
**Student ID:** 2511727
**Repository:** rohitkadam_2511727_part3_regression_insights
**Tool Used:** Microsoft Excel

---

## Business Problem Summary

A retail chain leadership team wants to understand what factors are driving monthly sales performance across stores. They are considering business actions such as increasing marketing spend, improving inventory availability, changing discounting strategy, reallocating staff, and prioritizing certain store types or regions. Regression analysis is used to identify which factors appear most strongly associated with monthly sales.

---

## Dataset Description

| Property | Details |
|---|---|
| File | business_regression_data.xlsx |
| Total Records | 320 rows |
| Stores | 80 unique stores |
| Time Period | January 2025 – April 2025 (4 months) |
| Total Columns | 14 |

---

## Dependent and Independent Variables

### Dependent Variable

| Variable | Description |
|---|---|
| `monthly_sales` | Total monthly sales value per store. This is the outcome variable the regression models aim to explain. Range: 400,831 to 946,833. Mean: 680,629. |

### Potential Independent Variables

| Variable | Type | Description |
|---|---|---|
| `marketing_spend` | Numerical | Monthly marketing expenditure per store |
| `footfall` | Numerical | Number of customer visits per month |
| `avg_discount_pct` | Numerical | Average discount percentage applied |
| `staff_count` | Numerical | Number of staff in the store |
| `inventory_availability_pct` | Numerical | Percentage of inventory available |
| `competitor_distance_km` | Numerical | Distance to nearest competitor in km |
| `holiday_flag` | Binary (0/1) | Whether the month included a public holiday |
| `customer_rating` | Numerical | Average customer satisfaction rating |
| `region` | Categorical | Store region — East, North, South, West |
| `store_type` | Categorical | Store type — Airport, High Street, Mall, Residential |

### Numerical Variables

| Variable | Min | Max | Mean |
|---|---|---|---|
| `marketing_spend` | 9,534.65 | 172,415.52 | 56,279.47 |
| `footfall` | 971 | 12,870 | 6,564.77 |
| `avg_discount_pct` | 0.00 | 0.292 | 0.124 |
| `staff_count` | 5 | 31 | 16.49 |
| `inventory_availability_pct` | 71.0 | 99.0 | 88.29 |
| `competitor_distance_km` | 0.20 | 22.02 | 4.56 |
| `customer_rating` | 2.8 | 5.0 | 3.92 |
| `monthly_sales` | 400,831.65 | 946,833.54 | 680,628.72 |
| `monthly_profit` | 53,544.36 | 200,575.34 | 111,568.20 |

### Categorical Variables

| Variable | Categories |
|---|---|
| `region` | East, North, South, West |
| `store_type` | Airport, High Street, Mall, Residential |
| `store_id` | 80 unique store identifiers (STR-1001 to STR-1080) |

### Variables That May Need Cleaning or Transformation

| Variable | Issue | Action Required |
|---|---|---|
| `competitor_distance_km` | 6 missing values | Fill with median before regression |
| `customer_rating` | 8 missing values | Fill with median before regression |
| `region` | Categorical text — cannot be used directly in regression | Convert to dummy variables |
| `store_type` | Categorical text — cannot be used directly in regression | Convert to dummy variables |

### Variables That May Not Be Useful for Regression

| Variable | Reason |
|---|---|
| `store_id` | Unique identifier only — no predictive value |
| `month` | Only 4 unique values (Jan–Apr 2025) — insufficient time variation for meaningful time regression |
| `monthly_profit` | This is another outcome variable derived from sales — not an independent predictor of sales |
| `customer_rating` | Very low correlation with monthly_sales (r = -0.028, p = 0.622) — not statistically significant |

---

## Regression Approach

Three regression models were built and compared:

**Model SR1 — Simple Linear Regression (Footfall)**
- Dependent variable: monthly_sales
- Independent variable: footfall
- R-squared: 0.7363 — footfall alone explains 73.63% of sales variation
- Equation: monthly_sales = 446,410.58 + 35.678 × footfall

**Model SR2 — Simple Linear Regression (Marketing Spend)**
- Dependent variable: monthly_sales
- Independent variable: marketing_spend
- R-squared: 0.1672 — marketing spend alone explains 16.72% of sales variation
- Equation: monthly_sales = 560,777.35 + 2.130 × marketing_spend

**Model MR1 — Multiple Linear Regression (Full Model)**
- Dependent variable: monthly_sales
- Independent variables: footfall, marketing_spend, staff_count, inventory_availability_pct, holiday_flag + 6 dummy variables for region and store_type
- R-squared: 0.8327 — explains 83.27% of sales variation
- 9 out of 11 variables statistically significant (p < 0.05)

All regression outputs are documented in `analysis/regression_workbook.xlsx`.

---

## Dummy Variable Approach

Two categorical variables were converted to dummy variables for use in MR1:

**region** (4 categories → 3 dummies, reference = East):
- `region_North`, `region_South`, `region_West`

**store_type** (4 categories → 3 dummies, reference = Airport):
- `store_type_HighStreet`, `store_type_Mall`, `store_type_Residential`

The reference category (East for region, Airport for store_type) is dropped to avoid the dummy variable trap (perfect multicollinearity). All dummy coefficients are interpreted as the difference in monthly_sales relative to the reference category.

Full dummy variable explanation in `outputs/model_equations.md`.

---

## Model Comparison Summary

| Model | Variables | R-squared | Significant Variables | Recommended? |
|---|---|---|---|---|
| SR1 — Simple (Footfall) | footfall | 0.7363 | footfall (p < 0.0001) | Partial use |
| SR2 — Simple (Marketing) | marketing_spend | 0.1672 | marketing_spend (p < 0.0001) | Not alone |
| MR1 — Multiple (Full) | 11 variables + dummies | 0.8327 | 9 out of 11 (p < 0.05) | ✅ Yes |

Full comparison in `analysis/model_comparison.md` and `outputs/regression_summary.xlsx`.

---

## Final Model Selected

**MR1 — Multiple Linear Regression** is selected as the final model.

MR1 has the highest R-squared (83.27%), the most statistically significant variables (9/11), and provides the most complete picture for multi-factor business decisions. SR1 is a strong supplementary model for quick footfall-based estimates. SR2 is too weak to use independently.

---

## Business Recommendation

Based on MR1 regression evidence:

1. **Footfall is the strongest driver** — each additional visitor adds ₹28.14 in monthly sales. Invest in traffic-driving initiatives for low-footfall stores.
2. **Resolve inventory gaps** — each 1% improvement in inventory availability adds ₹3,081 per month. Fix stock-out issues immediately.
3. **Staff adequately** — each additional staff member adds ₹2,957 per month. Review staffing at underperforming high-footfall stores.
4. **Prepare for holiday months** — holiday months add ₹15,895 on average. Deploy a full playbook of staffing, inventory, and promotions.
5. **Prioritise Airport locations for expansion** — Residential stores underperform Airport stores by ₹39,891 per month.
6. **Investigate South and West regional outperformance** — replicate what drives their ₹20,000+ advantage over East region stores.

Do not over-interpret region_North (p = 0.28) or store_type_Mall (p = 0.31) — these are not statistically significant.

Full recommendation in `outputs/final_recommendation.md`.

---

## Assumptions and Limitations

### Assumptions
1. The relationship between each independent variable and monthly_sales is linear
2. Missing values in competitor_distance_km (6) and customer_rating (8) were filled with median — these records are treated as complete
3. The 4-month observation window is representative of typical store performance
4. Randomness in store-month observations is assumed — no systematic sampling bias
5. East region and Airport store type are appropriate reference categories for dummy variables

### Limitations
1. Only 4 months of data — seasonal peaks, festive seasons, and year-end effects are not captured
2. 16.73% of sales variation remains unexplained — missing variables include competitor pricing, local economic conditions, and promotional activity
3. Regression shows association, not causation — higher footfall may be a result of high sales (popular stores) rather than a cause
4. Coefficients are averages across all stores — individual store impacts will vary
5. customer_rating and avg_discount_pct showed weak or insignificant correlations and were excluded — their true business impact may require different data or analysis approaches

---

## Screenshots Included

| File | Shows |
|---|---|
| `screenshots/simple_regression_output.png` | Simple regression output — SR1 (footfall model) results |
| `screenshots/multiple_regression_output.png` | Multiple regression output — MR1 coefficient table with p-values |
| `screenshots/residuals_preview.png` | Predicted values and residuals for all 320 records |
| `screenshots/model_comparison_preview.png` | Model comparison table — SR1 vs SR2 vs MR1 |

---

## Repository Structure

```
part3_regression_insights/
├── data/
│   └── business_regression_data.xlsx
├── analysis/
│   ├── regression_workbook.xlsx
│   ├── model_comparison.md
│   └── residual_analysis.md
├── outputs/
│   ├── regression_summary.xlsx
│   ├── final_recommendation.md
│   └── model_equations.md
├── screenshots/
│   ├── simple_regression_output.png
│   ├── multiple_regression_output.png
│   ├── residuals_preview.png
│   └── model_comparison_preview.png
└── README.md
```

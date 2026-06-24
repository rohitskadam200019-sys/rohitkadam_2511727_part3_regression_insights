# Model Comparison — Part 3: Regression Analysis

**Student:** Rohit Kadam
**Student ID:** 2511727

---

## Model SR1: Simple Regression — Footfall

**Model Name:** SR1 — Simple Linear Regression (Footfall)

**Variables Used:**
- Dependent variable: monthly_sales
- Independent variable: footfall

**R-squared:** 0.7363
Footfall alone explains 73.63% of the variation in monthly sales. This is a strong result for a single-variable model.

**Significant Variables:**
- footfall — p-value < 0.0001 (highly significant)

**Business Usefulness:**
This model is highly useful for quick store-level sales estimates when only footfall data is available. It gives leadership a strong, reliable signal: stores with more visitors generate significantly more sales. Useful for prioritizing store traffic improvement initiatives.

**Limitations:**
- Ignores marketing spend, staff count, discounting, inventory, and store type
- Cannot explain why two stores with similar footfall have different sales
- Not suitable for multi-factor business decisions such as budget allocation across marketing and staffing

---

## Model SR2: Simple Regression — Marketing Spend

**Model Name:** SR2 — Simple Linear Regression (Marketing Spend)

**Variables Used:**
- Dependent variable: monthly_sales
- Independent variable: marketing_spend

**R-squared:** 0.1672
Marketing spend alone explains only 16.72% of the variation in monthly sales. Weak explanatory power on its own.

**Significant Variables:**
- marketing_spend — p-value < 0.0001 (statistically significant but weak predictor alone)

**Business Usefulness:**
Confirms that marketing spend has a positive relationship with sales (each ₹1 in marketing adds ~₹2.13 in sales). However, the low R-squared means marketing spend is only one small piece of the picture. Not suitable as a standalone model for sales forecasting or resource decisions.

**Limitations:**
- Explains less than 17% of sales variation
- Does not account for footfall, store type, region, staffing, or discounting
- A high marketing spend store may still underperform if located in a low-footfall area

---

## Model MR1: Multiple Regression — All Predictors

**Model Name:** MR1 — Multiple Linear Regression (Full Model)

**Variables Used:**
- Dependent variable: monthly_sales
- Independent variables: footfall, marketing_spend, staff_count, inventory_availability_pct, holiday_flag, region_North, region_South, region_West, store_type_HighStreet, store_type_Mall, store_type_Residential

**R-squared:** 0.8327
The full model explains 83.27% of the variation in monthly sales — the strongest of the three models.

**Significant Variables (p < 0.05):**
- footfall (p < 0.0001) — strongest driver
- marketing_spend (p < 0.0001)
- staff_count (p = 0.0183)
- inventory_availability_pct (p = 0.0162)
- holiday_flag (p = 0.0014)
- region_South (p = 0.0028)
- region_West (p = 0.0177)
- store_type_HighStreet (p = 0.0177)
- store_type_Residential (p < 0.0001)

**Variables Not Statistically Significant (p > 0.05):**
- region_North (p = 0.2766) — not significantly different from East
- store_type_Mall (p = 0.3056) — not significantly different from Airport

**Business Usefulness:**
This is the most complete and useful model for leadership decision-making. It captures the combined effect of operational factors (footfall, staff, inventory), marketing investment, seasonal effects (holidays), geographic differences (region), and store format differences (store type). It can inform decisions on staffing, marketing budget, store prioritization, and regional strategy simultaneously.

**Limitations:**
- Does not include competitor pricing or promotional activity
- Does not capture long-term trends or seasonality beyond the 4-month observation window
- region_North and store_type_Mall coefficients are not statistically reliable
- Regression shows association, not causation — higher marketing spend may reflect store size rather than marketing effectiveness

---

## Side-by-Side Comparison

| Item | SR1 | SR2 | MR1 |
|---|---|---|---|
| Model Type | Simple | Simple | Multiple |
| Dependent Variable | monthly_sales | monthly_sales | monthly_sales |
| Independent Variables | footfall | marketing_spend | 11 variables + dummies |
| R-squared | 0.7363 | 0.1672 | 0.8327 |
| Significant Variables | footfall | marketing_spend | 9 out of 11 |
| Best Use | Quick footfall-based estimate | Marketing ROI check | Full business decision support |
| Main Limitation | Single factor only | Very low explanatory power | Missing competitor and seasonal data |
| Recommended? | Partial use | No — too weak alone | ✅ Yes — best model |

---

## Final Model Selected

**MR1** is selected as the final model.

It has the highest R-squared (83.27%), the most significant variables, and provides the most complete picture for business decision-making. SR1 is a useful supplementary model for footfall-based quick estimates. SR2 is too weak to use independently.

# Final Recommendation — Part 3: Regression-Based Business Insights

**Student:** Rohit Kadam
**Student ID:** 2511727
**Based on:** MR1 — Multiple Linear Regression (R-squared = 0.8327)

---

## 1. Which Factors Appear Most Strongly Associated with Monthly Sales?

Based on the regression analysis of 320 store-month records across 80 stores, the following factors show the strongest and most statistically reliable association with monthly sales:

| Factor | Coefficient | P-value | Strength |
|---|---|---|---|
| Footfall | +28.14 per visitor | < 0.0001 | ★★★★★ Strongest |
| Marketing Spend | +1.17 per ₹1 spent | < 0.0001 | ★★★ Moderate |
| Store Type — Residential vs Airport | −39,891 | < 0.0001 | ★★★★ Strong |
| Region — South vs East | +21,231 | 0.0028 | ★★★ Significant |
| Region — West vs East | +20,222 | 0.0177 | ★★★ Significant |
| Holiday Month | +15,895 | 0.0014 | ★★★ Significant |
| Staff Count | +2,957 per staff member | 0.0183 | ★★ Moderate |
| Inventory Availability | +3,081 per 1% increase | 0.0162 | ★★ Moderate |

**Footfall is by far the strongest factor.** The simple regression model (SR1) showed footfall alone explains 73.63% of sales variation (R² = 0.7363). In the full multiple regression model (MR1), each additional visitor adds ₹28.14 in monthly sales after controlling for all other factors.

---

## 2. Which Variables Should Leadership Focus On?

Leadership should focus on the following variables where the regression evidence is strong (statistically significant, p < 0.05) and the business impact is meaningful:

**Priority 1 — Footfall (strongest lever)**
Footfall has the highest impact per unit of any variable. Every initiative that increases customer visits — better signage, location improvement, loyalty programmes, local partnerships — is likely to produce the highest return in monthly sales.

**Priority 2 — Store Type and Location Strategy**
Airport stores significantly outperform Residential stores by ₹39,891 per month and High Street stores by ₹22,007 per month. Leadership should factor store format into expansion and investment decisions. New store openings in Airport or Mall locations are likely to generate higher baseline sales than Residential locations.

**Priority 3 — Regional Strategy (South and West)**
South and West region stores significantly outperform East region stores (by ₹21,231 and ₹20,222 respectively). Leadership should investigate what drives this regional advantage — whether it is demographics, competition density, or income levels — and apply those learnings to underperforming regions.

**Priority 4 — Holiday Month Preparation**
Holiday months generate an additional ₹15,895 in sales. Leadership should ensure full inventory stocking, maximum staffing, and targeted promotions ahead of every public holiday month to fully capture this uplift.

**Priority 5 — Inventory Availability**
Each 1 percentage point increase in inventory availability adds ₹3,081 in monthly sales. Stores with stock-out issues are losing revenue directly. Improving supply chain reliability and replenishment speed for low-availability stores is a concrete and measurable action.

**Priority 6 — Staff Count**
Each additional staff member adds ₹2,957 in monthly sales. Understaffed stores may be losing sales due to long queues, poor service, or missed conversions. Leadership should review staffing levels at stores with below-average sales relative to their footfall.

---

## 3. Which Variables Should Not Be Over-Interpreted?

**region_North (p = 0.2766 — not significant):**
North region stores appear to generate ₹7,606 more than East region stores, but this difference is not statistically significant. Leadership should not make major regional investment decisions based on this coefficient. It may simply reflect random variation in this dataset.

**store_type_Mall (p = 0.3056 — not significant):**
Mall stores appear to generate ₹9,852 less than Airport stores, but again this difference is not statistically significant. Mall and Airport stores perform comparably in this data — do not treat this as evidence that Mall stores are inferior to Airport stores.

**marketing_spend (low return relative to cost):**
While marketing spend is statistically significant (p < 0.0001), each ₹1 spent returns only ₹1.17 in sales — a modest multiplier. Leadership should be cautious about large increases in marketing budget as a standalone strategy without first ensuring strong footfall and operational readiness.

**customer_rating and avg_discount_pct:**
These variables were not included in the final model due to very low or statistically insignificant correlations with monthly sales (customer_rating r = −0.028, p = 0.622; avg_discount_pct r = −0.091, p = 0.104). Leadership should not rely on discount increases as a reliable sales driver based on this data.

---

## 4. What Business Action Would You Recommend?

Based on the regression evidence, the following actions are recommended in order of priority:

**Action 1 — Invest in footfall-driving initiatives for low-traffic stores**
The single highest-return action is increasing customer visits. Stores with below-average footfall relative to their region and store type should be prioritised for marketing campaigns, signage improvement, and loyalty programmes.

**Action 2 — Resolve inventory availability issues immediately**
Stores with inventory availability below 85% are measurably losing sales. Each percentage point of improvement adds ₹3,081 per month. A focused supply chain review for the lowest-availability stores should be the fastest short-term revenue win.

**Action 3 — Optimise staffing at high-footfall stores**
Stores with high footfall but underperforming sales relative to the model (large negative residuals) should be reviewed for staffing adequacy. Adding one staff member is predicted to add ₹2,957 per month.

**Action 4 — Prepare a holiday month playbook**
Holiday months add ₹15,895 on average. A standardised playbook — maximum inventory, full staffing, promotional offers — should be deployed across all stores ahead of every public holiday month.

**Action 5 — Review store expansion strategy**
New store openings should prioritise Airport and high-footfall locations. Residential stores consistently underperform Airport stores by nearly ₹40,000 per month after controlling for all other factors.

**Action 6 — Investigate South and West regional outperformance**
South and West stores significantly outperform East stores. Understanding why — whether it is local demographics, competitor weakness, or store management practices — can help replicate this success in the East and North regions.

---

## 5. What Risks or Limitations Should Leadership Keep in Mind?

**Limitation 1 — Short observation window:**
The dataset covers only 4 months (January–April 2025). Seasonal patterns, year-end peaks, and festive season effects are not captured. The model may not generalise well to months outside this window.

**Limitation 2 — Missing variables:**
The model explains 83.27% of sales variation, but 16.73% remains unexplained. Important factors not in the dataset include competitor pricing and promotions, local economic conditions, store age and renovation status, and online vs in-store sales split.

**Limitation 3 — Residual outliers:**
Several stores have large residuals (e.g., STR-1017 under-performed by ₹174,527 in March 2025). These suggest store-specific events — local disruptions, competitor openings, or operational problems — that the model cannot anticipate or explain.

**Limitation 4 — Coefficients are averages:**
Each coefficient represents the average effect across all 80 stores and 4 months. The actual impact of, say, adding one staff member may vary significantly between a small Residential store and a large Airport store.

**Limitation 5 — Multicollinearity:**
Some independent variables (e.g., footfall and staff_count) may be correlated with each other, which can affect the precision of individual coefficients. Leadership should interpret individual coefficients directionally rather than as precise point estimates.

---

## 6. Why Does Regression Show Association but Not Automatically Prove Causation?

Regression analysis identifies statistical associations — patterns in which variables tend to move together — but it cannot confirm that one variable directly causes another to change. There are three key reasons this matters for leadership:

**Reason 1 — Reverse causation:**
Higher footfall may cause higher sales, but higher sales may also attract more footfall (popular stores draw more visitors). The regression cannot determine which direction the effect runs.

**Reason 2 — Confounding variables:**
A store in a wealthy neighbourhood may have both high marketing spend and high sales — but the real driver could be the neighbourhood's income level, not the marketing. If income level is not in the model, marketing spend gets credit for an effect it may not truly cause.

**Reason 3 — Coincidence across time:**
Two variables can move together across the 4-month observation window purely by coincidence. A variable that appears significant in this short window may not maintain that relationship over a full year or across different market conditions.

**Practical implication for leadership:**
Use the regression findings to form hypotheses and prioritise investigation — not to make irreversible commitments. Before significantly increasing marketing spend based solely on its coefficient, run a controlled experiment (such as an A/B test across stores) to confirm the causal relationship. Regression evidence is the starting point for business decisions, not the final proof.

---

*Analysis based on 320 records, 80 stores, Jan–Apr 2025. Final model: MR1 (R² = 0.8327). Full workings in analysis/regression_workbook.xlsx.*

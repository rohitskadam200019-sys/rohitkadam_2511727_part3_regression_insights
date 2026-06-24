# Model Equations — Part 3: Regression Analysis

**Student:** Rohit Kadam
**Student ID:** 2511727

---

## Dummy Variable Approach

### Why Dummy Variables Are Needed
The dataset contains two categorical variables — `region` and `store_type` — that cannot be used directly in a regression model because regression requires numerical inputs. Dummy variables convert each category into a binary column (1 = belongs to this category, 0 = does not).

### Categorical Variables Converted

**Variable 1: region**
Categories: East, North, South, West

**Variable 2: store_type**
Categories: Airport, High Street, Mall, Residential

---

### Reference Category Selection

To avoid the dummy variable trap (perfect multicollinearity), one category from each variable must be dropped and used as the reference category. All other dummy coefficients are interpreted relative to this reference.

| Variable | Reference Category | Reason |
|---|---|---|
| `region` | **East** | East has the largest number of records and serves as a natural baseline |
| `store_type` | **Airport** | Airport stores have the highest average sales and serve as a meaningful baseline |

---

### Dummy Variables Created

**For region (reference = East — dropped):**

| Dummy Column | Value = 1 When | Value = 0 When |
|---|---|---|
| `region_North` | Store is in North region | Store is not in North region |
| `region_South` | Store is in South region | Store is not in South region |
| `region_West` | Store is in West region | Store is not in West region |

**For store_type (reference = Airport — dropped):**

| Dummy Column | Value = 1 When | Value = 0 When |
|---|---|---|
| `store_type_HighStreet` | Store is High Street type | Store is not High Street type |
| `store_type_Mall` | Store is Mall type | Store is not Mall type |
| `store_type_Residential` | Store is Residential type | Store is not Residential type |

---

### How to Interpret Dummy Coefficients

Each dummy coefficient shows the estimated difference in monthly_sales compared to the reference category, holding all other variables constant.

**Example — region_South coefficient = +21,231:**
A South region store is predicted to have ₹21,231 higher monthly sales than an East region store (the reference), all else equal.

**Example — store_type_Residential coefficient = -39,891:**
A Residential store is predicted to have ₹39,891 lower monthly sales than an Airport store (the reference), all else equal.

---

### Avoiding the Dummy Variable Trap

If all categories were included (e.g., East + North + South + West), their sum would always equal 1 for every row, creating perfect multicollinearity. This makes the regression mathematically unsolvable. By dropping one category (the reference), this redundancy is eliminated.

- Total region categories: 4 → Dummies created: 3 (East dropped)
- Total store_type categories: 4 → Dummies created: 3 (Airport dropped)

The dummy variables are created in `analysis/regression_workbook.xlsx` on the `dummy_variables` sheet and used in the multiple regression model (MR1).

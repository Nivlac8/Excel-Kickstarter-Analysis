# 📊 Kickstarter Campaign Analysis (Excel)

## 🎯 Objective
The goal of this project was to analyze a real-world dataset of 300,000+ crowdfunding campaigns to identify the specific factors that drive "Viral" success versus failure. 

I acted as a Data Analyst to clean the raw data, engineer new business metrics, and visualize which categories yield the highest return on investment.

## 📂 Dataset
**Source:** [Kaggle - Kickstarter Projects (Raw Data)](https://www.kaggle.com/datasets/kemical/kickstarter-projects)  
**Volume:** ~370,000 Rows, 15 Columns  
**Condition:** The raw data contained mixed currencies, corrupted rows, Unix timestamps, and "future dates" (Year 2042 errors).

## 🛠️ Skills Applied
* **Advanced Data Cleaning:** Audited and removed 4,000+ corrupted rows where project names caused column shifts.
* **Data Normalization:** Standardized mixed currencies (GBP, EUR, AUD) into a single `USD` metric for accurate comparison.
* **Feature Engineering:** Built complex Nested `IF/AND` logic to segment campaigns into performance tiers ("Viral Hit" vs. "Funded").
* **Pivot Table Analysis:** Shifted analysis from raw counts to **Success Rates (% of Row Total)** to normalize for category size.

## 🔍 Key Cleaning Steps
1.  **The "Time Travel" Fix:** Identified and removed rows with launch dates in 1970 (Unix Epoch errors) and 2042 (System errors).
2.  **Currency Traps:** Hid original `goal` and `pledged` columns to prevent accidental aggregation of mixed currencies, utilizing only `usd_pledged_real`.
3.  **Ghost Row Removal:** Filtered and deleted 100+ blank rows that were creating null categories in the final reporting.

## 🧠 Business Logic (Feature Engineering)
To differentiate between a project that raised $10 and one that raised $1,000,000, I created a custom **`Status_Tier`** column using this logic:

```excel
=IF(K2="failed", "Failed", IF(AND(K2="successful", N2>=10000), "Viral Hit", IF(K2="successful", "Funded", "Other")))

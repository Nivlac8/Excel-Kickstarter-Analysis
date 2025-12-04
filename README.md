# 📊 Kickstarter Campaign Analysis (Excel)

## 🎯 Executive Summary
The goal of this project was to analyze a dataset of **300,000+ crowdfunding campaigns** to identify the specific factors that differentiate "Viral" global hits from standard success stories.

Acting as a Data Analyst, I performed an end-to-end audit: cleaning corrupted raw data, engineering new financial logic to classify success, and building a dynamic dashboard to visualize Return on Investment (ROI) by category.

## 📂 The Dataset
**Source:** [Kaggle - Kickstarter Projects (Raw Data)](https://www.kaggle.com/datasets/kemical/kickstarter-projects)  
**Volume:** ~375,000 Rows, 15 Columns  
**Condition:** The raw data was "dirty," containing mixed currencies (GBP, EUR, AUD), corrupted row shifts, Unix timestamp errors, and system glitches (dates in the year 2042).

## 🛠️ Technical Skills Applied
* **Advanced Data Cleaning:** Used filtering techniques to identify and remove "Ghost Rows" (blanks) and "Time Traveler" data (future dates).
* **Feature Engineering:** Constructed nested logical tests (`IF/AND`) to create custom business tiers.
* **Normalization:** Standardized 10+ international currencies into a single `USD` comparison metric.
* **Pivot Table Analysis:** Shifted from raw volume counts to **Percentage Success Rates** to normalize for category popularity.

## 🔍 The Cleaning Process (ETL)
I transformed the raw CSV into an analytical dataset using the following pipeline:

1.  **Corrupted Row Removal:** Identified rows where project names containing commas caused column shifting, resulting in text appearing in numeric columns.
2.  **Date Integrity Fix:** * Converted text strings to valid `Short Date` format.
    * Removed "Time Traveler" records (Years > 2025) and "Unix Epoch" errors (Year 1970).
    * Calculated `Days_Active` using `=INT(Deadline - Launched)` to measure campaign duration.
3.  **Currency Standardization:** * Detected a "Currency Trap" where the `Goal` column mixed Yen, Euro, and Dollars.
    * Hid the misleading columns and utilized `usd_pledged_real` for all financial calculations.

## 🧠 Business Logic (Feature Engineering)
To solve the business question *"What makes a project a viral hit?"*, I created a new variable called **`Status_Tier`**.

I used a **Nested IF Statement** to segment successful projects into high-value outliers vs. standard funding:

```excel
=IF(K2="failed", "Failed", IF(AND(K2="successful", N2>=10000), "Viral Hit", IF(K2="successful", "Funded", "Other")))

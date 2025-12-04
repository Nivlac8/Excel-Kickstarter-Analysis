<img width="532" height="362" alt="Pivot Chart" src="https://github.com/user-attachments/assets/008da512-b028-4b35-9cb7-a46428037261" /># 📊 Kickstarter Campaign Analysis (Excel)

## 🎯 Executive Summary
The goal of this project was to analyze a dataset of **300,000+ crowdfunding campaigns** to identify the specific factors that differentiate "Viral" global hits from standard success stories.

Acting as a Data Analyst, I performed an end-to-end audit: cleaning corrupted raw data, engineering new financial logic to classify success, and building a dynamic dashboard to visualize Return on Investment (ROI) by category.

## 📂 The Dataset
**Source:** [Kaggle - Kickstarter Projects (Raw Data)](https://www.kaggle.com/datasets/kemical/kickstarter-projects)  
**Volume:** ~375,000 Rows, 15 Columns  
**Condition:** The raw data was "dirty," containing mixed currencies (GBP, EUR, AUD), corrupted row shifts, Unix timestamp errors, and system glitches.

## 🛠️ Technical Skills Applied
* **Advanced Data Cleaning:** Used filtering techniques to identify and remove "Ghost Rows" (blanks) and "Time Traveler" data (future dates).
* **Feature Engineering:** Constructed nested logical tests (`IF/AND`) to create custom business tiers.
* **Normalization:** Standardized 10+ international currencies into a single `USD` comparison metric.
* **Pivot Table Analysis:** Shifted from raw volume counts to **Percentage Success Rates** to normalize for category popularity.

## 🔍 The Cleaning Process (ETL)
I transformed the raw CSV into an analytical dataset using the following pipeline:

1.  **Corrupted Row Removal:** Identified rows where project names containing commas caused column shifting, resulting in text appearing in numeric columns.
2.  **Date Integrity Fix:**
    * Converted text strings to valid `Short Date` format.
    * Removed "Time Traveler" records (Years > 2025) and "Unix Epoch" errors (Year 1970).
    * Calculated `Days_Active` using `=INT(Deadline - Launched)` to measure campaign duration.
3.  **Currency Standardization:**
    * Detected a "Currency Trap" where the `Goal` column mixed Yen, Euro, and Dollars.
    * Hid the misleading columns and utilized `usd_pledged_real` for all financial calculations.

## 🧠 Business Logic (Feature Engineering)
To solve the business question *"What makes a project a viral hit?"*, I created a new variable called **`Status_Tier`** using this nested logic:

```excel
=IF(K2="failed", "Failed", IF(AND(K2="successful", N2>=10000), "Viral Hit", IF(K2="successful", "Funded", "Other")))
```

## Category Definitions
* **Viral Hit:** Successful status AND raised ≥ $10,000 USD.
* **Funded:** Successful status AND raised < $10,000 USD.
* **Failed:** Project failed to reach the goal.

## Key Insights & Results
* **The Winner:** The Design category (specifically Product Design) has the highest probability of becoming a "Viral Hit."
* **The Volume Trap:** While "Film & Video" has the highest volume of projects, its viral success rate is significantly lower than niche categories like "Tabletop Games."

## Conclusion & Recommendations
Based on the data analysis, simply launching in a popular category like Film does not guarantee high returns. To maximize the probability of a "Viral Hit" (raising >$10k USD), creators and investors should focus on the **Product Design** and **Tabletop Games** sectors, which demonstrate a significantly higher success-to-failure ratio compared to other categories.

## Portfolio Visuals

### 1. The Analysis Dashboard
Showing the "Success Rate" pivot table and chart proving Design is the winner.
![Dashboard](<img width="482" height="364" alt="Pivot Table" src="https://github.com/user-attachments/assets/3f9fcbfa-e49e-4ee0-a729-0275dcff9164" />
 )
 ![Dashboard](<img width="532" height="362" alt="Pivot Chart" src="https://github.com/user-attachments/assets/590d643e-ecec-4f77-8878-d7252a884c78" />
 )

### 2. Complex Logic Implementation
Showing the nested IF/AND formula used to categorize the 300k rows.
![Formula](Formula.png)

### 3. Data Cleaning Verification
Showing the cleaned dataset with valid Dates, right-aligned Currency, and hidden "Trap" columns.
![Cleaning](Cleaning.png)

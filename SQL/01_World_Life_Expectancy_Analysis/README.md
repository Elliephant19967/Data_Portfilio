# [Project Title: e.g., Analyzing Global Life Expectancy Trends]

## 📌 Overview
A concise one-paragraph summary of the business question or hypothesis you investigated and the primary outcome.
*   **Objective:** [e.g., To identify key factors influencing life expectancy changes worldwide and visualize trends over time.]
*   **Key Findings:** [e.g., Found a strong positive correlation (r=0.85) between socioeconomic factors and life expectancy, while the relationship with healthcare spending was more nuanced.]

## 🧠 The Why (Context & Hypothesis)
*This is where your Psychology BA becomes a superpower. Explain the reasoning behind the analysis.*
*   **Background:** [e.g., Understanding global health disparities requires moving beyond simple metrics. Research in social psychology suggests...]
*   **Initial Hypothesis:** [e.g., I hypothesized that GDP per capita would be a stronger predictor of life expectancy than total healthcare expenditure per capita, based on theories of societal development and well-being.]

## 📊 Data Sources
| Source | Description | Link |
| :--- | :--- | :--- |
| Kaggle: World Life Expectancy | Dataset containing life expectancy and related health/economic metrics by country and year. | [URL] |

## 🛠️ Tools & Technologies
*   **Database:** MySQL
*   **Key Techniques:** Data cleaning, complex joins, window functions (ROW_NUMBER, RANK), aggregate functions, CTEs.

## 🔧 Data Cleaning & Preparation
The raw data required several transformations:
1.  **Handling Duplicates:** Used `ROW_NUMBER()` with `PARTITION BY` to identify and remove duplicate country-year entries.
2.  **Standardizing Values:** Converted all country names to a standard format using `TRIM()` and `UPPER()`.
3.  **Addressing Missing Data:** Used `AVG(...) OVER (PARTITION BY Country)` to impute missing values based on a country's own averages, which is more accurate than a global average.

## 📈 Exploratory Data Analysis
Key questions I sought to answer:
1.  How has global life expectancy changed from 2000-2015?
2.  What is the relationship between life expectancy and economic indicators?
3.  Which countries showed the most significant improvement or decline?

```sql
-- Example snippet of a core query used.
SELECT
    Country,
    Year,
    `Life expectancy`,
    AVG(`Life expectancy`) OVER(PARTITION BY Country) AS Avg_Country_Life_Exp,
    `GDP per capita`
FROM world_life_expectancy
WHERE Year > 1999
ORDER BY Country, Year;
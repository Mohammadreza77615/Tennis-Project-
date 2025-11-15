# Tennis-Project-
This project performs EDA on a tennis dataset, integrating 440k files into 15 unified datasets. It answers 25 key questions covering demographics, match stats, and performance metrics. Strong emphasis is placed on data cleaning, validation, and inferring miss values. It concludes by comparing bookmaker (69.3%) vs. crowd (68.6%) prediction accuracy.


# 🎾 Exploratory Data Analysis on Professional Tennis

This project performs a comprehensive Exploratory Data Analysis (EDA) on a large-scale tennis dataset. The dataset comprises over 440,000 individual parquet files aggregated from 60 daily folders.

The notebook (`EDA Tennis Project.ipynb`) details the full data pipeline, from raw file integration and rigorous cleaning to in-depth statistical analysis to answer 17 key questions about the sport.

## 🗂️ Dataset

The project integrates 15 distinct datasets from raw parquet files. Key datasets include:
* **Match Info:** `event`, `tournament`, `season`, `round`, `venue`
* **Player Info:** `home_team`, `away_team` (containing demographics like height, weight, handedness)
* **Match Stats:** `home_team_score`, `away_team_score`, `time`, `statistics` (Aces, Double Faults), `pbp`
* **Prediction Data:** `odds`, `votes`

## 🚀 Project Workflow

1.  **Data Integration (`TennisDataProcessor`):**
    * Processes 60 folders containing 440,000+ `.parquet` files in batches.
    * Finds missing files and inspects data structure.
    * Combines batches into 15 final, unified `.parquet` files (e.g., `event_complete.parquet`).

2.  **Data Cleaning & Validation:**
    * Employs a strict validation logic for match analysis:
        * Matches must have a valid `winner_code`.
        * Matches must have at least 2 **valid sets**.
        * A **valid set** is defined as lasting 15-60 minutes and containing 6-16 games.
    * Missing player `gender` is inferred from tournament type (e.g., 'WTA' → 'F', 'ATP' → 'M').
    * Missing player `height` or `weight` is imputed using a healthy BMI average calculated from valid data (Men: 22.8, Women: 21.2).

3.  **Key Analytical Questions (EDA):**
    * **Player Demographics:**
        * Identified 2,644 unique players from 105 countries.
        * Calculated average height (182.2 cm) and found men (184.3 cm) are significantly taller than women (173.2 cm).
        * Found that 11.6% of players (with known data) are left-handed.
    * **Match Statistics:**
        * Calculated average match duration (88.9 min) and average aces per match (5.63).
        * Determined that 2-set matches (66.3%) are significantly more common than 3-set matches (33.7%).
        * Analyzed statistical differences by gender (e.g., Men: 9.07 games/set vs. Women: 8.66 games/set).
    * **Performance & Prediction Analysis:**
        * Identified the player with the most wins (`Popko D.` - 28) and longest winning streak (`Popko D.` - 21).
        * Developed a "Composite Success Score" (weighting player count, Top 100 players, weighted wins, and prize money) to find the most successful country (Result: **USA**).
        * Analyzed "Comeback Kings" (players who win after losing the first set).
        * Compared the predictive accuracy of **Bookmaker Odds (69.3%)** to the **"Wisdom of the Crowd" (68.6%)**, finding them almost identical.

## 🛠️ Core Libraries Used

* `pandas`
* `numpy`
* `matplotlib` & `seaborn`
* `scipy.stats` (for t-tests and ANOVA)
* `pathlib`

## 🏃 How to Run

1.  Ensure the 15 final `.parquet` datasets are available in the `Final_parquet/` directory.
2.  Open the `EDA Tennis Project.ipynb` notebook in a Jupyter environment.
3.  Install the required libraries (e.g., `pip install pandas matplotlib seaborn scipy`).
4.  Run the cells sequentially to reproduce the analysis.
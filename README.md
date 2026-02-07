# 📊 MERS Epidemiological Data Analysis & Predictive Modeling (2012–2019)

## 📝 Project Overview
This project presents a comprehensive epidemiological study of the **Middle East Respiratory Syndrome (MERS-CoV)** based on official data from the **World Health Organization (WHO)**. The study covers the period from the initial identification in 2012 through 2019.

The core of this project is a **Case Study in Data Science**, following the **CRISP-DM methodology**. It explores the challenges of modeling "bursty," non-linear medical data, where zero-inflated distributions and extreme outliers (outbreaks) make traditional statistical methods difficult to apply.

## 🎯 Objectives
*   **Data Exploration:** Analyze the geographical and demographic distribution of MERS.
*   **Transmission Study:** Investigate the relationship between primary (zoonotic) and secondary (human-to-human) transmission.
*   **Predictive Modeling:** Build and compare models to forecast weekly new cases.
*   **Methodological Contrast:** Evaluate why non-linear machine learning models (Random Forest) outperform classical statistical approaches (Linear Regression) in epidemiological contexts.

## 📂 Dataset Description
The analysis utilizes six distinct datasets providing various angles of the epidemic:
1.  **`weekly_clean.csv`**: Time-series data of new weekly cases (Primary modeling set).
2.  **`country_count_latest.csv`**: Global distribution across 27 countries.
3.  **`demographics.csv`**: Annual data on gender ratios, fatality rates, and healthcare worker infections.
4.  **`type_of_contact.csv`**: Data on primary vs. secondary transmission pathways.
5.  **`details.csv`**: Clinical metadata regarding symptoms and incubation periods.
6.  **`saudi_arabia_vs_south_korea_comparison.csv`**: Specific metrics comparing the two largest outbreak epicenters.

## 🛠 Tech Stack
*   **Language:** R
*   **Data Manipulation:** `dplyr`, `tidyr`, `zoo`, `lubridate`
*   **Visualization:** `ggplot2`, `scales`
*   **Statistical Analysis:** `moments`, `lmtest`, `nortest`
*   **Machine Learning:** `randomForest`
*   **Reporting:** `RMarkdown`, `knitr`

## 📈 Methodology (CRISP-DM)

### 1. Data Understanding & Quality
Conducted rigorous data diagnostics including:
*   **Skewness Analysis:** Identified high positive skewness (2.65), typical for epidemic spikes.
*   **Outlier Detection:** Identified 107 significant outliers representing major outbreaks rather than errors.
*   **Zero-Inflation:** Managed a dataset where ~21% of records were zero, requiring specific handling in modeling.

### 2. Feature Engineering
To improve model accuracy, I developed several derived features:
*   **Lag Variables (`Lag1`, `Lag2`):** Capturing the "memory" of the epidemic.
*   **Rolling Means (`RollMean4`):** Smoothing noise to identify medium-term trends.
*   **Logarithmic Transformation:** Normalized the target variable (`log1p`) to stabilize variance across outbreaks.

### 3. Modeling Approach
*   **Baseline Model:** Log-Linear Multiple Regression.
*   **Advanced Model:** Optimized Random Forest (Regression Mode).
    *   *Tuning:* Optimized `nodesize` and `mtry` to minimize overfitting.

## 🏆 Results & Evaluation
The models were tested on a hold-out set of the last 4 weeks of the data.

| Metric | Log-Linear Model | Random Forest (Optimized) |
| :--- | :--- | :--- |
| **R-squared** | ~0.66 | **~0.71** |
| **MAE (Mean Absolute Error)** | 0.66 | **0.69** |
| **MAPE (%)** | ~97% | **~30%** |

**Key Finding:** While the Linear Model performed surprisingly well after log-transformation, the **Random Forest** provided superior stability and handled the non-linear "bursts" of the virus more effectively, yielding a significantly lower MAPE.

## 🚀 How to Run
1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/mers-data-science-project.git
   ```
2. Ensure you have R and RStudio installed.
3. Install required packages:
   ```r
   install.packages(c("tidyverse", "randomForest", "zoo", "moments", "knitr", "lmtest", "nortest"))
   ```
4. Open `CaseStudy_MERS.Rmd` and click **Knit** to generate the HTML report.

or just open html file to see results

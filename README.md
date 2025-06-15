# Insurance Risk Analytics Challenge - Week 3  
## Task 1: Git/GitHub Setup + Exploratory Data Analysis (EDA)

> **Challenge Title:** B5W3: End-to-End Insurance Risk Analytics & Predictive Modeling  
> **Company:** AlphaCare Insurance Solutions (ACIS)  
> **Goal:** Analyze historical insurance claim data to uncover low-risk segments and build smart models that optimize premiums.  

This repository contains the code, data, and documentation for **Task 1**, which focuses on setting up version control using **Git & GitHub**, and performing **Exploratory Data Analysis (EDA)** on South African car insurance data.

---

## 🧭 Project Overview

As a Marketing Analytics Engineer at **AlphaCare Insurance Solutions (ACIS)**, your task is to analyze historical insurance claim data from February 2014 to August 2015. This analysis will help ACIS optimize marketing strategies and identify low-risk customer segments for competitive pricing.

In this task, we:

- ✅ Set up a Git repository with proper documentation (`README`, `.gitignore`)
- ✅ Implemented Continuous Integration (CI) using GitHub Actions
- ✅ Performed exploratory data analysis (EDA) to understand the structure, quality, and patterns in the dataset
- ✅ Visualized key insights such as loss ratios, trends over time, geographic differences, and vehicle risk profiles

---

# Insurance Risk Analytics Challenge - Week 3  
## Task 1: Git/GitHub Setup + Exploratory Data Analysis (EDA)

> **Challenge Title:** B5W3: End-to-End Insurance Risk Analytics & Predictive Modeling  
> **Company:** AlphaCare Insurance Solutions (ACIS)  
> **Goal:** Analyze historical insurance claim data to uncover low-risk segments and build smart models that optimize premiums.  

This repository contains the code, data, and documentation for **Task 1**, which focuses on setting up version control using **Git & GitHub**, and performing **Exploratory Data Analysis (EDA)** on South African car insurance data.

---

## 🧭 Project Overview

As a Marketing Analytics Engineer at **AlphaCare Insurance Solutions (ACIS)**, your task is to analyze historical insurance claim data from February 2014 to August 2015. This analysis will help ACIS optimize marketing strategies and identify low-risk customer segments for competitive pricing.

In this task, we:

- ✅ Set up a Git repository with proper documentation (`README`, `.gitignore`)
- ✅ Implemented Continuous Integration (CI) using GitHub Actions
- ✅ Performed exploratory data analysis (EDA) to understand the structure, quality, and patterns in the dataset
- ✅ Visualized key insights such as loss ratios, trends over time, geographic differences, and vehicle risk profiles

---

## 🗂️ Repository Structure

insurance-risk-modeling/
├── data/ # Folder containing raw and processed datasets
│ └── MachineLearningRating_v3.txt # Raw insurance dataset (text format)
├── Notebook/ # Folder containing notebook files
│ └── EDA.ipynb # Jupyter notebook with full EDA
├── requirements.txt # Python dependencies
├── .gitignore # Files to exclude from version control
├── README.md # This file
└── .github/
└── workflows/
└── ci.yml # GitHub Actions CI workflow
# 📊 Statistical Analysis & Data Interpretation Summary

## 1. 📁 Dataset Overview
The dataset includes various insurance policy attributes and a target variable `TotalClaims`, representing the total amount claimed. Key numeric predictors include:
- `TotalPremium`, `SumInsured`, `ExcessSelected`, `CalculatedPremiumPerTerm`, `CustomValueEstimate`
- Categorical or encoded fields: `PolicyID`, `PostalCode`, `UnderwrittenCoverID`, `TransactionMonth`, etc.

---

## 2. 🧪 Statistical Testing & Exploratory Insights

### 🔹 2.1 Correlation Analysis (Pearson)
| Feature                 | Correlation with `TotalClaims` |
|-------------------------|-------------------------------|
| `TotalPremium`          | **+0.78** (strong positive)   |
| `SumInsured`            | **+0.70**                     |
| `ExcessSelected`        | **-0.22** (mild negative)     |
| `CalculatedPremiumPerTerm` | +0.30                      |

**Interpretation**:
- Higher premiums and insured values are **strongly associated** with higher claim amounts.
- `ExcessSelected` (deductible) shows a **weak inverse relation**, indicating customers with higher excess may claim less.

---

### 🔹 2.2 Distribution Testing
- **Target (`TotalClaims`)** is **right-skewed** with outliers.
  - Transformation (e.g., `log1p`) is recommended for normalization.
- Features like `TotalPremium` and `SumInsured` are also **positively skewed**.

### 🔹 2.3 ANOVA / t-Test on Categorical Groups
- **ANOVA tests** were used to assess differences in `TotalClaims` across levels of:
  - `TransactionMonth`: ✅ Significant variation (seasonality)
  - `UnderwrittenCoverID`: ✅ Significant impact on mean claims
  - `PostalCode`: ❌ Not significant — potential noise

---

## 3. 🧠 SHAP-Based Interpretability Insights

| Rank | Feature               | SHAP Impact (Mean) | Insight Summary                                                   |
|------|-----------------------|--------------------|--------------------------------------------------------------------|
| 1    | `TotalPremium`        | 🔥 Very High       | Main driver of predicted claims                                   |
| 2    | `SumInsured`          | High               | Larger coverage leads to higher risk exposure                     |
| 3    | `ExcessSelected`      | Moderate (↘️)      | Higher excess = lower predicted claims                            |
| 4    | `TransactionMonth`    | Moderate           | Indicates seasonal claim trends (e.g., accidents in certain months)|
| 5    | `UnderwrittenCoverID` | Moderate           | Type of coverage affects claim likelihood                         |

---

## 4. 📉 Modeling Error Analysis

### 🔸 CV & Test Performance
| Model         | CV RMSE | Test RMSE | R²     | Interpretation                                 |
|---------------|---------|-----------|--------|------------------------------------------------|
| Random Forest | 2229    | 2257.7    | -0.04  | Better generalization but underfits slightly   |
| XGBoost       | 2673    | 2502.4    | -0.28  | Overfits CV, performs worse on unseen data     |

**Conclusion**:
- Models underperform on test data due to noise, outliers, or irrelevant features.
- Simplifying features using SHAP improved consistency but not generalization.

---

## 5. 📌 Final Interpretation & Recommendations

- **Statistical relationships** (via correlation and ANOVA) and **SHAP results** strongly support that:
  - `TotalPremium`, `SumInsured`, and `ExcessSelected` should be core modeling features.
  - Many low-impact features introduce noise and **should be dropped**.
- Applying **log-transformation** to skewed variables (including `TotalClaims`) may improve model linearity and performance.
- **Simplified models** with selected features and robust preprocessing are preferred over complex ones in this context.

---

## ✅ Next Actions
- Conduct outlier analysis & winsorization for extreme values.
- Retrain models on top SHAP features with transformed variables.
- Reassess model performance after rebalancing and potential resampling (if necessary).


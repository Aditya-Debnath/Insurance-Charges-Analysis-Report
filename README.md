# Insurance-Charges-Analysis-Report
It is a project for CSE303 - Statistics for Data Science, CSE, East West University

This report analyzes two insurance datasets to explore data characteristics, perform
preprocessing, visualize relationships between features, and build machine learning
regression models to predict insurance charges.

# Insurance Charges Analysis

A comparative analysis of two insurance datasets to explore data characteristics, perform preprocessing, visualize relationships between features, and build regression models to predict medical charges.

## Table of Contents
- [Project Overview](#project-overview)
- [Datasets](#datasets)
- [Preprocessing](#preprocessing)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Machine Learning Models](#machine-learning-models)
- [Results](#results)
- [Conclusion](#conclusion)
- [Repository Structure](#repository-structure)
- [Installation & Usage](#installation--usage)
- [Team](#team)
- [Acknowledgments](#acknowledgments)

## Project Overview
This project was completed as part of **CSE303: Statistics for Data Science**.  
We analyze two insurance datasets—one clean and one realistic/uncleaned—to predict individual medical costs billed by health insurance. The workflow includes data cleaning, exploratory visualizations, and regression modeling using Linear Regression and Decision Tree algorithms.

## Datasets
Two CSV files were used:

| Feature            | Dataset 1 (`insurance.csv`)       | Dataset 2 (`insurance_uncleaned_realistic.csv`) |
|--------------------|-----------------------------------|-------------------------------------------------|
| Rows               | 1,338                             | 1,338                                           |
| Columns            | 7                                 | 10                                              |
| Features           | age, sex, bmi, children, smoker, region, charges | age, sex, bmi, children, smoker, region, blood_pressure, exercise_level, medical_history, charges |

**Target variable:** `charges` (continuous)

## Preprocessing
- Standardized column names.
- Handled missing values (numeric imputation with mode/mean, categorical encoding).
- Removed duplicate rows (1 duplicate in Dataset 1, 0 in Dataset 2).
- Converted categorical columns to numeric:
  - `smoker` → `smoker_num` (yes=1, no=0)
  - `sex` → `sex_num` (male=0, female=1)
  - `region` → `region_num` (ordinal mapping)
- Ensured `charges` column is numeric (median imputation for conversion errors).

### Preprocessing Summary – Dataset 2
Missing values before imputation:
- `bmi`: 50, `smoker`: 30, `blood_pressure`: 353, `exercise_level`: 540, `medical_history`: 259

## Exploratory Data Analysis (EDA)
Key visualizations and insights:

- **Correlation Matrix (Dataset 1):** Strong positive correlation (0.79) between `smoker_num` and `charges`. Moderate positive correlation of `age` and `bmi` with charges.
- **Correlation Matrix (Dataset 2):** Smoking again shows the strongest link to higher charges.
- **Count Plots:** Nearly balanced male/female distribution, with males slightly outnumbering females.
- **Bar Plot of Total Charges by Region:** Southeast region has the highest total charges (>$5M), while Northwest, Northeast, and Southwest are lower and similar.
- **BMI Histogram:** Approximately normal distribution centered around BMI 30.
- **Pie Charts:** Non-smokers represent ~80% of records; males account for >50% of total charges.
- **Boxplot (BMI by Gender):** Medians and IQRs similar, but outliers extend higher for males.
- **Scatter Plots (BMI vs Charges):** Clear separation: smokers show a positive trend (charges increase with BMI), non-smokers form a low-cost cluster.
- **Line Plots (Age vs Charges, Age vs Number of Children):** Charges rise with age, high variability, no consistent gender difference. Children count fluctuates with age, peaking around 40 for females.

## Machine Learning Models
Two regression models were trained and evaluated on each dataset:
- **Linear Regression**
- **Decision Tree Regressor**

### Training & Evaluation
- 80/20 train-test split
- Metrics: MAE, MSE, RMSE, R² Score
- MAE and RMSE also expressed as percentage of mean target value.

## Results

### Dataset 1 – Model Performance
| Metric              | Linear Regression | Decision Tree |
|---------------------|-------------------|---------------|
| Mean Target         | $14,272.01        | $14,272.01    |
| MAE                 | $4,181.35         | $2,591.67     |
| MAE (% of Mean)     | 29.29%            | 18.16%        |
| MSE                 | 35,604,894.07     | 18,722,739.94 |
| RMSE                | $5,966.99         | $4,326.98     |
| RMSE (% of Mean)    | 41.81%            | 30.32%        |
| R² Score            | 0.8062            | 0.8981        |

### Dataset 2 – Model Performance
| Metric              | Linear Regression | Decision Tree |
|---------------------|-------------------|---------------|
| Mean Target         | $15,836.71        | $15,836.71    |
| MAE                 | $2,143.18         | $2,066.35     |
| MAE (% of Mean)     | 13.53%            | 13.05%        |
| MSE                 | 7,157,336.70      | 7,066,064.17  |
| RMSE                | $2,675.32         | $2,658.21     |
| RMSE (% of Mean)    | 16.89%            | 16.79%        |
| R² Score            | 0.9006            | 0.9019        |

**Key takeaway:** In both datasets the Decision Tree outperforms Linear Regression with lower error and higher R².

## Conclusion
Both models demonstrate strong predictive capability:
- **Dataset 1:** R² ≈ 0.80 (80% variance explained)
- **Dataset 2:** R² ≈ 0.90 (90% variance explained)

The **Decision Tree** consistently achieves lower MAE, RMSE, and higher R², making it the preferred model for this insurance cost prediction task. Smoking status is the single most influential factor, and regional differences (especially in the Southeast) suggest healthcare cost disparities.

## Repository Structure
```
├── README.md
├── Insurance_Analysis_Report.pdf   # Full project report
├── insurance data for 2.1.csv
├── insurance data for 2.2.csv
├── CSE-303-Project.pptx
├── 2_1.ipynb
└── 2_2.ipynb
```

## Acknowledgments
- Course: CSE303 – Statistics for Data Science, Section 03
- Datasets inspired by typical medical cost prediction problems.

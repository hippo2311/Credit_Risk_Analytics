# Credit Risk Prediction

This project focuses on predicting whether a customer will be a _good_ or _bad_ credit risk. Using various attributes such as age, job, loan amount, loan duration, and other factors, the goal is to **develop machine learning models** that effectively distinguish between high-risk and low-risk borrowers.

---

## Table of Contents

1. [Project Overview](#project-overview)  
2. [Dataset Description](#dataset-description)  
3. [Data Handling & Preprocessing](#data-handling--preprocessing)  
4. [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)  
   - [Age & Gender Analysis](#age--gender-analysis)  
   - [Wealth Analysis](#wealth-analysis)  
   - [Purpose of Loan](#purpose-of-loan)  
   - [High vs. Low Risk](#high-vs-low-risk)  
5. [Machine Learning Models](#machine-learning-models)  
   - [Model Comparison](#model-comparison)  
   - [Decision Tree Analysis](#decision-tree-analysis)  
6. [Key Findings & Insights](#key-findings--insights)  
7. [How to Run](#how-to-run)  
8. [Recommendations & Future Work](#recommendations--future-work)  
9. [License](#license)

---

## Project Overview

Financial institutions must manage **credit risk** to reduce default rates and ensure profitability. This project leverages machine learning techniques (e.g., Logistic Regression, Support Vector Machine, Decision Tree, etc.) to build a **classification model** that predicts whether a borrower is likely to be a *good* (low risk) or *bad* (high risk) credit.

**Objectives**:
- Analyze demographic and financial attributes to identify their correlation with credit risk.
- Compare and select the best model(s) for predicting good/bad risk.
- Provide insights on which features most significantly impact credit risk decisions.

---

## Dataset Description

Each row in the dataset represents **one customer** with the following columns:

- **Age** (numeric): Customer’s age (range 19–75).  
- **Sex** (categorical): Male or Female.  
- **Job** (numeric): Job type/level (0–3).  
- **Housing** (categorical): Own, rent, or free.  
- **Saving accounts** (categorical): Levels of saving (little, moderate, rich, etc.) – _some missing_.  
- **Checking account** (categorical): Levels of checking (little, moderate, rich) – _some missing_.  
- **Credit amount** (numeric): Amount of credit (in Deutsche Marks).  
- **Duration** (numeric): Duration of the loan (in months).  
- **Purpose** (categorical): Purpose of the loan (car, education, furniture, etc.).  
- **Risk** (categorical): The target variable indicating **good** or **bad** risk.

**Note**: Missing data in `Saving accounts` and `Checking account` led to either imputation or column dropping (depending on the approach taken).

---

## Data Handling & Preprocessing

1. **Missing Values**  
   - A significant portion of missing data in `Saving accounts` and `Checking account` columns.  
   - Decision taken in the notebook: Drop these columns to avoid biased imputations (though other strategies like imputation are also possible).

2. **Encoding**  
   - **Label Encoding** for categorical variables (`Sex`, `Purpose`, `Housing`, etc.) to convert them into numeric form.  
   - The `Risk` column is converted to `0` (bad) and `1` (good) for correlation analyses and modeling.

3. **Train–Test Split**  
   - Split the data (e.g., 80% train and 20% test) for unbiased model evaluation.  

---

## Exploratory Data Analysis (EDA)

### Age & Gender Analysis
- **Gender Ratio**: The dataset contains roughly 2x more male customers than female.  
- **Age Groups**: Younger borrowers (\< 30) tend to borrow slightly higher amounts; older borrowers (\> 50) show higher default risk.  

### Wealth Analysis
- Grouped customers based on checking/saving account levels: _little_, _moderate_, and _rich_.  
- Observed higher defaults among those with **little** wealth indicators. Conversely, **rich** or **moderate** categories had a higher proportion of good loans.

### Purpose of Loan
- **Car Loans**: Largest loan amounts, also the highest risk (~35% classified as bad).  
- **Furniture/Equipment** and **Radio/TV**: Substantial proportion, with Radio/TV having somewhat lower credit amounts but higher bad risk.  
- **Domestic Appliances & Repairs**: Smaller loan sizes, minimal risk.  

### High vs. Low Risk
- **Correlation**: Loan amount (`Credit_amount`) and duration are negatively correlated with `Risk` (i.e., higher amounts and longer durations often mean _bad_ risk).  
- Borrowers with larger loans (\> 10k) and longer repayment terms face increased likelihood of being bad risk.

---

## Machine Learning Models

A variety of models were tested with cross-validation:

- **Logistic Regression (LR)**: Accuracy ~95.1%  
- **Linear Discriminant Analysis (LDA)**: Accuracy ~94.2%  
- **K-Nearest Neighbors (KNN)**: Accuracy ~81.9%  
- **Decision Tree (CART)**: Accuracy ~72.9%  
- **Naive Bayes (NB)**: Accuracy ~90.1%  
- **Random Forest (RF)**: Accuracy ~87.9%  
- **Support Vector Machine (SVM)**: Accuracy ~99.8% (highest)  
- **XGBoost (XGB)**: Accuracy ~81.8%

### Model Comparison
- **SVM** yielded the best overall accuracy (~99.8%), though further checks on overfitting would be advisable.  
- **Logistic Regression** and **LDA** also showed strong performance (\>94% accuracy).  
- **Decision Tree** had lower accuracy (~72.9%) but offers interpretability.

### Decision Tree Analysis
- Top features: **Credit amount**, **Duration**, **Age**.  
- Borrowers with lower `Credit_amount` and shorter `Duration` are classified as _good_.  
- Visual tree structure provides interpretability for business stakeholders.

---

## Key Findings & Insights

1. **Credit Amount & Duration**  
   - Major determinants of credit risk. Large, long-term loans are more prone to default.

2. **Age Factor**  
   - Younger (< 30) or older (> 50) borrowers display higher propensity for _bad_ risk.  
   - Middle-aged borrowers (30–40) often have lower default rates.

3. **Wealth Indicators**  
   - Borrowers with minimal savings/checking are riskier. Rich/moderate accounts correlate with better repayment outcomes.

4. **SVM**  
   - Achieves the best performance in terms of accuracy (~99.8%), but simpler models like Logistic Regression or LDA remain valuable for interpretability.

---

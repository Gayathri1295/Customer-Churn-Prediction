# Customer Churn Prediction

## Overview

This project focuses on predicting customer churn in a telecom company using machine learning techniques. By analyzing customer demographic data, service usage patterns, and contract details, the project identifies key factors contributing to churn and develops predictive models to enable proactive retention strategies.

Skills:
data preprocessing, exploratory data analysis (EDA), feature engineering, machine learning model development, and evaluation.

---

## Dataset

The dataset contains 7,043 rows and 28 columns, representing telecom customers. Key features include:

- **Demographic Information:** `Gender`, `Senior_Citizen`, `Partner`, `Dependents`
- **Service Usage Details:** `Service_type`, `Multiple_Lines`, `Internet_Service_type`, `Streaming_TV`
- **Contract Information:** `Contract`, `Monthly_Charges`, `Total_Charges`, `Tenure`
- **Customer Behavior:** `Number_of_Referrals`, `Offer`, `Avg_Monthly_Long_Distance_Charges`
- **Target Variable:** `Churn` (Yes/No)

---

## Project Workflow

### 1. Data Preprocessing
- **Inspection:** Checked for missing values, data types, and inconsistencies.
- **Data Cleaning:** Removed null values and handled invalid entries in columns like `Total_Charges`.
- **Data Transformation:**
  - Converted categorical variables (e.g., `Gender`, `Contract`) into numerical formats using label encoding and one-hot encoding.
  - Scaled numerical features (e.g., `Monthly_Charges`) using MinMaxScaler for logistic regression and StandardScaler for other models.

---

### 2. Exploratory Data Analysis (EDA)
- Analyzed customer demographics:
  - Most customers are non-senior citizens.
  - The majority of customers prefer month-to-month contracts.
- Service preferences:
  - Fiber Optic is the most popular internet service type.
  - Many customers do not opt for multiple lines or streaming services.
- Visualized relationships between churn and key features using:
  - Countplots (`seaborn`) for categorical features.
  - Heatmaps to identify correlations.

---

### 3. Feature Engineering
- Applied label encoding to binary categorical features like:
  - `Partner`, `Dependents`, `Streaming_TV`
- Used one-hot encoding for multi-class features like:
  - `Contract` (Month-to-Month, One Year, Two Year)
- Engineered new features like:
  - **Customer Lifetime Value (CLV):** Derived from tenure and monthly charges.

---

### 4. Machine Learning Models
Implemented multiple models to predict churn:

#### Logistic Regression
- **Scaling:** MinMaxScaler applied to numerical features.
- **Performance Metrics:**
  - Accuracy: **83%**
  - Insights: Features like tenure reduce churn probability, while high monthly charges increase churn risk.

#### Decision Tree
- **Scaling:** StandardScaler applied to numerical features.
- **Performance Metrics:**
  - Accuracy: **76%**
  - Insights: Decision tree captured non-linear relationships but overfitting was observed.

#### XGBoost
- **Hyperparameter Tuning:** GridSearchCV used to optimize learning rate, max depth, and number of estimators.
- **Performance Metrics:**
  - Accuracy: Improved with hyperparameter tuning.
  - Insights: XGBoost effectively handled imbalanced data with its built-in regularization.

#### K-Means Clustering
- Applied PCA to reduce dimensionality before clustering.
- Evaluated clusters using ARI (Adjusted Rand Index) and NMI (Normalized Mutual Information).

#### Random Forest
- Performed stratified k-fold cross-validation for robust evaluation.
- Achieved high accuracy with reduced overfitting compared to decision trees.

---

### 5. Model Evaluation

| Model               | Accuracy | Precision | Recall | F1 Score | ROC-AUC Score |
|---------------------|----------|-----------|--------|----------|---------------|
| Logistic Regression | 83%      | 0.81      | 0.78   | 0.79     | 0.85          |
| Decision Tree       | 76%      | 0.74      | 0.70   | 0.72     | 0.78          |
| XGBoost             | 88%      | 0.86      | 0.82   | 0.84     | 0.90          |
| Random Forest       | 85%      | 0.83      | 0.80   | 0.81     | 0.88          |

---

## Key Findings
1. Customers with month-to-month contracts are more likely to churn compared to those with long-term contracts.
2. High monthly charges are strongly correlated with churn.
3. Tenure is inversely related to churn—longer-tenured customers are less likely to leave.
4. Customers without dependents or partners exhibit higher churn rates.

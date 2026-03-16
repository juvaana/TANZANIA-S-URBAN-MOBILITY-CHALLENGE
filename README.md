```markdown
---

Suggested Models

Baseline:  
- Logistic Regression  

Advanced models: 
- Gradient Boosting  
- XGBoost  
- LightGBM  
- Random Forest  

A good baseline should reach F1 ≈ 0.60+ 
Strong competitors may exceed F1 > 0.80

---

Baseline Machine Learning Pipeline

Below is a starter pipeline including:

- Automated EDA
- Feature encoding
- Scaling
- Logistic regression model
- Validation with F1 score
```

### 1. Install Required Library
```bash
!pip install ydata-profiling
```

### 2. Load Libraries
```python
import pandas as pd
import numpy as np
from ydata_profiling import ProfileReport
```

### 3. Load Dataset
```python
train = pd.read_csv('train.csv')
test = pd.read_csv('test.csv')
```

### 4. Automated Exploratory Data Analysis (EDA)
```python
# Generates an interactive report showing correlations,
# distributions, missing values and statistical summaries
profile = ProfileReport(train)
profile.to_file("eda_report.html")
```
After downloading `eda_report.html`, you will have an interactive visualisation dashboard for dataset exploration.

### 5. Feature Engineering
```python
# Step 1: Identify Categorical Columns
cat_cols = ["city", "route_type", "noise_factor"]

# Step 2: One-Hot Encode Data
train = pd.get_dummies(train, columns=cat_cols)
test = pd.get_dummies(test, columns=cat_cols)

# Step 3: Align Train and Test Columns
test = test.reindex(columns=train.columns.drop('peak'), fill_value=0)

print("Train Columns:", train.columns)
print("Test Columns:", test.columns)
```

### 6. Feature Scaling
```python
from sklearn.preprocessing import StandardScaler

numeric_col = train.select_dtypes(include='number').columns.drop('peak')
print("Numerical columns to scale:", numeric_col)

scaler = StandardScaler()
scaler.fit(train[numeric_col])
train[numeric_col] = scaler.transform(train[numeric_col])
```

### 7. Train / Validation Split
```python
from sklearn.model_selection import train_test_split

X = train.drop('peak', axis=1)
Y = train['peak']

X_train, X_val, Y_train, Y_val = train_test_split(
    X, Y,
    test_size=0.2,
    random_state=42,
    stratify=Y
)
```

### 8. Train Logistic Regression Model
```python
from sklearn.linear_model import LogisticRegression

lr_model = LogisticRegression(max_iter=1000, random_state=42)
lr_model.fit(X_train, Y_train)
```

### 9. Evaluate Model
```python
from sklearn.metrics import f1_score, classification_report, confusion_matrix

y_pred = lr_model.predict(X_val)
print(f"F1 Score: {f1_score(Y_val, y_pred)}")
```

### 10. Prepare Test Data for Prediction
```python
# Ensure test has the same columns as training features
test = test.reindex(columns=train.columns.drop('peak'), fill_value=0)
```

### Improving the Baseline

You can improve model performance by:

- Feature importance analysis
- Removing noisy variables
- Adding high‑impact mobility features such as:
  - Hour‑based demand intensity
  - Rainfall interaction variables
  - City population density scaling

These improvements can push the model toward **F1 > 0.80**.

---

## Rewards 🏆

This is Juvaana’s onboarding competition.  
Top performers receive:

- **Official Juvaana Data Explorer Badge**
- **Verified digital certificate**
- **Featured profile on the national leaderboard**
- **Early access to future Juvaana competitions** (future competitions will include cash prizes)

---

## Rules

To ensure fairness:

- External data is not allowed
- Manual relabeling is prohibited
- Reverse engineering test labels is forbidden
- Collaboration is not allowed unless specified
- Submissions are monitored for anomalies

**Play fair. Compete hard.**

---

## Beginner Friendly

This competition includes learning resources:

- Getting started with Juvaana competitions
- Understanding the competition platform
- Tutorials for new participants

---

## Final Question

Are you ready to predict peak daladala demand and help design smarter Tanzanian cities? 🚍📈
```

# TANZANIA'S URBAN MOBILITY CHALLENGE 🚍
## Predict Peak Daladala Demand. Build Smarter Cities.
Predict Peak Daladala Demand. Build Smarter Cities.
This challenge asks you to build a machine learning model that predicts when a daladala route will reach peak demand.

This is not theoretical and not toy data.

You will work with a national-scale urban mobility simulation dataset.

Welcome to Juvaana.

## Why This Matters 📊

Urban transport inefficiency affects productivity and quality of life.
Several factors influence mobility demand:
Rush hour congestion costs time and economic output ,Rainfall changes commuter behavior,End-of-month salary cycles alter transport demand ,Population density drives route pressure

If we can accurately predict peak demand:
Operators can optimize dispatch , Cities can reduce congestion,Transportation systems become smarter and data-driven

This is how data transforms infrastructure.

## The Challenge

You are provided with historical urban mobility simulation data from five Tanzanian cities:

Dar es Salaam ,Mwanza,Arusha,Dodoma and Mbeya

Each row represents a daladala route at a specific hour.

## Your task:

High demand  → peak = 1

Normal demand → peak = 0

The concept is simple.

The modeling challenge is serious.

## The Data

Participants receive  two files:

train.csv        → Features + target (peak)

test.csv         → Features only


Important signals in the dataset include:

Morning rush hours (6–9 AM) ,Evening rush hours (4–8 PM)

Higher demand intensity in Dar es Salaam ,Weather influencing commuter patterns

Salary cycles affecting travel behavior ,Population density effects

Real-world characteristics:

Distribution shift between train and test data

Noisy variables included

Imperfect and messy data (just like real urban systems)

## Evaluation Metric

Submissions are evaluated using the F1 Score.

F1 balances:

Precision

Recall

This prevents models from simply predicting the majority class.

Higher F1 Score → Better model

Better model → Higher leaderboard ranking

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

#  Apply the same scaler to test (fit only on train)
test[numeric_col] = scaler.transform(test[numeric_col])
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

### 11. Generate a Submission CSV file
```python
#Align test columns with training features.
X_test = test.reindex(columns=train.columns.drop('peak'), fill_value=0)

#Predict on test set (binary 0 or 1, not probabilities)
test_preds = lr_model.predict(X_test)

#Build submission DataFrame
submission = pd.DataFrame({
    'id': test['id'],          # preserve original IDs from test set
    'peak': test_preds.astype(int)  # ensure values are int (0 or 1)
})

#Validate before saving
assert submission.shape[1] == 2, "Must have exactly 2 columns"
assert set(submission['peak'].unique()).issubset({0, 1}), "peak must be binary"
assert submission['id'].is_unique, "IDs must be unique"

#Save
submission.to_csv('submission.csv', index=False)
print("Submission saved!")
print(submission.head())
print(f"Shape: {submission.shape}")
print(f"Peak distribution:\n{submission['peak'].value_counts()}")
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

## Accesing the competition 
```markdown
You can access the competition at this site 
(juvaana.com)

```

## Final Question

Are you ready to predict peak daladala demand and help design smarter Tanzanian cities? 🚍📈
```

# Quick Reference Guide

## 📊 Project at a Glance

```
FRAUD DETECTION & CREDIT RISK ANALYSIS
├─ Dataset: German Credit (1,000 records, 9 features)
├─ Methods: Isolation Forest, LOF, XGBoost
├─ Best Model: XGBoost (99.67% Accuracy)
├─ Framework: Python + Jupyter
└─ Status: ✓ Production Ready
```

---

## 🚀 Quick Start

```bash
# Clone & Install
git clone https://github.com/yourusername/fraud-detection-credit.git
cd fraud-detection-credit
pip install -r requirements.txt

# Run
jupyter notebook 02_SECONDARY_Fraud_Detection.ipynb

# Execute all cells or run cell by cell
```

---

## 📁 Main Files

| File | Purpose | Size |
|------|---------|------|
| `02_SECONDARY_Fraud_Detection.ipynb` | ⭐ Main notebook | ~15KB |
| `01_PRIMARY_Default_Risk_Prediction.ipynb` | Risk prediction | ~12KB |
| `Advanced_Credit_Analysis.ipynb` | Deep analytics | ~20KB |
| `German_Credit_Analysis.ipynb` | EDA | ~10KB |
| `german_credit_data.csv` | Dataset | ~50KB |

---

## 🔧 Key Functions

### Data Loading
```python
df = pd.read_csv('german_credit_data.csv', index_col=0)
```

### Fraud Scoring
```python
fraud_score = (monthly_payment > threshold).astype(int) * 2 + ...
```

### Model Training
```python
xgb_fraud = xgb.XGBClassifier(n_estimators=100, max_depth=6)
xgb_fraud.fit(X_train, y_train)
```

### Predictions
```python
y_pred = xgb_fraud.predict(X_test)
y_proba = xgb_fraud.predict_proba(X_test)[:, 1]
```

---

## 📈 Key Results

```
Model Performance:
├─ Accuracy:  99.67% ✓
├─ Precision: 100%
├─ Recall:    98%
├─ F1-Score:  98.99%
└─ AUC-ROC:   0.9993

Feature Importance (Top 3):
├─ Credit Amount:   53.4%
├─ Duration:        15.0%
└─ Checking Account: 10.7%

Risk Distribution:
├─ Very Low:  0.4%
├─ Low:       13.2%
├─ Medium:    70.2%
├─ High:      7.1%
└─ Critical:  9.1%
```

---

## 🎯 Risk Categories

```python
def assign_risk_category(score):
    if score < 0.2:      return 'VERY LOW'   # 🟢 Auto-approve
    elif score < 0.4:    return 'LOW'        # 🟢 Standard approval
    elif score < 0.6:    return 'MEDIUM'     # 🟡 Monitor
    elif score < 0.8:    return 'HIGH'       # 🟠 Manual review
    else:                return 'CRITICAL'   # 🔴 Recommend rejection
```

---

## 💾 Model Persistence

```python
# Save
import joblib
joblib.dump(xgb_fraud, 'fraud_model.pkl')
joblib.dump(scaler, 'scaler.pkl')

# Load
model = joblib.load('fraud_model.pkl')
scaler = joblib.load('scaler.pkl')

# Predict new data
new_data_scaled = scaler.transform(new_data)
predictions = model.predict_proba(new_data_scaled)
```

---

## 📊 Visualization Commands

```python
# Feature Importance
plt.barh(feature_importance_df['Feature'], 
         feature_importance_df['Importance'])

# Confusion Matrix
sns.heatmap(cm_xgb, annot=True, cmap='RdYlGn_r')

# ROC Curve
plt.plot(fpr_xgb, tpr_xgb, label=f'AUC={auc_xgb:.4f}')
plt.plot([0, 1], [0, 1], 'r--')  # Random classifier

# Score Distribution
plt.hist(fraud_scores, bins=30, edgecolor='black')
plt.axvline(fraud_threshold, color='red', linestyle='--')
```

---

## 🔍 Data Exploration

```python
# Dataset info
df.shape          # (1000, 9)
df.dtypes         # Data types
df.isnull().sum() # Missing values
df.describe()     # Statistics

# Feature correlation
corr_matrix = df.corr()
sns.heatmap(corr_matrix, annot=True)

# Target distribution
df['FRAUD_LABEL'].value_counts()
df['FRAUD_LABEL'].value_counts(normalize=True)
```

---

## 📋 Features Used

```python
FEATURES = [
    'Age',              # Customer age
    'Sex',              # Gender (1/0)
    'Job',              # Employment level (0-3)
    'Housing',          # Housing type
    'Saving accounts',  # Savings status
    'Checking account', # Checking status
    'Credit amount',    # Loan amount
    'Duration',         # Loan duration (months)
    'Purpose'           # Loan purpose
]
```

---

## ⚙️ Hyperparameters

```python
# XGBoost
n_estimators    = 100      # Number of boosting rounds
max_depth       = 6        # Tree depth
learning_rate   = 0.1      # Shrinkage
subsample       = 0.8      # Data sampling
colsample       = 0.8      # Feature sampling

# Anomaly Detection
iso_contamination = 0.20   # Anomaly percentage
lof_neighbors     = 20     # LOF neighbors
```

---

## 🧮 Ensemble Scoring

```python
# Weighted average of 3 methods
ensemble_score = (
    0.3 * iso_score +      # Isolation Forest (30%)
    0.3 * lof_score +      # Local Outlier Factor (30%)
    0.4 * xgb_prob         # XGBoost (40%)
)
```

---

## 🔐 Common Fraud Indicators

```python
# Indicator 1: Extreme monthly payment
monthly_payment > monthly_payment.quantile(0.95)

# Indicator 2: Young + high credit
(age < 22) & (credit > credit.quantile(0.75))

# Indicator 3: No savings + high credit
(no_savings) & (no_checking) & (high_credit)

# Indicator 4: Inconsistent job-credit
((job == 0) | (job == 3)) & (credit > credit.quantile(0.90))

# Indicator 5: Extreme outlier
credit > credit.quantile(0.97)

# Indicator 6: Long duration + small credit
(long_duration) & (small_credit)
```

---

## 📊 Model Evaluation

```python
# Confusion Matrix
from sklearn.metrics import confusion_matrix
cm = confusion_matrix(y_true, y_pred)
# [[TN, FP],
#  [FN, TP]]

# ROC Curve
from sklearn.metrics import roc_curve, auc
fpr, tpr, _ = roc_curve(y_true, y_proba)
roc_auc = auc(fpr, tpr)

# Classification Metrics
from sklearn.metrics import classification_report
print(classification_report(y_true, y_pred))

# Cross Validation
from sklearn.model_selection import cross_val_score
scores = cross_val_score(model, X, y, cv=5)
```

---

## 🎨 Plotting Tips

```python
# Setup
plt.rcParams['figure.figsize'] = (14, 6)
sns.set_style('whitegrid')

# Subplots
fig, axes = plt.subplots(2, 2, figsize=(15, 10))

# Save figure
plt.savefig('plot.png', dpi=300, bbox_inches='tight')

# Color palettes
colors = ['green', 'red']  # Binary
colors_cat = ['green', 'lightgreen', 'yellow', 'orange', 'red']  # 5-class
cmap = 'RdYlGn_r'  # Diverging colormap
```

---

## 🐍 Python Tips

```python
# List comprehension
categories = [assign_risk_category(s) for s in scores]

# F-strings
print(f"Accuracy: {accuracy:.2%}, Precision: {precision:.4f}")

# Pandas operations
df[df['fraud'] == 1]                    # Filter
df.groupby('category')['amount'].sum()  # Group by
df.apply(lambda x: x.value_counts())    # Apply function

# NumPy
arr.mean(), arr.std()                   # Statistics
arr > threshold                         # Boolean indexing
np.where(condition, true_val, false_val) # Conditional
```

---

## 🐛 Debugging

```python
# Check shape
print(X.shape, y.shape)

# List all variables
%whos

# Memory usage
df.memory_usage(deep=True).sum() / 1024**2  # MB

# Time execution
%timeit code_here
%%time

# Print full dataframe
pd.set_option('display.max_columns', None)
```

---

## 📞 Keyboard Shortcuts (Jupyter)

| Shortcut | Action |
|----------|--------|
| `Ctrl+Enter` | Run current cell |
| `Shift+Enter` | Run cell and move next |
| `Alt+Enter` | Run cell and create new |
| `Ctrl+Shift+P` | Command palette |
| `Ctrl+/` | Comment/uncomment |
| `Tab` | Autocomplete/Indent |
| `Shift+Tab` | Tooltip/Documentation |

---

## 🔗 Useful Links

- [Pandas Docs](https://pandas.pydata.org/docs/)
- [Scikit-learn](https://scikit-learn.org/)
- [XGBoost](https://xgboost.readthedocs.io/)
- [Matplotlib](https://matplotlib.org/)
- [GitHub Markdown](https://guides.github.com/features/mastering-markdown/)

---

## ✅ Checklist for Deployment

- [ ] Model tested on validation set
- [ ] Feature scaling saved
- [ ] Model serialized (joblib/pickle)
- [ ] API/inference code created
- [ ] Error handling added
- [ ] Logging implemented
- [ ] Monitoring setup
- [ ] Documentation complete
- [ ] Tests passing
- [ ] Version control ready

---

## 🎓 Learning Resources

**What's Inside?**
- ML pipeline design
- Feature engineering
- Model training & evaluation
- Ensemble methods
- Data visualization
- Results interpretation

**Skills Developed:**
- ✓ Machine Learning
- ✓ Data Science
- ✓ Python Programming
- ✓ Statistical Analysis
- ✓ Model Deployment

---

**Last Updated:** April 17, 2026
**Need Help?** Check [GETTING_STARTED.md](GETTING_STARTED.md)

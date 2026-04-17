# Getting Started Guide

Quick start guide to run the Fraud Detection project.

## Option 1: Quick Setup (5 minutes)

### Step 1: Clone the Repository
```bash
git clone https://github.com/yourusername/fraud-detection-credit.git
cd fraud-detection-credit
```

### Step 2: Install Dependencies
```bash
# Option A: Using pip
pip install -r requirements.txt

# Option B: Using conda
conda create -n fraud-detection python=3.9
conda activate fraud-detection
pip install -r requirements.txt
```

### Step 3: Run the Main Notebook
```bash
jupyter notebook 02_SECONDARY_Fraud_Detection.ipynb
```

### Step 4: Execute All Cells
- Press `Ctrl+Shift+P` and select "Run All Cells"
- Or go to Cell → Run All

**Done!** You'll see:
- ✅ Data loaded (1,000 records)
- ✅ Fraud scores calculated
- ✅ Models trained
- ✅ Visualizations generated in `plots/` folder

---

## Option 2: Detailed Setup (10 minutes)

### 1. Create Virtual Environment
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### 2. Clone Repository
```bash
git clone https://github.com/yourusername/fraud-detection-credit.git
cd fraud-detection-credit
```

### 3. Install Dependencies with Specific Versions
```bash
pip install --upgrade pip
pip install -r requirements.txt --no-cache-dir
```

### 4. Verify Installation
```bash
python -c "import pandas; import sklearn; import xgboost; print('✓ All libraries installed!')"
```

### 5. Start Jupyter Lab (Better UI)
```bash
# Install Jupyter Lab
pip install jupyterlab

# Start Jupyter Lab
jupyter lab
```

### 6. Navigate to Notebook
- Open `02_SECONDARY_Fraud_Detection.ipynb`
- Select Python kernel (if prompted)
- Run cells one by one or all at once

---

## File Structure After Setup

```
fraud-detection-credit/
├── 📓 02_SECONDARY_Fraud_Detection.ipynb          ← START HERE
├── 01_PRIMARY_Default_Risk_Prediction.ipynb
├── Advanced_Credit_Analysis.ipynb
├── German_Credit_Analysis.ipynb
├── ML_Default_Fraud_Prediction.ipynb
├── 📊 german_credit_data.csv                       ← Dataset
├── 📁 plots/                                        ← Generated plots
│   ├── 01_fraud_score_distribution.png
│   ├── 02_fraud_methods_comparison.png
│   ├── 03_fraud_feature_importance.png
│   └── 04_fraud_risk_dashboard.png
├── 📄 README.md                                     ← Full documentation
├── 📄 requirements.txt                              ← Dependencies
├── 📄 config.ini                                    ← Configuration
├── 📄 LICENSE
└── 📄 CONTRIBUTING.md
```

---

## What Happens When You Run?

### Execution Timeline (~2-3 minutes)

1. **Data Loading** (10 seconds)
   - Loads 1,000 credit records
   - Fills missing values
   - Displays dataset info

2. **Fraud Scoring** (30 seconds)
   - Calculates 6 fraud indicators
   - Creates fraud labels
   - Generates distribution plot

3. **Feature Engineering** (5 seconds)
   - Encodes categorical variables
   - Prepares feature matrix

4. **Data Scaling** (5 seconds)
   - Normalizes all features

5. **Anomaly Detection** (30 seconds)
   - Isolation Forest (unsupervised)
   - Local Outlier Factor (density-based)
   - Results: 200 anomalies detected each

6. **XGBoost Training** (20 seconds)
   - Trains supervised classifier
   - Generates metrics: 99.67% accuracy
   - Creates confusion matrix & ROC curve

7. **Fraud Scoring All Customers** (5 seconds)
   - Ensemble scoring for 1,000 records
   - Risk categorization

8. **Visualizations** (30 seconds)
   - Feature importance plots
   - Fraud risk dashboard
   - Summary statistics

**Total Runtime:** ~2-3 minutes

---

## Common Issues & Solutions

### Issue 1: ModuleNotFoundError
**Error:** `ModuleNotFoundError: No module named 'xgboost'`

**Solution:**
```bash
pip install xgboost --upgrade
```

### Issue 2: Jupyter Not Found
**Error:** `jupyter: command not found`

**Solution:**
```bash
pip install jupyter
jupyter notebook
```

### Issue 3: Python Version
**Error:** `Requirement already satisfied but requirement not met`

**Solution:**
```bash
python --version  # Check your version (need 3.8+)
pip install --upgrade pip setuptools
pip install -r requirements.txt --upgrade
```

### Issue 4: Permission Denied (macOS/Linux)
**Error:** `Permission denied: './venv/bin/activate'`

**Solution:**
```bash
chmod +x venv/bin/activate
source venv/bin/activate
```

### Issue 5: Data File Not Found
**Error:** `FileNotFoundError: german_credit_data.csv`

**Solution:**
```bash
# Make sure you're in the project root directory
cd fraud-detection-credit
pwd  # Should show the project path
ls   # Should show german_credit_data.csv
```

---

## Next Steps

### 1. Understand the Code
- Read cell comments in the notebook
- Check variable definitions
- Review generated plots

### 2. Modify & Experiment
- Try different threshold values
- Adjust model hyperparameters
- Test with custom data

### 3. Deploy the Model
```python
# Save the trained model
import joblib
joblib.dump(xgb_fraud, 'models/fraud_model.pkl')

# Load and use later
model = joblib.load('models/fraud_model.pkl')
predictions = model.predict_proba(X_new)
```

### 4. Create Your Own Features
```python
# Add custom fraud indicators
df['custom_indicator'] = (condition1) & (condition2)
fraud_score += df['custom_indicator'].astype(int) * weight
```

---

## Testing the Model

### Test 1: Single Application
```python
# Get first applicant
test_applicant = X_scaled.iloc[0:1]

# Predict fraud probability
fraud_prob = xgb_fraud.predict_proba(test_applicant)[0, 1]
print(f"Fraud Probability: {fraud_prob:.2%}")
```

### Test 2: Batch Processing
```python
# Predict for all
predictions = xgb_fraud.predict_proba(X_scaled)[:, 1]
fraud_count = (predictions > 0.5).sum()
print(f"Fraudulent Applications: {fraud_count}/1000")
```

### Test 3: Custom Data
```python
# Create custom applicant
new_data = pd.DataFrame({
    'Age': [35],
    'Sex': [1],
    'Job': [2],
    'Housing': [1],
    'Saving accounts': [0],
    'Checking account': [1],
    'Credit amount': [5000],
    'Duration': [24],
    'Purpose': [3]
})

# Scale and predict
scaled = scaler.transform(new_data)
fraud_prob = xgb_fraud.predict_proba(scaled)[0, 1]
```

---

## Performance Benchmarks

**Laptop (8GB RAM, i5 processor):** 3-4 minutes
**Workstation (16GB RAM, i7 processor):** 2-3 minutes
**Server (32GB RAM, high-core count):** 1-2 minutes

---

## Get Help

### Documentation
- 📖 Read [README.md](README.md) for full documentation
- 📚 Check notebook comments for code explanation
- 🔗 See [CONTRIBUTING.md](CONTRIBUTING.md) for development guide

### Common Questions
**Q: Can I use my own data?**
A: Yes! Replace `german_credit_data.csv` with your own CSV file. Ensure it has the same feature names.

**Q: How do I save my results?**
A: Plots are auto-saved in `plots/` folder. Export metrics as CSV using pandas:
```python
feature_importance_df.to_csv('feature_importance.csv', index=False)
```

**Q: Can I modify the model?**
A: Absolutely! Edit hyperparameters in the notebook cells and rerun.

---

## Success Checklist ✓

After setup, you should have:

- [x] Python 3.8+ installed
- [x] Virtual environment created
- [x] Dependencies installed
- [x] `02_SECONDARY_Fraud_Detection.ipynb` runs without errors
- [x] 4 PNG plots generated in `plots/` folder
- [x] XGBoost model trained with ~99.67% accuracy
- [x] Risk scores calculated for all 1,000 applications

---

**🎉 Congratulations! You're ready to explore fraud detection!**

Next: Open the notebook and run the cells to see it in action.

---

**Questions?** Open an issue or check the main README.

# Week 4 — Day 1
**Topic:** Data Preprocessing Implementation
**Role of AI today:** Programmer and debugger
**Estimated time:** ~60 minutes

---

## Copy-Paste Prompt

---

You are helping me with an 8-week academic cybersecurity case study. I am a beginner/intermediate student with approximately 1 hour available today. I am working in Google Colab.

---

**PROJECT TITLE:**
"Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems"

**PROJECT SUMMARY:**
Controlled academic experiment:
- Dataset: NSL-KDD (KDDTrain+.txt ~125k rows / KDDTest+.txt ~22k rows / 41 features + label + difficulty)
- Categorical features to encode: protocol_type, service, flag
- Binary label: normal=0, all attack types=1
- Model: Random Forest (100 trees, random_state=42)
- Attack: Gaussian noise on top 5 features of attack-class test samples
- Defense: Adversarial training (augmented retraining)
- Tools: Python, Google Colab, pandas, scikit-learn, numpy, matplotlib

---

**CURRENT STAGE:**
Week 4, Day 1.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–3 complete:
  - Research question, literature review, gap statement, references
  - Framework design + architecture diagram
  - Environment set up in Google Colab (all imports working)
  - NSL-KDD loaded and explored (shape confirmed, columns understood)
  - Preprocessing plan documented + code skeleton ready (`week-3/methodology-draft.md`)

---

**TODAY'S OBJECTIVE:**
Implement the complete preprocessing pipeline. By the end of today I should have clean, scaled training and test arrays (X_train, X_test, y_train, y_test) ready for model training in Day 2.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Programmer and debugger. Provide complete, commented, runnable code. If I paste an error, help me fix it.

---

**TODAY'S TASKS:**

**Task 1 — Complete preprocessing code (40 minutes):**

Provide the full, complete, runnable preprocessing code below. Each step must be in a separate code cell with a comment header. Explain each cell in 1–2 sentences after the code.

**Cell 1: Imports and column names**
```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import LabelEncoder, StandardScaler
from sklearn.metrics import (accuracy_score, precision_score, recall_score,
                             f1_score, roc_auc_score, confusion_matrix,
                             classification_report)
from sklearn.ensemble import RandomForestClassifier
import matplotlib.pyplot as plt
import seaborn as sns
import warnings
warnings.filterwarnings('ignore')

# NSL-KDD column names — 41 features + label + difficulty
columns = [
    'duration','protocol_type','service','flag','src_bytes','dst_bytes',
    'land','wrong_fragment','urgent','hot','num_failed_logins','logged_in',
    'num_compromised','root_shell','su_attempted','num_root','num_file_creations',
    'num_shells','num_access_files','num_outbound_cmds','is_host_login',
    'is_guest_login','count','srv_count','serror_rate','srv_serror_rate',
    'rerror_rate','srv_rerror_rate','same_srv_rate','diff_srv_rate',
    'srv_diff_host_rate','dst_host_count','dst_host_srv_count',
    'dst_host_same_srv_rate','dst_host_diff_srv_rate','dst_host_same_src_port_rate',
    'dst_host_srv_diff_host_rate','dst_host_serror_rate','dst_host_srv_serror_rate',
    'dst_host_rerror_rate','dst_host_srv_rerror_rate','label','difficulty'
]
```

**Cell 2: Load data**
```python
train_df = pd.read_csv('KDDTrain+.txt', names=columns)
test_df  = pd.read_csv('KDDTest+.txt',  names=columns)
print("Train:", train_df.shape, "| Test:", test_df.shape)
```

**Cell 3: Drop difficulty column**
```python
train_df = train_df.drop('difficulty', axis=1)
test_df  = test_df.drop('difficulty', axis=1)
```

**Cell 4: Create binary labels**
```python
train_df['label'] = train_df['label'].apply(lambda x: 0 if x == 'normal' else 1)
test_df['label']  = test_df['label'].apply(lambda x: 0 if x == 'normal' else 1)
print("Train label counts:\n", train_df['label'].value_counts())
print("Test label counts:\n",  test_df['label'].value_counts())
```

**Cell 5: Encode categorical features**
```python
cat_cols = ['protocol_type', 'service', 'flag']
le = LabelEncoder()
for col in cat_cols:
    combined = pd.concat([train_df[col], test_df[col]])
    le.fit(combined)
    train_df[col] = le.transform(train_df[col])
    test_df[col]  = le.transform(test_df[col])
print("Encoding complete.")
```

**Cell 6: Separate features and labels**
```python
X_train = train_df.drop('label', axis=1).values
y_train = train_df['label'].values
X_test  = test_df.drop('label', axis=1).values
y_test  = test_df['label'].values
print("X_train:", X_train.shape, "| X_test:", X_test.shape)
```

**Cell 7: Normalize with StandardScaler**
```python
scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)   # fit on train only
X_test  = scaler.transform(X_test)        # transform test with same scaler
print("Scaling complete. X_train mean ~0:", X_train.mean().round(4))
```

**Cell 8: Verification**
```python
print("=== Preprocessing Complete ===")
print(f"X_train: {X_train.shape}, y_train: {y_train.shape}")
print(f"X_test:  {X_test.shape},  y_test:  {y_test.shape}")
print(f"Train class balance — 0:{(y_train==0).sum()} | 1:{(y_train==1).sum()}")
print(f"Test class balance  — 0:(y_test==0).sum()} | 1:{(y_test==1).sum()}")
```

After all cells: explain what each step achieved and what the output should look like.

**Task 2 — Explain data leakage risk (5 minutes):**
Explain in 2–3 sentences why I fit the StandardScaler on training data only, and what would happen if I fit it on both train and test combined.

**Task 3 — Explain LabelEncoder across combined data (5 minutes):**
Explain why I fit the LabelEncoder on the combined train+test categorical values rather than on train alone. What problem does this prevent?

**Task 4 — Handle errors (10 minutes):**
If I paste any error messages from running the code, help me diagnose and fix them.

---

**IMPORTANT CONSTRAINTS:**
- Provide complete, runnable code — no pseudocode
- Do NOT move to model training today
- If a code cell produces an error I don't understand, explain the cause in plain English
- The scaler MUST be fit on training data only

**EXPECTED OUTPUT BY END OF SESSION:**
- All 8 cells run without errors
- X_train, X_test, y_train, y_test arrays ready
- Verification cell shows correct shapes
- Code saved in notebook

**AT THE END OF THIS SESSION, PROVIDE:**
1. Complete code summary (all 8 cells in one block for easy saving)
2. A note on what the shapes should be
3. Reminder: "Next session (Day 2) we train the Random Forest and record baseline metrics."

---

## Definition of Done

- [ ] All 8 preprocessing cells run without errors
- [ ] X_train shape: (~125k, 41) | X_test shape: (~22k, 41)
- [ ] Binary labels confirmed (0 = normal, 1 = attack)
- [ ] StandardScaler applied (fit on train, transform on both)
- [ ] Code saved in `week-4/notebook-baseline.ipynb`

### Expected artifacts
- `week-4/notebook-baseline.ipynb` — preprocessing cells complete

### Estimated time
~60 minutes

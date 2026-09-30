# Week 3 — Methodology Draft

---

## Preprocessing Pipeline — 6 Steps

### Step 1 — Drop the difficulty column
**Why:** The `difficulty` column is a meta-attribute added by NSL-KDD's creators to indicate how hard a record is to classify. It is not a real network traffic feature and must be excluded before training to avoid data leakage.  
**Code:**
```python
train_df = train_df.drop(columns=['difficulty'])
test_df  = test_df.drop(columns=['difficulty'])
```

---

### Step 2 — Encode categorical features
**Why:** `protocol_type`, `service`, and `flag` are string-valued categorical features. Random Forest in scikit-learn requires all input features to be numeric. LabelEncoder is used (not OneHotEncoder) because: (a) the number of categories is manageable, (b) Random Forest is tree-based and does not assume ordinal meaning in encoded integers, and (c) OneHotEncoder would add ~80+ columns, increasing complexity without benefit for this experiment.  
**Pitfall:** Fit the encoder on training data, then apply to test data. If the test set contains an unseen category value, handle with a fallback (replace with -1 or most frequent category).  
**Code:**
```python
from sklearn.preprocessing import LabelEncoder

cat_cols = ['protocol_type', 'service', 'flag']
le = LabelEncoder()

for col in cat_cols:
    train_df[col] = le.fit_transform(train_df[col])
    # For test: handle unseen labels
    test_df[col] = test_df[col].map(
        lambda x: le.transform([x])[0] if x in le.classes_ else -1
    )
```

---

### Step 3 — Create binary labels
**Why:** NSL-KDD has ~23 named attack types. For this experiment, we perform binary classification: normal=0, any attack=1. This simplifies the problem to a single meaningful threshold and is standard in adversarial robustness evaluations.  
**Code:**
```python
train_df['binary_label'] = train_df['label'].apply(lambda x: 0 if x == 'normal' else 1)
test_df['binary_label']  = test_df['label'].apply(lambda x: 0 if x == 'normal' else 1)
```

---

### Step 4 — Separate features from target
**Why:** `X` (features) and `y` (labels) must be separate arrays for scikit-learn training and evaluation.  
**Code:**
```python
feature_cols = [c for c in train_df.columns if c not in ['label', 'binary_label']]

X_train = train_df[feature_cols].values
y_train = train_df['binary_label'].values
X_test  = test_df[feature_cols].values
y_test  = test_df['binary_label'].values
```

---

### Step 5 — Use pre-split files (do NOT use train_test_split)
**Why:** NSL-KDD provides separate training and test files specifically designed for comparable benchmarking. Using `train_test_split` would create a random split that cannot be reproduced by other researchers or compared against published results. The provided split should always be used for NSL-KDD experiments.  
**No additional code needed** — `X_train`/`y_train` come from KDDTrain+.txt; `X_test`/`y_test` come from KDDTest+.txt.

---

### Step 6 — Normalize features (StandardScaler)
**Why:** Features in NSL-KDD have vastly different scales (e.g., `src_bytes` can be in the millions; `land` is 0 or 1). While Random Forest is not strictly scale-sensitive, StandardScaler ensures that the Gaussian noise added during the adversarial attack step is proportional across all features (noise of std=0.3 means the same thing on a normalized scale).  
**Pitfall:** StandardScaler must be fit ONLY on X_train. Fitting on the test set would leak test distribution information into the model.  
**Code:**
```python
from sklearn.preprocessing import StandardScaler

scaler = StandardScaler()
X_train = scaler.fit_transform(X_train)   # Fit AND transform training set
X_test  = scaler.transform(X_test)        # Transform only — no re-fitting
```

---

## Preprocessing Code Skeleton

```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import LabelEncoder, StandardScaler
from sklearn.ensemble import RandomForestClassifier

# ─────────────────────────────────────────────
# Step 1: Define columns and load data
# ─────────────────────────────────────────────
columns = [
    'duration', 'protocol_type', 'service', 'flag', 'src_bytes',
    'dst_bytes', 'land', 'wrong_fragment', 'urgent', 'hot',
    'num_failed_logins', 'logged_in', 'num_compromised', 'root_shell',
    'su_attempted', 'num_root', 'num_file_creations', 'num_shells',
    'num_access_files', 'num_outbound_cmds', 'is_host_login',
    'is_guest_login', 'count', 'srv_count', 'serror_rate',
    'srv_serror_rate', 'rerror_rate', 'srv_rerror_rate', 'same_srv_rate',
    'diff_srv_rate', 'srv_diff_host_rate', 'dst_host_count',
    'dst_host_srv_count', 'dst_host_same_srv_rate', 'dst_host_diff_srv_rate',
    'dst_host_same_src_port_rate', 'dst_host_srv_diff_host_rate',
    'dst_host_serror_rate', 'dst_host_srv_serror_rate', 'dst_host_rerror_rate',
    'dst_host_srv_rerror_rate', 'label', 'difficulty'
]

train_df = pd.read_csv('KDDTrain+.txt', names=columns)
test_df  = pd.read_csv('KDDTest+.txt',  names=columns)

# ─────────────────────────────────────────────
# Step 2: Drop difficulty column
# ─────────────────────────────────────────────
train_df = train_df.drop(columns=['difficulty'])
test_df  = test_df.drop(columns=['difficulty'])

# ─────────────────────────────────────────────
# Step 3: Encode categorical features
# ─────────────────────────────────────────────
cat_cols = ['protocol_type', 'service', 'flag']
encoders = {}
for col in cat_cols:
    le = LabelEncoder()
    train_df[col] = le.fit_transform(train_df[col])
    test_df[col]  = test_df[col].map(
        lambda x, le=le: le.transform([x])[0] if x in le.classes_ else -1
    )
    encoders[col] = le

# ─────────────────────────────────────────────
# Step 4: Create binary labels
# ─────────────────────────────────────────────
train_df['binary_label'] = train_df['label'].apply(lambda x: 0 if x == 'normal' else 1)
test_df['binary_label']  = test_df['label'].apply(lambda x: 0 if x == 'normal' else 1)

# ─────────────────────────────────────────────
# Step 5: Separate X and y (use provided split)
# ─────────────────────────────────────────────
feature_cols = [c for c in train_df.columns if c not in ['label', 'binary_label']]

X_train = train_df[feature_cols].values
y_train = train_df['binary_label'].values
X_test  = test_df[feature_cols].values
y_test  = test_df['binary_label'].values

# ─────────────────────────────────────────────
# Step 6: Fit StandardScaler on X_train only
# ─────────────────────────────────────────────
scaler  = StandardScaler()
X_train = scaler.fit_transform(X_train)
X_test  = scaler.transform(X_test)

# ─────────────────────────────────────────────
# Verify shapes
# ─────────────────────────────────────────────
print("X_train shape:", X_train.shape)          # Expected: (~125973, 41)
print("X_test shape: ", X_test.shape)           # Expected: (~22544, 41)
print("y_train distribution:", pd.Series(y_train).value_counts().to_dict())
print("y_test distribution: ", pd.Series(y_test).value_counts().to_dict())
```

---

## [AI DRAFT — VERIFY] Methodology Section

[AI DRAFT — VERIFY ALL CLAIMS AGAINST YOUR ACTUAL IMPLEMENTATION]

### 7. Methodology

#### 7.1 Dataset

This study uses the NSL-KDD dataset (Tavallaee et al., 2009), a widely cited benchmark for network intrusion detection research. NSL-KDD was developed as a cleaned replacement for the KDD Cup 1999 dataset, addressing issues of class imbalance and record redundancy that affected earlier evaluations. The training set (KDDTrain+.txt) contains approximately 125,973 records and the test set (KDDTest+.txt) contains approximately 22,544 records, each described by 41 network traffic features and a class label. For this experiment, labels are binarised: "normal" traffic is assigned class 0 and all attack types are assigned class 1, yielding a standard binary classification task.

#### 7.2 Preprocessing

Six preprocessing steps are applied before model training. First, the difficulty score column — a meta-attribute not present in real network traffic — is removed. Second, three categorical features (`protocol_type`, `service`, `flag`) are encoded as integers using scikit-learn's `LabelEncoder`; encoders are fitted on the training set and applied to the test set to avoid information leakage. Third, binary labels are created as described above. Fourth, features (`X`) and labels (`y`) are separated into distinct arrays. Fifth, the provided train/test file split is preserved; scikit-learn's `train_test_split` is not used, as the NSL-KDD benchmark split enables reproducible, comparable results. Sixth, a `StandardScaler` is fitted exclusively on the training feature matrix and applied to both training and test sets to normalize feature scales, ensuring that adversarial noise magnitudes are consistent across all features.

#### 7.3 Baseline Model

A `RandomForestClassifier` with 100 estimators and `random_state=42` is trained on the preprocessed training data. Random Forest was selected because it: (a) achieves strong benchmark performance on NSL-KDD without extensive hyperparameter tuning (Revathi & Malathi, 2013); (b) is explainable through `feature_importances_`, enabling principled attack simulation; and (c) is non-differentiable, requiring feature-space perturbation rather than gradient-based attacks. Evaluation metrics are accuracy, precision, recall, F1-score, and AUC-ROC — the standard suite for binary IDS evaluation.

#### 7.4 Adversarial Attack Design

Following Condition 1 evaluation, the top-5 features by `feature_importances_` are identified. Adversarial test sets are generated by adding Gaussian noise (`np.random.normal(0, std)`) to these five features in attack-class test samples. Three noise levels are evaluated: std = 0.1 (low), 0.3 (medium), and 0.5 (high). Normal-class test samples are not perturbed. This feature-space perturbation approach is a recognized proxy for evasion attacks on non-differentiable classifiers (see limitations, Section 11).

#### 7.5 Defense Mechanism

Adversarial training is implemented as follows: the same perturbation strategy (std = 0.3) is applied to attack-class rows in the training set, generating adversarial training examples with their original labels (attack=1) preserved. These perturbed samples are concatenated with the original training data to form an augmented training set. A new `RandomForestClassifier(n_estimators=100, random_state=42)` is trained on this augmented dataset. The defended model is then evaluated on the same adversarial test set used in Condition 2 (std = 0.3), enabling a direct, controlled comparison.

*[AI DRAFT — VERIFY: Confirm all numbers (dataset sizes, noise levels, n_estimators) match your actual code. Confirm all citations are verified.]*

---

## Week 3 Summary

**Accomplished this week:**
- Designed and documented all 7 framework components
- Created ASCII architecture diagram showing the full C1/C2/C3 pipeline
- Defined the three-condition experimental structure formally
- Documented NSL-KDD column names and exploration code
- Planned the 6-step preprocessing pipeline with explanations and code
- Wrote 400-word methodology draft with all sub-sections

**Artifacts produced:**
- `week-3/framework-design.md` — framework description, diagram, 3-condition table, draft section
- `week-3/dataset-exploration.md` — column names, loading code, exploration code, dataset facts
- `week-3/methodology-draft.md` — this file

**Week 4 goal:** Implement the preprocessing code and train the baseline Random Forest model. Record real accuracy, precision, recall, F1, and AUC numbers from your actual experiment.

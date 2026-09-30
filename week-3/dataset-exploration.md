# Week 3 — Dataset Exploration Notes

---

## Environment Setup

### Required imports (run first in Colab)

```python
import pandas as pd
import numpy as np
from sklearn.ensemble import RandomForestClassifier
from sklearn.preprocessing import LabelEncoder, StandardScaler
from sklearn.model_selection import train_test_split
from sklearn.metrics import (accuracy_score, precision_score, recall_score,
                             f1_score, roc_auc_score, classification_report,
                             confusion_matrix, ConfusionMatrixDisplay, RocCurveDisplay)
import matplotlib.pyplot as plt
import seaborn as sns
print("All imports successful.")
```

All listed libraries are pre-installed in Google Colab. No `pip install` required.

---

## NSL-KDD Dataset

**Files needed:**
- `KDDTrain+.txt` — training set (~125,973 records)
- `KDDTest+.txt` — test set (~22,544 records)

**Download source:** https://www.unb.ca/cic/datasets/nsl.html  
*Verify this URL yourself before downloading. Backup: search "NSL-KDD dataset" on Kaggle.*

**Important:** Both files have NO header row. Column names must be supplied manually.

---

## NSL-KDD Column Names (43 columns)

```python
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
```

*Feature columns: indices 0–40 (41 features)*  
*Label column: index 41*  
*Difficulty score: index 42 (drop before training)*

---

## Data Loading Code

```python
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

# Load training and test data (no header in files)
train_df = pd.read_csv('KDDTrain+.txt', names=columns)
test_df  = pd.read_csv('KDDTest+.txt',  names=columns)

print("Train shape:", train_df.shape)   # Expected: (~125973, 43)
print("Test shape: ", test_df.shape)    # Expected: (~22544, 43)
train_df.head(3)
```

---

## Dataset Exploration Code

### Cell 1 — Data types
```python
print(train_df.dtypes)
# Expected: protocol_type, service, flag are 'object' (string)
# All others should be int64 or float64
```

### Cell 2 — Null values
```python
print(train_df.isnull().sum().sum())
# Expected: 0 — NSL-KDD has no missing values after standard loading
```

### Cell 3 — Label distribution
```python
print(train_df['label'].value_counts())
# Expected: "normal" is one class; many named attack types (neptune, smurf, etc.)
# This confirms multi-class labels that we will binarize to 0/1
```

### Cell 4 — Categorical feature unique values
```python
for col in ['protocol_type', 'service', 'flag']:
    print(f"\n{col} ({train_df[col].nunique()} unique):")
    print(train_df[col].unique())
# protocol_type: ~3 values (tcp, udp, icmp)
# service: ~70 values (http, ftp, smtp, etc.)
# flag: ~11 values (SF, S0, REJ, etc.)
```

### Cell 5 — Sample numerical feature statistics
```python
train_df[['duration','src_bytes','dst_bytes','wrong_fragment','urgent']].describe()
# Shows range, mean, std for 5 numerical features
# Note: src_bytes and dst_bytes have very wide ranges — confirms normalization is needed
```

---

## Key Dataset Facts

| Property | Training set | Test set |
|---|---|---|
| Rows | ~125,973 | ~22,544 |
| Columns | 43 (41 features + label + difficulty) | 43 |
| Categorical features | 3 (protocol_type, service, flag) | Same |
| Numerical features | 38 | Same |
| Null values | 0 | 0 |
| Unique label values | ~23 (normal + 22 attack types) | ~38 (includes new attack types) |
| Binary class balance | ~53% normal, ~47% attack (training) | ~43% normal, ~57% attack (test) |

**Important note on test set:** The NSL-KDD test set (KDDTest+.txt) includes some attack types not present in the training set. For binary classification (normal=0, attack=1), this does not affect the experiment — all attack types map to label 1.

---

*Artifact created: Week 3, Day 2*  
*Next session (Day 3): Plan preprocessing steps and write methodology draft*

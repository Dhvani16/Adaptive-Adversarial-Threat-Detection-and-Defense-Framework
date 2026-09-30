# Week 3 — Day 2
**Topic:** Environment Setup and Dataset Exploration
**Role of AI today:** Technical guide and programmer
**Estimated time:** ~60 minutes

---

## Copy-Paste Prompt

---

You are helping me with an 8-week academic cybersecurity case study. I am a beginner/intermediate student with approximately 1 hour available today.

---

**PROJECT TITLE:**
"Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems"

**PROJECT SUMMARY:**
Controlled academic experiment using:
- Dataset: NSL-KDD (KDDTrain+.txt and KDDTest+.txt)
- Model: Random Forest classifier (scikit-learn)
- Attack: Gaussian noise on top 5 features of attack-class test samples
- Defense: Adversarial training (augmented retraining)
- Tools: Python, Google Colab, pandas, scikit-learn, numpy, matplotlib
- Output: Academic case study report (~4,000–5,000 words)

---

**CURRENT STAGE:**
Week 3, Day 2.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–2 complete: research question, literature review, reference list
- Week 3 Day 1 complete:
  - All 7 framework components defined
  - ASCII architecture diagram created
  - Three-condition experimental table written
  - 400-word [AI DRAFT] framework section written
  - Saved in `week-3/framework-design.md`

---

**TODAY'S OBJECTIVE:**
Set up the technical environment (Google Colab), download the NSL-KDD dataset, load it into Python, and explore its structure. By the end of today I should have a working notebook that loads the data, shows its shape, and confirms the feature names — ready for preprocessing next session.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Technical guide and programmer. Walk me through each setup step. Provide exact code I can run in Colab. Explain what each step does.

---

**TODAY'S TASKS:**

**Task 1 — Environment setup (10 minutes):**

Walk me through setting up a new Google Colab notebook:
1. How to open a new notebook at colab.research.google.com
2. How to install any libraries that are not pre-installed (check if pandas, scikit-learn, numpy, matplotlib are available)
3. How to mount Google Drive if I want to save files persistently
4. Give me a cell I can run to verify all imports work:

```python
import pandas as pd
import numpy as np
from sklearn.ensemble import RandomForestClassifier
from sklearn.preprocessing import LabelEncoder, StandardScaler
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score, classification_report, roc_auc_score
import matplotlib.pyplot as plt
print("All imports successful.")
```

**Task 2 — NSL-KDD dataset guidance (10 minutes):**

Tell me:
1. What the NSL-KDD dataset files are called (KDDTrain+.txt and KDDTest+.txt)
2. Where to download them from (the official UNB-CIC source — remind me to verify the URL myself)
3. That the files have NO header row — I need to supply column names manually
4. Give me the list of the 43 column names for NSL-KDD (41 feature columns + label + difficulty score)

**Task 3 — Data loading code (15 minutes):**

Provide complete, commented code to load the dataset:

```python
# NSL-KDD column names (41 features + label + difficulty)
columns = [
    # ... all 43 names here
]

# Load training and test data
train_df = pd.read_csv('KDDTrain+.txt', names=columns)
test_df = pd.read_csv('KDDTest+.txt', names=columns)

print("Train shape:", train_df.shape)
print("Test shape:", test_df.shape)
print("\nFirst 3 rows:")
train_df.head(3)
```

Explain each line so I understand what it does.

**Task 4 — Dataset exploration code (20 minutes):**

Provide code for these exploration steps (each as a separate cell):

1. Check data types: `train_df.dtypes`
2. Check for null values: `train_df.isnull().sum()`
3. Show value counts for the label column
4. Show the 3 categorical feature columns and their unique values (protocol_type, service, flag)
5. Show basic statistics for 5 numerical features: `train_df[['duration','src_bytes','dst_bytes','wrong_fragment','urgent']].describe()`

After each cell, tell me what I should expect to see and what it means.

**Task 5 — Understand what I just loaded (5 minutes):**

After I run the exploration code and paste the output, help me interpret:
- How many records are in training vs. test set?
- How many unique attack types exist?
- What is the class balance (normal vs. attacks)?
- What do the categorical features tell me?

---

**IMPORTANT CONSTRAINTS:**
- Provide exact runnable Python code — no pseudocode
- Explain every line of code in plain English
- Do not move ahead to preprocessing today — just loading and exploration
- If I report an error when running code, help me debug it
- The NSL-KDD column names must be accurate — flag if you are uncertain about any name

**EXPECTED OUTPUT BY END OF SESSION:**
- Working Colab notebook with all imports running
- Dataset successfully loaded (both train and test)
- Exploration code run and output understood
- Notes saved to `week-3/dataset-exploration.md`

**HOW TO WORK WITH ME:**
- Give code in blocks I can run one at a time
- After each block, explain what I should see
- If I paste error output, help me fix it before moving on

**CONTINGENCY — if dataset download fails:**
Search for "NSL-KDD dataset" on Kaggle as a backup. The files should be named KDDTrain+.txt and KDDTest+.txt. Do not use a different dataset.

**AT THE END OF THIS SESSION, PROVIDE:**
1. A summary of what the dataset looks like (shape, classes, key features)
2. Everything formatted for `week-3/dataset-exploration.md`
3. The complete notebook code in one block for easy copying
4. Reminder: "Next session (Day 3) we plan the preprocessing steps and write the methodology draft."

---

## Definition of Done

- [ ] Google Colab notebook opens and all imports work
- [ ] NSL-KDD files downloaded and loaded successfully
- [ ] `train_df.shape` shows correct dimensions (~125k rows, 43 columns)
- [ ] Label column explored — I know how many unique attack types exist
- [ ] 3 categorical columns identified
- [ ] Exploration notes saved to `week-3/dataset-exploration.md`

### Expected artifacts
- `week-3/notebook.ipynb` — save the Colab notebook
- `week-3/dataset-exploration.md` — notes on dataset structure

### Estimated time
~60 minutes

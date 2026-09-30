# Week 3 — Day 3
**Topic:** Preprocessing Plan and Methodology Draft
**Role of AI today:** Programmer and academic writing assistant
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
- Dataset: NSL-KDD (KDDTrain+.txt ~125k rows, KDDTest+.txt ~22k rows, 41 features)
- Categorical features: protocol_type, service, flag (to be encoded with LabelEncoder)
- Target: binary label (normal=0, all attack types=1)
- Model: Random Forest (100 trees, random_state=42)
- Attack: Gaussian noise on top 5 features of attack-class test samples (std=0.1, 0.3, 0.5)
- Defense: Adversarial training (augmented retraining)
- Tools: Python, Google Colab, pandas, scikit-learn, numpy, matplotlib

---

**CURRENT STAGE:**
Week 3, Day 3.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–2 complete: research question, literature review, gap statement, reference list
- Week 3 Day 1 complete: framework design, architecture diagram, 3-condition table, draft section
- Week 3 Day 2 complete:
  - Google Colab set up with all imports working
  - NSL-KDD loaded (train: ~125k rows, test: ~22k rows, 43 columns)
  - Dataset explored: label values known, 3 categorical features identified, no null values
  - Notes in `week-3/dataset-exploration.md`

---

**TODAY'S OBJECTIVE:**
Plan and document the complete preprocessing pipeline step-by-step. Write the Methodology section draft for the report. End the session with a code skeleton (structure without full implementation) ready for next week.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Programmer and academic writing assistant. First we plan the preprocessing pipeline carefully, then we write the methodology, then we build the code skeleton.

---

**TODAY'S TASKS:**

**Task 1 — Design the preprocessing pipeline (15 minutes):**

Walk me through exactly what preprocessing must happen before training, in what order, and why:

1. **Drop the difficulty column** — NSL-KDD has a difficulty score column that should be excluded from features. Why?
2. **Encode categorical features** — protocol_type, service, flag must be converted to numbers. Why LabelEncoder and not OneHotEncoder for this experiment?
3. **Create binary labels** — "normal" → 0, all other labels → 1. Write the exact pandas code for this.
4. **Separate features from target** — X = all feature columns, y = binary label column
5. **Train/test split** — Do I use sklearn's train_test_split or just use the provided train and test files separately? Which is better for NSL-KDD and why?
6. **Normalize features** — Apply StandardScaler to numerical features. Why is this important? Should I fit on train and transform both train and test?

For each step: explain the reason, potential pitfalls, and give me the code.

**Task 2 — Write preprocessing code skeleton (15 minutes):**

Provide a complete code skeleton with comments showing the structure:

```python
# Step 1: Define columns and load data
# ...

# Step 2: Drop difficulty column
# ...

# Step 3: Encode categorical features
# ...

# Step 4: Create binary labels
# ...

# Step 5: Separate X and y
# ...

# Step 6: Use pre-split train/test files (do NOT use train_test_split)
# ...

# Step 7: Fit StandardScaler on X_train, transform both X_train and X_test
# ...

# Step 8: Verify shapes
print("X_train shape:", X_train.shape)
print("X_test shape:", X_test.shape)
print("y_train value counts:", pd.Series(y_train).value_counts())
```

Fill in the key lines — this is a skeleton I will complete in Week 4.

**Task 3 — Write the Methodology section draft (25 minutes):**

Write a 400–500 word [AI DRAFT — VERIFY] methodology section for the report. It must include these sub-sections:

**3.1 Dataset**
- What NSL-KDD is, where it comes from, why it was chosen
- Training set size, test set size, number of features
- Binary classification setup (normal vs. attack)

**3.2 Preprocessing**
- The 6 preprocessing steps in order
- Why each step is necessary
- Note that StandardScaler is fit on training data only (no data leakage)

**3.3 Baseline Model**
- Random Forest: why chosen, configuration (100 trees, random_state=42)
- Evaluation metrics: accuracy, precision, recall, F1, AUC-ROC
- Why these metrics are standard for intrusion detection

**3.4 Adversarial Attack Design**
- Feature perturbation approach: Gaussian noise on top 5 features
- Why this is a valid proxy for evasion attack on a tree-based model
- Noise levels: 0.1, 0.3, 0.5

**3.5 Defense Mechanism**
- Adversarial training: how augmented dataset is created
- Why this should improve robustness
- How it differs from the baseline model

Mark all sections [AI DRAFT — VERIFY].

**Task 4 — Week 3 wrap-up (5 minutes):**
Summarize what Week 3 accomplished and confirm what is ready for Week 4.

---

**IMPORTANT CONSTRAINTS:**
- Preprocessing must prevent data leakage (scaler fit on train only)
- Do not implement full code today — skeleton only
- Methodology must accurately describe what I will actually do (not an ideal system)
- Do not add preprocessing steps that are not needed

**EXPECTED OUTPUT BY END OF SESSION:**
- Complete preprocessing pipeline documented (6 steps with explanations)
- Preprocessing code skeleton
- 400–500 word [AI DRAFT] methodology section
- `week-3/methodology-draft.md` saved

**AT THE END OF THIS SESSION, PROVIDE:**
1. Preprocessing steps (plain language + code skeleton)
2. Methodology draft (formatted, marked [AI DRAFT — VERIFY])
3. `week-3/methodology-draft.md` ready to copy
4. Reminder: "Week 3 complete. Week 4: implement preprocessing and train the baseline model."

---

## Definition of Done

- [ ] 6 preprocessing steps documented with explanations
- [ ] Code skeleton written (structure visible, key lines filled in)
- [ ] 400-word methodology draft written and marked [AI DRAFT — VERIFY]
- [ ] `week-3/methodology-draft.md` saved

### Expected artifacts
- `week-3/methodology-draft.md` — preprocessing plan + code skeleton + methodology draft

### Week 3 is complete when you have
- `week-3/framework-design.md`
- `week-3/dataset-exploration.md`
- `week-3/notebook.ipynb` (with imports + data loading)
- `week-3/methodology-draft.md`

### Estimated time
~60 minutes

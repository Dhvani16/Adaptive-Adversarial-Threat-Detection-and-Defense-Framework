# Week 4 — Day 2
**Topic:** Train Random Forest and Record Baseline Metrics
**Role of AI today:** Programmer and data analyst
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
- Dataset: NSL-KDD binary classification (normal=0, attack=1)
- Model: Random Forest (100 trees, random_state=42)
- Three conditions: C1 baseline / C2 under attack / C3 post-defense
- Metrics: Accuracy, Precision, Recall, F1-score, AUC-ROC
- Tools: Python, Google Colab, scikit-learn, pandas, matplotlib

---

**CURRENT STAGE:**
Week 4, Day 2.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–3 complete: research question, literature review, framework design, environment setup
- Week 4 Day 1 complete:
  - Full preprocessing pipeline implemented and verified
  - X_train (~125k × 41), X_test (~22k × 41), y_train, y_test ready
  - Code saved in `week-4/notebook-baseline.ipynb`
  - StandardScaler fitted on training data only

---

**TODAY'S OBJECTIVE:**
Train the Random Forest classifier on the clean training data, evaluate it on the clean test set, and record ALL baseline metrics (Accuracy, Precision, Recall, F1, AUC-ROC). These are my Condition 1 (C1) results — the reference point for the entire experiment.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Programmer and data analyst. Provide runnable code, help me record results accurately, and help me understand what the numbers mean.

---

**TODAY'S TASKS:**

**Task 1 — Train the Random Forest (10 minutes):**

Provide this code cell:

```python
# Train baseline Random Forest
rf_baseline = RandomForestClassifier(n_estimators=100, random_state=42, n_jobs=-1)
rf_baseline.fit(X_train, y_train)
print("Training complete.")
```

Explain: what does `n_jobs=-1` do? What does `random_state=42` ensure?

**Task 2 — Evaluate on clean test set (15 minutes):**

Provide complete evaluation code:

```python
# Predict on clean test set (Condition 1 — Baseline)
y_pred_baseline = rf_baseline.predict(X_test)
y_prob_baseline = rf_baseline.predict_proba(X_test)[:, 1]

# Compute metrics
acc_c1  = accuracy_score(y_test, y_pred_baseline)
prec_c1 = precision_score(y_test, y_pred_baseline)
rec_c1  = recall_score(y_test, y_pred_baseline)
f1_c1   = f1_score(y_test, y_pred_baseline)
auc_c1  = roc_auc_score(y_test, y_prob_baseline)

print("=== CONDITION 1: BASELINE RESULTS ===")
print(f"Accuracy : {acc_c1:.4f}")
print(f"Precision: {prec_c1:.4f}")
print(f"Recall   : {rec_c1:.4f}")
print(f"F1-Score : {f1_c1:.4f}")
print(f"AUC-ROC  : {auc_c1:.4f}")
```

After running this, I will paste my actual output. Help me interpret what the numbers mean.

**Task 3 — Feature importance (10 minutes):**

Provide code to extract and display the top 10 most important features:

```python
# Feature importances
feature_names = [col for col in train_df.columns if col != 'label']
importances = rf_baseline.feature_importances_
top10_idx = np.argsort(importances)[::-1][:10]

print("Top 10 features by importance:")
for i, idx in enumerate(top10_idx):
    print(f"  {i+1}. {feature_names[idx]}: {importances[idx]:.4f}")

# Save top 5 indices for attack simulation in Week 5
top5_idx = top10_idx[:5]
print("\nTop 5 feature indices (for adversarial attack):", top5_idx)
```

Explain why these top features matter for the adversarial attack in Week 5.

**Task 4 — Record results in a table (10 minutes):**

After I paste my output numbers, help me create a formatted results table I can put in my report:

| Condition | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|---|---|---|---|---|---|
| C1: Baseline | [my number] | [my number] | [my number] | [my number] | [my number] |
| C2: Under Attack | TBD | TBD | TBD | TBD | TBD |
| C3: Post-Defense | TBD | TBD | TBD | TBD | TBD |

**Task 5 — Interpret the baseline results (10 minutes):**

After I share my actual numbers, help me write 2–3 sentences interpreting the baseline:
- Is the model performing well? What do the metrics individually mean for intrusion detection?
- What does high recall mean vs. high precision in the IDS context?
- What should I say about this baseline in my report?

Mark interpretive text [AI DRAFT — VERIFY].

**Task 6 — Save important variables reminder (5 minutes):**

Tell me what I must save or note down for future sessions:
- The trained model object (`rf_baseline`)
- The top 5 feature indices (`top5_idx`)
- The exact baseline metric values (copy these to `week-4/results-baseline.md`)

---

**IMPORTANT CONSTRAINTS:**
- Record ONLY the actual numbers from my run — do not suggest what numbers "should" look like
- If my results seem unusually low or high, help me understand why (possible bug vs. expected outcome)
- Do not move to visualizations today — that is Day 3
- Save `top5_idx` — it is needed for the adversarial attack in Week 5

**EXPECTED OUTPUT BY END OF SESSION:**
- Random Forest trained successfully
- All 5 baseline metrics recorded with 4 decimal places
- Top 5 features identified and saved
- Results table started (C1 filled in, C2/C3 as TBD)
- `week-4/results-baseline.md` created with actual numbers

**AT THE END OF THIS SESSION, PROVIDE:**
1. All metric values in a copy-paste block for `week-4/results-baseline.md`
2. Top 5 feature names and indices
3. 2–3 sentence interpretation (marked [AI DRAFT — VERIFY])
4. Reminder: "Next session (Day 3) we generate confusion matrix and ROC curve."

---

## Definition of Done

- [ ] Random Forest trained without errors
- [ ] All 5 metrics recorded: Accuracy, Precision, Recall, F1, AUC-ROC (4 decimal places)
- [ ] Top 5 feature indices identified and noted
- [ ] Results table created with C1 values filled in
- [ ] `week-4/results-baseline.md` saved with actual numbers

### Expected artifacts
- `week-4/notebook-baseline.ipynb` — add training + evaluation cells
- `week-4/results-baseline.md` — actual baseline metric values

### Estimated time
~60 minutes

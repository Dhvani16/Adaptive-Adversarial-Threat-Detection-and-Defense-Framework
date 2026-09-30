# Week 6 — Day 2
**Topic:** Adversarial Training Implementation
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
- Dataset: NSL-KDD binary classification (preprocessed — X_train, X_test, y_train, y_test)
- Baseline Random Forest: trained, metrics saved as C1
- Adversarial attack: run at DEFENSE_NOISE_STD, metrics saved as C2
- Defense: adversarial training (augment X_train with perturbed attack samples, retrain, evaluate on same adversarial test set)
- Tools: Python, Google Colab, scikit-learn, numpy

---

**CURRENT STAGE:**
Week 6, Day 2.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–5 complete: all prior research, preprocessing, C1 baseline, C2 attack results
- Week 6 Day 1 complete:
  - Adversarial training theory understood
  - Augmented dataset construction plan documented
  - 150-word [AI DRAFT] defense methodology paragraph saved in `week-6/defense-design.md`
- Available in Colab: X_train, X_test, y_train, y_test, top5_idx, DEFENSE_NOISE_STD, rf_baseline

---

**TODAY'S OBJECTIVE:**
Implement adversarial training: create the augmented training set, retrain a new Random Forest, evaluate it on the adversarial test set (same one used for C2), and record the Condition 3 metrics.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Programmer and debugger. Provide complete runnable code. Help me record actual results.

---

**TODAY'S TASKS:**

**Task 1 — Create the adversarial training function (15 minutes):**

Provide a function that creates adversarial copies of the attack-class TRAINING samples:

```python
def create_adversarial_train(X_train, y_train, top5_idx, noise_std, random_state=42):
    """
    Create adversarial copies of attack-class training samples.
    These will be added to the training set to augment it.
    """
    np.random.seed(random_state)
    attack_mask = (y_train == 1)
    X_attack = X_train[attack_mask].copy()
    noise = np.random.normal(0, noise_std, size=(X_attack.shape[0], len(top5_idx)))
    X_attack[:, top5_idx] += noise
    return X_attack, y_train[attack_mask].copy()
```

Explain: why do we keep the labels as 1 for the adversarial training samples? What is the logic here?

**Task 2 — Build the augmented training set (10 minutes):**

```python
# Generate adversarial training samples
X_adv_train, y_adv_train = create_adversarial_train(
    X_train, y_train, top5_idx, noise_std=DEFENSE_NOISE_STD
)

# Augment: stack original + adversarial samples
X_train_augmented = np.vstack([X_train, X_adv_train])
y_train_augmented = np.concatenate([y_train, y_adv_train])

print(f"Original training set: {X_train.shape}")
print(f"Adversarial samples added: {X_adv_train.shape}")
print(f"Augmented training set: {X_train_augmented.shape}")
print(f"Augmented class balance — 0:{(y_train_augmented==0).sum()} | 1:{(y_train_augmented==1).sum()}")
```

Explain: why does the augmented training set have more attack samples than normal samples? Is this a problem?

**Task 3 — Train the defended model (10 minutes):**

```python
# Train defended Random Forest on augmented dataset
rf_defended = RandomForestClassifier(n_estimators=100, random_state=42, n_jobs=-1)
rf_defended.fit(X_train_augmented, y_train_augmented)
print("Defended model training complete.")
```

This uses the same hyperparameters as the baseline — explain why this is important for a fair comparison.

**Task 4 — Evaluate on the adversarial test set (15 minutes):**

Evaluate the DEFENDED model on the SAME adversarial test set used for C2:

```python
# Use the same adversarial test set from Week 5
# (recreate it if not still in memory)
X_adv_test = create_adversarial_test(X_test, y_test, top5_idx, noise_std=DEFENSE_NOISE_STD)

y_pred_defended = rf_defended.predict(X_adv_test)
y_prob_defended = rf_defended.predict_proba(X_adv_test)[:, 1]

acc_c3  = accuracy_score(y_test, y_pred_defended)
prec_c3 = precision_score(y_test, y_pred_defended)
rec_c3  = recall_score(y_test, y_pred_defended)
f1_c3   = f1_score(y_test, y_pred_defended)
auc_c3  = roc_auc_score(y_test, y_prob_defended)

print("=== CONDITION 3: POST-DEFENSE RESULTS ===")
print(f"Accuracy : {acc_c3:.4f}")
print(f"Precision: {prec_c3:.4f}")
print(f"Recall   : {rec_c3:.4f}")
print(f"F1-Score : {f1_c3:.4f}")
print(f"AUC-ROC  : {auc_c3:.4f}")
```

After I paste my output, help me interpret the results: did the defense work? By how much?

**Task 5 — Save C3 results (10 minutes):**

```python
print("\n=== THREE-CONDITION SUMMARY ===")
print(f"{'Condition':>25} | {'Accuracy':>10} | {'Recall':>8} | {'F1':>8} | {'AUC':>8}")
print("-" * 70)
print(f"{'C1: Baseline':>25} | {acc_c1:>10.4f} | {rec_c1:>8.4f} | {f1_c1:>8.4f} | {auc_c1:>8.4f}")
# Paste your C2 values from week-5/attack-results.md:
print(f"{'C2: Under Attack':>25} | {ACC_C2:>10.4f} | {REC_C2:>8.4f} | {F1_C2:>8.4f} | {AUC_C2:>8.4f}")
print(f"{'C3: Post-Defense':>25} | {acc_c3:>10.4f} | {rec_c3:>8.4f} | {f1_c3:>8.4f} | {auc_c3:>8.4f}")
```

Help me save this to `week-6/defense-results.md`.

---

**IMPORTANT CONSTRAINTS:**
- The defended model must be evaluated on the SAME adversarial test set as C2 — not the clean test set
- Record ONLY actual experimental numbers — no invented results
- If the defense shows no improvement, report this honestly — it is still valid

**CONTINGENCY — if C3 metrics are no better than C2:**
Try creating adversarial training samples at a lower noise level (std=0.1) even if DEFENSE_NOISE_STD is higher. If still no improvement, report the null result and explain why in the limitations section.

**EXPECTED OUTPUT BY END OF SESSION:**
- Augmented training set created
- Defended model trained
- C3 metrics recorded (all 5 values)
- Three-condition summary table complete
- `week-6/defense-results.md` saved

**AT THE END OF THIS SESSION, PROVIDE:**
1. All three-condition results formatted for `week-6/defense-results.md`
2. Brief interpretation: did the defense work?
3. Reminder: "Next session (Day 3) we generate comparison visualizations and wrap up experiments."

---

## Definition of Done

- [ ] Augmented training set created (shapes printed and confirmed)
- [ ] Defended model trained without errors
- [ ] C3 metrics recorded (Accuracy, Precision, Recall, F1, AUC — 4 decimal places)
- [ ] Three-condition summary table complete
- [ ] `week-6/defense-results.md` saved with actual numbers

### Expected artifacts
- `week-6/notebook-defense.ipynb` — adversarial training code
- `week-6/defense-results.md` — C3 metrics + 3-condition table

### Estimated time
~60 minutes

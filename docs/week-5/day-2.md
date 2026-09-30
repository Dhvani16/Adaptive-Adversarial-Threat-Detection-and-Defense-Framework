# Week 5 — Day 2
**Topic:** Adversarial Attack Implementation and Testing
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
- Dataset: NSL-KDD (preprocessed — X_train, X_test, y_train, y_test ready)
- Model: Random Forest (trained as `rf_baseline`, baseline metrics recorded)
- Attack: Add Gaussian noise (std=0.1, 0.3, 0.5) to top 5 features of attack-class test samples
- Top 5 feature indices: saved as `top5_idx` from Week 4 Day 2
- Metrics to record: Accuracy, Recall, F1-score at each noise level

---

**CURRENT STAGE:**
Week 5, Day 2.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–4 complete: research, framework, preprocessing, baseline model trained
- Week 5 Day 1 complete:
  - Attack theory understood
  - 8-step attack procedure documented
  - Noise level selection rationale written
  - [AI DRAFT] methodology paragraph saved in `week-5/attack-design.md`
- I have open in Colab: X_train, X_test, y_train, y_test, rf_baseline, top5_idx

---

**TODAY'S OBJECTIVE:**
Implement the adversarial attack — add Gaussian noise to the top 5 features of attack-class test samples at three noise levels (std=0.1, 0.3, 0.5). Run the baseline model on each adversarial test set. Record ALL metrics. Select the noise level for use in the defense phase.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Programmer and debugger. Provide complete runnable code. Help me record and interpret real results.

---

**TODAY'S TASKS:**

**Task 1 — Attack function (15 minutes):**

Provide a reusable function that creates adversarial test data:

```python
def create_adversarial_test(X_test, y_test, top5_idx, noise_std, random_state=42):
    """
    Add Gaussian noise to the top 5 features of attack-class test samples.
    Normal-class samples are NOT modified.
    Returns a perturbed copy of X_test.
    """
    np.random.seed(random_state)
    X_adv = X_test.copy()
    attack_mask = (y_test == 1)   # Only modify attack-class samples
    noise = np.random.normal(0, noise_std, size=(attack_mask.sum(), len(top5_idx)))
    X_adv[np.ix_(np.where(attack_mask)[0], top5_idx)] += noise
    return X_adv
```

Explain each line. Why do we use `np.ix_` here? Why do we copy X_test rather than modify it directly?

**Task 2 — Run attack at 3 noise levels (20 minutes):**

Provide a loop that runs the attack at all three levels and records results:

```python
noise_levels = [0.1, 0.3, 0.5]
attack_results = {}

for std in noise_levels:
    X_adv = create_adversarial_test(X_test, y_test, top5_idx, noise_std=std)
    y_pred_adv = rf_baseline.predict(X_adv)
    y_prob_adv = rf_baseline.predict_proba(X_adv)[:, 1]

    attack_results[std] = {
        'accuracy': accuracy_score(y_test, y_pred_adv),
        'recall':   recall_score(y_test, y_pred_adv),
        'f1':       f1_score(y_test, y_pred_adv),
        'auc':      roc_auc_score(y_test, y_prob_adv)
    }

print("=== ADVERSARIAL ATTACK RESULTS ===")
print(f"{'Noise':>8} | {'Accuracy':>10} | {'Recall':>8} | {'F1':>8} | {'AUC':>8}")
print("-" * 55)
for std, m in attack_results.items():
    print(f"{std:>8.1f} | {m['accuracy']:>10.4f} | {m['recall']:>8.4f} | {m['f1']:>8.4f} | {m['auc']:>8.4f}")
```

After I run this and paste my output, help me interpret which noise level causes the most meaningful degradation.

**Task 3 — Compare against baseline (10 minutes):**

Help me add a baseline row to the results output (using C1 values from `week-4/results-baseline.md`) so I can see the drop:

```python
print("\n=== COMPARISON: BASELINE vs. ADVERSARIAL ===")
print(f"{'Condition':>20} | {'Accuracy':>10} | {'Recall':>8} | {'F1':>8}")
print("-" * 58)
print(f"{'C1 Baseline':>20} | {acc_c1:>10.4f} | {rec_c1:>8.4f} | {f1_c1:>8.4f}")
for std, m in attack_results.items():
    label = f"C2 Attack (std={std})"
    print(f"{label:>20} | {m['accuracy']:>10.4f} | {m['recall']:>8.4f} | {m['f1']:>8.4f}")
```

**Task 4 — Select the defense noise level (5 minutes):**

After I share my actual results, help me decide which noise level (0.1, 0.3, or 0.5) to use for the defense phase. Criteria:
- Shows clear, measurable degradation (not trivial)
- Does not completely destroy performance (not all zeros)
- std=0.3 is the default choice — confirm or adjust based on my results

Save the chosen level as `DEFENSE_NOISE_STD`.

**Task 5 — Save results to file (10 minutes):**

Create a formatted results block I can paste into `week-5/attack-results.md`:

```
=== CONDITION 2: ADVERSARIAL ATTACK RESULTS ===
Baseline (C1): Accuracy=X, Recall=X, F1=X
Attack std=0.1: Accuracy=X, Recall=X, F1=X  (drop: -X%)
Attack std=0.3: Accuracy=X, Recall=X, F1=X  (drop: -X%)
Attack std=0.5: Accuracy=X, Recall=X, F1=X  (drop: -X%)
Selected noise level for defense: std=X
Top 5 features perturbed: [list them by name]
```

Fill this with my actual numbers after I share the output.

---

**IMPORTANT CONSTRAINTS:**
- Record ONLY my actual experimental output — do not suggest what numbers "should" be
- Do not move to visualization today — that is Day 3
- The attack must use the same `top5_idx` identified in Week 4
- All noise is added to attack-class samples only (normal samples unchanged)

**CONTINGENCY — if noise=0.5 shows no degradation:**
Try std=1.0 or std=2.0. If still no degradation, perturb all top 10 features instead of top 5.

**EXPECTED OUTPUT BY END OF SESSION:**
- Attack function implemented and working
- Attack run at std=0.1, 0.3, 0.5 with real results recorded
- Comparison table (C1 vs. C2 at 3 noise levels)
- Defense noise level selected and saved as `DEFENSE_NOISE_STD`
- `week-5/attack-results.md` saved with actual numbers

**AT THE END OF THIS SESSION, PROVIDE:**
1. All results formatted for `week-5/attack-results.md`
2. The `DEFENSE_NOISE_STD` value chosen
3. Reminder: "Next session (Day 3) we plot the attack curve and document findings."

---

## Definition of Done

- [ ] Attack function runs without errors at all 3 noise levels
- [ ] Performance drop measured at std=0.1, 0.3, 0.5 (real numbers)
- [ ] Comparison table created (C1 vs. C2 at each noise level)
- [ ] `DEFENSE_NOISE_STD` chosen and documented
- [ ] `week-5/attack-results.md` saved with actual metric values

### Expected artifacts
- `week-5/notebook-attack.ipynb` — attack code cells
- `week-5/attack-results.md` — metric table with actual numbers

### Estimated time
~60 minutes

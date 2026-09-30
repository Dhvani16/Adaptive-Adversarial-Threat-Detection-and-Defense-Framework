# Week 5 — Adversarial Attack Design

---

## Theory: Feature-Space Evasion Attacks

### 1. What is a feature-space evasion attack?

A feature-space evasion attack manipulates the numerical input features of a sample at inference time so that a trained classifier misclassifies it. In network intrusion detection, this means slightly modifying the traffic feature values of a malicious connection so that the model sees it as normal traffic. The attacker does not change the actual behaviour of the attack — only the values the model sees.

An everyday analogy: imagine a customs officer trained to spot known smugglers based on their appearance. An adversary does not stop smuggling — they just change their clothes, add a disguise, and adjust their walk slightly so the customs officer no longer recognizes them.

### 2. Why does Gaussian noise on important features simulate an evasion attack on Random Forest?

Random Forest is a non-differentiable model — you cannot compute a gradient through it, so gradient-based attacks (FGSM, PGD) do not apply. Gaussian noise on the top-5 features is a recognized heuristic proxy because:

- Attackers who partially understand the model will focus their manipulation on the features the model relies on most — these are exactly `feature_importances_` top-5
- Gaussian noise simulates the small, bounded modifications an attacker might make to traffic feature values
- Adding noise shifts attack samples toward a region of feature space where the decision boundary is less certain, increasing the chance of misclassification

**Underlying assumption:** The attacker knows the approximate set of important features but applies random perturbation rather than an optimal attack. This is a realistic threat model for a partially informed adversary.

### 3. Limitations of Gaussian noise as an attack proxy

These limitations MUST appear in the report's limitations section:

1. **Not a true adversarial example:** A real adversary would optimize the perturbation to maximize misclassification. Gaussian noise is random, not optimized — it is weaker than a real attack.
2. **Feature-space vs. problem-space:** In practice, not all feature combinations are realistic network traffic. A random perturbation may produce feature values that no real packet could generate.
3. **No attacker knowledge simulation:** This approach assumes a specific, simplified attacker model. A real attacker could use different techniques.
4. **Non-transferable across models:** The perturbation is tailored to the top features of this specific model. It may not generalize to other classifiers.

### 4. Why do we only perturb attack-class samples?

We only perturb attack-class samples because the experiment models an evasion attack: the adversary's goal is to make attack traffic look like normal traffic. Perturbing normal traffic would model a different scenario (making normal traffic trigger false alarms), which is not what we are studying. Keeping normal samples unmodified isolates the effect of the attack on detection performance (recall).

### 5. Why use `feature_importances_` to choose which features to perturb?

`feature_importances_` identifies the features the model weighted most heavily when making decisions. An attacker who partially knows the model's behaviour would target these features first — they are the ones most likely to shift the classification outcome when modified. Perturbing less important features would have minimal effect on predictions.

---

## Attack Procedure (8 Steps)

Follow this exactly when coding in Day 2:

1. **Ensure the following are available:** `X_test`, `y_test`, `rf_baseline`, `top5_idx`, baseline metrics (`acc_c1`, `rec_c1`, `f1_c1`)
2. **Write the `create_adversarial_test()` function** — takes `X_test`, `y_test`, `top5_idx`, `noise_std`; returns a perturbed copy of `X_test`
3. **Identify attack-class rows** in `X_test` using mask `y_test == 1`
4. **For each noise level (0.1, 0.3, 0.5):**
   - Call `create_adversarial_test()` to generate `X_adv`
   - Run `rf_baseline.predict(X_adv)` and `rf_baseline.predict_proba(X_adv)`
   - Record: Accuracy, Recall, F1-score, AUC-ROC
5. **Print comparison table:** C1 baseline row vs. C2 at each noise level
6. **Select `DEFENSE_NOISE_STD`:** the noise level that causes clear but not total degradation (target: recall drop of 0.1–0.3, not 0.9+)
7. **Record actual numbers in `week-5/attack-results.md`**
8. **Verify:** normal-class rows in `X_adv` must be identical to `X_test` (check with assertion)

---

## Noise Level Rationale

| Parameter | What it controls |
|---|---|
| `noise_std = 0.1` | Small perturbation — likely minimal degradation |
| `noise_std = 0.3` | Medium perturbation — expected to show meaningful drop |
| `noise_std = 0.5` | Larger perturbation — potentially severe degradation |

**Why test three levels?** Testing a range of intensities (1) shows the relationship between attack strength and model vulnerability, (2) allows us to select a representative level for the defense phase, and (3) produces the attack curve figure — a key visualization for the report.

**Default selection for defense phase:** `std = 0.3`. This is the "medium" level. If it causes less than 5% recall drop, use `std = 0.5`. If it causes more than 50% drop, use `std = 0.1`. Document which level was chosen and why.

---

## [AI DRAFT — VERIFY] Methodology Paragraph — Adversarial Attack Design

[AI DRAFT — VERIFY]

#### 7.4 Adversarial Attack Design

This study simulates an adversarial evasion attack using feature-space perturbation — a technique appropriate for non-differentiable classifiers such as Random Forest, where gradient-based attack methods (e.g., FGSM) are inapplicable. Following Condition 1 evaluation, the five features with the highest importance scores from `feature_importances_` are identified as the attack targets. For each of three noise magnitude levels (Gaussian noise with standard deviations of 0.1, 0.3, and 0.5), independent adversarial test sets are generated by adding random Gaussian noise to only these five features in attack-class test samples. Normal-class samples remain unmodified, isolating the evasion scenario. The baseline Random Forest model is then evaluated on each adversarial test set, and the resulting degradation in accuracy, recall, and F1-score is recorded. Feature-space perturbation is acknowledged as a simplified proxy for a real adversarial attack; it models a partially informed attacker rather than an optimized adversary (see Section 11 — Limitations).

*[AI DRAFT — VERIFY: Confirm that `feature_importances_` was used to select features, that noise levels match your implementation, and that the limitation acknowledgement is accurate.]*

---

## Day 2 Preparation Checklist

Before starting Day 2 coding, confirm the following are available in your Colab session:
- [ ] `X_train`, `X_test`, `y_train`, `y_test` (preprocessed from Week 4)
- [ ] `rf_baseline` (trained Random Forest from Week 4)
- [ ] `top5_idx` (numpy array of 5 feature indices from Week 4 Cell 12)
- [ ] `acc_c1`, `rec_c1`, `f1_c1`, `auc_c1` (baseline metric variables from Week 4 Cell 11)
- [ ] `feature_names` (list of 41 feature column names from Week 4)
- [ ] `week-5/attack-design.md` open for reference

*Next session (Day 2): Code and run the attack at all 3 noise levels.*

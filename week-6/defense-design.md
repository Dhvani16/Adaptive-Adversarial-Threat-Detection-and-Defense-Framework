# Week 6 — Adversarial Training Defense Design

---

## Theory: Adversarial Training

### 1. What is adversarial training in plain language?

Adversarial training is a defense technique where the model is retrained on a dataset that includes both the original clean samples AND deliberately perturbed (adversarial) versions of those samples. The perturbed samples are labelled correctly — the model is taught that even "disguised" attack samples are still attacks.

Analogy: A security guard who has been trained only on criminals with visible weapons may fail to identify criminals who hide their weapons. Adversarial training is like giving the guard a new training program that includes criminals in various disguises — after training, the guard recognizes the pattern regardless of the disguise.

### 2. How does it help the model generalize to adversarial inputs?

When adversarial examples are added to training data with correct labels, the model's decision boundary shifts to include the adversarial region. In Random Forest terms: the trees are grown on a training set that now includes perturbed attack samples in the feature space. When an attack sample is perturbed at test time, it falls into a region the model has already learned to classify as attack — instead of the ambiguous boundary region it fell into before.

### 3. Core assumption about the attacker

Adversarial training assumes the attacker uses a **similar perturbation type and magnitude** to what was used during augmentation. The defense is specific to the threat model it was trained against. If the attacker uses a completely different attack strategy or a much larger perturbation, the defense may not generalize.

### 4. Known failure modes

1. **Mismatch in perturbation type or magnitude:** Training on noise std=0.3 does not guarantee robustness against noise std=1.0 or different attack types
2. **Adaptive attackers:** If an attacker knows a defense has been applied, they can adapt their attack to bypass it (Carlini & Wagner, 2017)
3. **Accuracy–robustness trade-off:** Adding adversarial samples slightly shifts the decision boundary, which can modestly reduce clean-data accuracy
4. **Distribution shift:** Adversarial training generalizes to perturbations similar to training; out-of-distribution perturbations remain effective

### 5. Why adversarial training is "basic" and what more sophisticated defenses exist

Adversarial training is considered basic because it is a heuristic — it does not provide formal robustness guarantees. More sophisticated defenses (NOT implemented here):
- **Certified defenses (randomized smoothing):** Provide provable robustness bounds but require significant computational overhead
- **Ensemble adversarial training (Tramèr et al., 2018):** Uses adversarial examples from multiple models for better generalization
- **Feature squeezing / input preprocessing:** Removes perturbations before they reach the model
- **Adversarial detection layers:** Add a separate anomaly detector to flag adversarial inputs

These are excluded because they are beyond the 24-hour time budget. They are appropriate for the Future Work section of the report.

---

## Augmented Dataset Construction

Step-by-step procedure:

1. Start with clean training set: `X_train`, `y_train` from preprocessing
2. Identify attack-class rows: `attack_rows = X_train[y_train == 1]`
3. Apply the SAME perturbation used in the attack: Gaussian noise (mean=0, std=`DEFENSE_NOISE_STD`) to top-5 features only
4. **Keep labels as 1 (attack)** for these perturbed samples
5. Stack: `X_train_augmented = [X_train; adversarial_attack_copies]`
6. Stack labels: `y_train_augmented = [y_train; adversarial_labels_all_1]`

**Why keep labels as 1 (attack)?**  
The adversarial training samples ARE attack-class samples with added noise. Labelling them as 1 teaches the model that perturbed attack traffic is still attack traffic. If they were mislabelled as 0 (normal), the model would learn the opposite lesson — that perturbed attacks are normal — which would make the model MORE vulnerable, not less.

**Does the class imbalance matter?**  
The augmented dataset has proportionally more attack samples than normal samples. This may cause a slight increase in recall at the potential cost of precision on the clean test set. This is acceptable for an intrusion detection task where recall is prioritized. Note it in the limitations or results discussion.

---

## Outcome Prediction Table

| Outcome | What it means | Likelihood |
|---|---|---|
| C3 recall = C1 recall | Full recovery — adversarial training perfectly compensated for the attack | Less common; occurs when noise magnitude is well-matched |
| C3 recall > C2 but < C1 | Partial recovery — defense helped but did not fully close the gap | Most likely outcome; academically interesting |
| C3 recall = C2 recall | No improvement — defense did not work at this noise level | Possible if training noise level was mismatched |
| C3 recall < C2 recall | Defense made things worse — significant problem with implementation | Should be investigated as a bug if it occurs |

**Most academically interesting outcome:** Partial recovery (C3 > C2 but C3 < C1). This is the honest expected result of a basic adversarial training implementation and supports a nuanced discussion: the defense improves robustness but does not eliminate the vulnerability, motivating more sophisticated defenses in future work.

---

## [AI DRAFT — VERIFY] Defense Methodology Paragraph

[AI DRAFT — VERIFY]

#### 7.5 Defense Mechanism

The adversarial training defense is implemented as follows. First, Gaussian noise (mean=0, std = `DEFENSE_NOISE_STD`) is applied to the top-5 features of all attack-class samples in the training set, generating an adversarial copy of the attack-class training data. The correct labels (attack=1) are preserved for these perturbed samples. These adversarial training examples are then concatenated with the original training data to form an augmented training set. A new `RandomForestClassifier(n_estimators=100, random_state=42)` — identical in configuration to the baseline — is trained on this augmented dataset. The defended model is evaluated on the same adversarial test set used in Condition 2, enabling a direct comparison. The key limitation of this approach is that robustness improvements are specific to the perturbation type and magnitude seen during augmentation; a different or stronger attack may not be mitigated.

*[AI DRAFT — VERIFY: Replace `DEFENSE_NOISE_STD` with your actual value. Confirm hyperparameters match your implementation.]*

---

## Day 2 Preparation Checklist

Before starting Day 2 coding, confirm the following are available in Colab:
- [ ] `X_train`, `y_train` (preprocessed from Week 4)
- [ ] `X_test`, `y_test` (preprocessed from Week 4)
- [ ] `top5_idx` (from Week 4 Cell 12)
- [ ] `DEFENSE_NOISE_STD` (chosen in Week 5 Cell 5)
- [ ] `rf_baseline` (trained in Week 4 Cell 10)
- [ ] `acc_c1`, `prec_c1`, `rec_c1`, `f1_c1`, `auc_c1` (from Week 4 Cell 11)
- [ ] `acc_c2`, `rec_c2`, `f1_c2`, `auc_c2` (from Week 5 Cell 5)
- [ ] `create_adversarial_test()` function (from Week 5 Cell 2)
- [ ] `week-6/defense-design.md` open for reference

*Next session (Day 2): Implement adversarial training and evaluate C3.*

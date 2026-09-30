# Week 6 — Three-Condition Experiment Summary

---

## Paragraph 1: Condition 1 — Baseline Performance

The baseline Random Forest classifier (`n_estimators=100`, `random_state=42`), trained and evaluated on clean NSL-KDD data, achieved an accuracy of 0.7707, precision of 0.9662, recall of 0.6188, F1-score of 0.7544, and AUC-ROC of 0.9620 (Condition 1). The high precision indicates that the model is highly reliable when it does flag an attack, but the recall of 0.6188 reveals that approximately 38% of genuine attacks are missed under clean test conditions — a meaningful false-negative rate. Feature importance analysis identified `src_bytes`, `dst_bytes`, `same_srv_rate`, `dst_host_same_srv_rate`, and `flag` as the top-5 most influential features (`top5_idx = [4, 5, 28, 33, 3]`); these are targeted in the adversarial attack simulation in Condition 2.

---

## Paragraph 2: Condition 2 — Adversarial Attack Impact

The adversarial attack simulation applied Gaussian noise (mean=0, std=0.3) to the top-5 features of attack-class test samples only, leaving normal-class samples unperturbed. Under this attack, recall dropped from 0.6188 to 0.4621 — a reduction of 0.1567, meaning approximately 25% of previously detected attacks were now misclassified as normal traffic. The F1-score fell from 0.7544 to 0.6229. Notably, the AUC-ROC marginally increased from 0.9620 to 0.9680, suggesting the model's probability score ranking remained intact even as hard-threshold predictions degraded — the perturbations shifted attack samples toward but not definitively past the decision boundary. A noise level of std=0.3 was selected as DEFENSE_NOISE_STD because it produced a meaningful but non-catastrophic recall drop, enabling a fair evaluation of adversarial training recovery.

---

## Paragraph 3: Condition 3 — Post-Defense Recovery

Following adversarial training — augmenting the training set with perturbed copies of all attack-class training samples (std=0.3, labels preserved as attack=1) and retraining an identical Random Forest — the defended model was evaluated on the same adversarial test set used in Condition 2. The results substantially exceeded expectations: the defended model achieved accuracy of 0.9868, precision of 0.9779, recall of 0.9995, F1-score of 0.9886, and AUC-ROC of 0.9872. Recall recovered from 0.4621 (C2) to 0.9995 (C3) — a recovery of +0.5374 — and the net change from the clean baseline (C1) to post-defense (C3) was +0.3807 in recall and +0.2342 in F1-score. The defended model therefore not only fully recovered from the attack but substantially surpassed the clean baseline across all metrics. This outcome likely reflects the benefit of doubled attack-class training examples, which appear to have improved the model's generalization to the test distribution in addition to providing robustness to feature-space perturbation.

---

## Three-Condition Results Table

Noise level used for attack and defense: `std = 0.3`

| Condition | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|---|---|---|---|---|---|
| **C1: Baseline** | 0.7707 | 0.9662 | 0.6188 | 0.7544 | 0.9620 |
| **C2: Under Attack** | 0.6815 | — | 0.4621 | 0.6229 | 0.9680 |
| **C3: Post-Defense** | 0.9868 | 0.9779 | 0.9995 | 0.9886 | 0.9872 |

| Change | Recall | F1-Score |
|---|---|---|
| C1 → C2 (attack impact) | −0.1567 | −0.1315 |
| C2 → C3 (defense recovery) | +0.5374 | +0.3657 |
| C1 → C3 (net change) | +0.3807 | +0.2342 |

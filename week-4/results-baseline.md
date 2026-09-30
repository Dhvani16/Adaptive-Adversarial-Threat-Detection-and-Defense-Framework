# Week 4 — Baseline Results
*Condition 1 (C1): Random Forest trained and evaluated on clean NSL-KDD data*

---

## C1 — Baseline Metrics

| Metric | Value |
|---|---|
| Accuracy | 0.7707 |
| Precision | 0.9662 |
| Recall | 0.6188 |
| F1-Score | 0.7544 |
| AUC-ROC | 0.9620 |

---

## Top 5 Features (needed for Week 5 attack)

| Rank | Feature Name | Array Index |
|---|---|---|
| 1 | src_bytes | 4 |
| 2 | dst_bytes | 5 |
| 3 | same_srv_rate | 28 |
| 4 | dst_host_same_srv_rate | 33 |
| 5 | flag | 3 |

`top5_idx = [4, 5, 28, 33, 3]`

---

## Three-Condition Results Table

| Condition | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|---|---|---|---|---|---|
| **C1: Baseline** | 0.7707 | 0.9662 | 0.6188 | 0.7544 | 0.9620 |
| **C2: Under Attack (std=0.3)** | 0.6815 | — | 0.4621 | 0.6229 | 0.9680 |
| **C3: Post-Defense** | 0.9868 | 0.9779 | 0.9995 | 0.9886 | 0.9872 |

---

## Figures Produced This Week

| Figure | Filename | Description |
|---|---|---|
| Confusion matrix | `confusion-matrix-baseline.png` | True/false positive/negative counts for C1 |
| ROC curve | `roc-baseline.png` | AUC-ROC curve for C1 |
| Feature importance | `feature-importance-baseline.png` | Top 10 features by RF importance score |

---

## Baseline Results Paragraph (for Report Section 9.1)

The baseline Random Forest classifier, trained on the clean NSL-KDD training set and evaluated on the unperturbed test set, achieved an accuracy of 0.7707, a precision of 0.9662, a recall of 0.6188, an F1-score of 0.7544, and an AUC-ROC of 0.9620 (Condition 1, Table 1). The high precision (0.9662) indicates that when the model flags traffic as an attack, it is almost always correct. The recall of 0.6188 means approximately 38% of real attacks are missed under clean conditions — a meaningful false-negative rate that the adversarial attack will further degrade. The confusion matrix (Figure 1) and ROC curve (Figure 2) confirm the model's strong discriminative ability (AUC=0.9620). Feature importance analysis (Figure 3) identified `src_bytes`, `dst_bytes`, `same_srv_rate`, `dst_host_same_srv_rate`, and `flag` as the top-5 features; these serve as the adversarial attack targets in Condition 2.

---

## Week 4 Checklist

- [x] notebook-baseline.ipynb run without errors
- [x] Accuracy, Precision, Recall, F1-Score, AUC-ROC recorded (4 decimal places)
- [x] Top 5 feature indices noted and saved
- [x] confusion-matrix-baseline.png saved
- [x] roc-baseline.png saved
- [x] feature-importance-baseline.png saved
- [x] This file updated with actual numbers

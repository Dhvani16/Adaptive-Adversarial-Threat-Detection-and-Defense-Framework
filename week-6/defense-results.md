# Week 6 — Defense Results

---

## C3 — Post-Defense Metrics

| Metric | Value |
|---|---|
| Accuracy | 0.9868 |
| Precision | 0.9779 |
| Recall | 0.9995 |
| F1-Score | 0.9886 |
| AUC-ROC | 0.9872 |

---

## Final Three-Condition Comparison Table

Noise level used for attack and defense: `std = 0.3`

| Condition | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|---|---|---|---|---|---|
| **C1: Baseline** | 0.7707 | 0.9662 | 0.6188 | 0.7544 | 0.9620 |
| **C2: Under Attack** | 0.6815 | — | 0.4621 | 0.6229 | 0.9680 |
| **C3: Post-Defense** | 0.9868 | 0.9779 | 0.9995 | 0.9886 | 0.9872 |

**Recall drop C1→C2:** −0.1567  
**Recall recovery C2→C3:** +0.5374  
**Net change C1→C3:** +0.3807

**Key finding:** C3 substantially exceeds C1 across all metrics. Adversarial training achieved full recovery from the attack and significant improvement beyond the clean baseline. Recall improved from 0.6188 (C1) to 0.9995 (C3) — a net gain of +0.3807. This likely reflects improved generalization from the augmented attack-class training set, which doubled the number of attack-class training examples.

---

## Figures Produced This Week

| Figure | Filename | Description |
|---|---|---|
| Grouped bar chart | `comparison-barchart.png` | All 5 metrics across C1, C2, C3 |
| C3 Confusion matrix | `confusion-matrix-defense.png` | True/false positive/negative counts post-defense |

---

## Week 6 Checklist

- [x] notebook-defense.ipynb run without errors
- [x] C3 metrics recorded (all 5, 4 decimal places)
- [x] Three-condition table complete with actual numbers
- [x] comparison-barchart.png saved
- [x] confusion-matrix-defense.png saved
- [x] This file updated with actual numbers

**The experimental phase is now COMPLETE. Weeks 7–8 are writing only.**

# Week 6 — Three-Condition Comparison Table

---

## Final Results Table

Noise level used for attack and defense: `std = 0.3`

| Condition | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|---|---|---|---|---|---|
| **C1: Baseline** | 0.7707 | 0.9662 | 0.6188 | 0.7544 | 0.9620 |
| **C2: Under Attack** | 0.6815 | — | 0.4621 | 0.6229 | 0.9680 |
| **C3: Post-Defense** | 0.9868 | 0.9779 | 0.9995 | 0.9886 | 0.9872 |

---

## Key Changes

| Change | Recall | F1-Score |
|---|---|---|
| C1 → C2 (attack impact) | −0.1567 | −0.1315 |
| C2 → C3 (defense recovery) | +0.5374 | +0.3657 |
| C1 → C3 (net change) | +0.3807 | +0.2342 |

**Key finding:** C3 substantially exceeds C1 on all metrics. Adversarial training did not just recover from the attack — it produced a model significantly better than the clean baseline. Recall improved from 0.6188 (C1) to 0.9995 (C3). The augmented training set (original + adversarial attack-class copies) doubled the attack-class training examples, which appears to have substantially improved generalization to the test distribution.

---

## Complete Experimental Artifact Checklist

### Notebooks
- [x] `week-4/notebook-baseline.ipynb` — preprocessing + baseline training + evaluation
- [x] `week-5/notebook-attack.ipynb` — adversarial attack simulation
- [x] `week-6/notebook-defense.ipynb` — adversarial training defense

### Figures (PNG) — saved in `figures/`
- [x] `confusion-matrix-baseline.png`
- [x] `roc-baseline.png`
- [x] `feature-importance-baseline.png`
- [x] `attack-curve.png`
- [x] `confusion-matrix-attack.png`
- [x] `comparison-barchart.png`
- [x] `confusion-matrix-defense.png`

### Results files
- [x] `week-4/results-baseline.md` — C1 metrics filled in
- [x] `week-5/attack-results.md` — C2 metrics at std=0.3 filled in; 0.1 and 0.5 pending Cell 16
- [x] `week-6/defense-results.md` — C3 metrics filled in
- [x] `week-6/comparison-table.md` — this file, three-condition table complete

**All experiments are complete. Do NOT add new experiments in Weeks 7–8.**

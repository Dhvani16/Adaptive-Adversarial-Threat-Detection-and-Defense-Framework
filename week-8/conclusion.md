# Week 8 — Conclusion, Future Work, and Experimental Setup

---

## 13. Conclusion

This case study investigated the following research question: *To what extent does adversarial training improve the robustness of a Random Forest-based intrusion detection system against feature-space evasion attacks, as evaluated on the NSL-KDD dataset?*

The experiment produced the following results across three controlled conditions. The baseline Random Forest classifier (C1) achieved recall of 0.6188 and F1-score of 0.7544 on clean NSL-KDD test data, with a precision of 0.9662 and AUC-ROC of 0.9620. A simulated feature-space evasion attack — Gaussian noise (std=0.3) applied to the top-5 features (`src_bytes`, `dst_bytes`, `same_srv_rate`, `dst_host_same_srv_rate`, `flag`) of attack-class test samples — reduced recall to 0.4621 and F1-score to 0.6229 (C2), a decrease of 0.1567 in recall. Following adversarial training — augmenting the training set with perturbed attack-class samples and retraining the same Random Forest configuration — the defended model achieved recall of 0.9995 and F1-score of 0.9886 (C3). This represents not merely a recovery from the attack, but a substantial improvement beyond the clean baseline: net recall gain of +0.3807 from C1 to C3.

These results confirm that adversarial training is a highly effective defense mechanism against the feature-space perturbation attack evaluated. The improvement is attributable to data augmentation alone — the defended model uses identical hyperparameters to the baseline — and likely reflects both adversarial robustness and improved generalization from the doubled attack-class training set. The experiment was conducted entirely in a controlled offline simulation; results should be interpreted as evidence under these specific conditions and not directly generalized to production environments without additional validation. This study contributes a concrete experimental data point to the comparatively under-studied area of adversarial robustness for tree-based classifiers in network intrusion detection.

---

## 12. Future Work

This study opens several directions for future investigation. First, the feature-space perturbation used here — random Gaussian noise — is a heuristic proxy for real adversarial attacks. Future work should evaluate Random Forest IDS resilience against principled adversarial attacks such as gradient-based methods (FGSM, PGD) adapted for non-differentiable models through surrogate network approaches or decision-boundary attacks. Second, NSL-KDD is based on 1999 traffic data; replicating this experiment on more recent datasets — such as CICIDS2017, UNSW-NB15, or CIC-IDS-2018 — would establish whether the findings generalize to contemporary network environments and attack vectors. Third, the mechanism behind C3's substantial outperformance of C1 warrants further investigation: is the improvement primarily due to adversarial robustness, improved class balance from augmentation, or both? Controlled experiments varying augmentation volume independently of perturbation would clarify this. Fourth, ensemble adversarial training (Tramèr et al., 2018) could be evaluated to determine whether adversarial examples from multiple surrogate classifiers produce more generalizable defenses. Fifth, real-world validation — through live traffic monitoring, adversarial red-team evaluation, or deployment in a controlled network testbed — would provide operational evidence beyond what offline simulation can demonstrate.

---

## 8. Experimental Setup

All experiments were implemented in Python 3 using Google Colab (free tier, CPU runtime) via a single notebook (`code/adversarial-ids-complete.ipynb`). Libraries used: scikit-learn, NumPy, pandas, Matplotlib, Seaborn.

The NSL-KDD dataset was loaded from `KDDTrain+.txt` (~125,973 records, 43 columns) and `KDDTest+.txt` (~22,544 records, 43 columns). The pre-defined train/test split was preserved throughout; `train_test_split` was not used.

The baseline model used `RandomForestClassifier(n_estimators=100, random_state=42, n_jobs=-1)`. The adversarial attack evaluated three noise levels (std = 0.1, 0.3, 0.5) using `np.random.normal(mean=0, scale=std, random_state=42)`, applied to the top-5 features (`src_bytes`, `dst_bytes`, `same_srv_rate`, `dst_host_same_srv_rate`, `flag`, indices `[4, 5, 28, 33, 3]`) of attack-class test samples only. `DEFENSE_NOISE_STD = 0.3` was selected based on the resulting recall drop.

The adversarial training augmented dataset combined the full original training set with perturbed copies of all attack-class training samples (std=0.3), increasing the training set from ~125,973 to approximately 200,000+ samples with a higher proportion of attack-class examples. The defended classifier used identical hyperparameters to the baseline. All evaluation used scikit-learn's binary classification metrics with default settings.

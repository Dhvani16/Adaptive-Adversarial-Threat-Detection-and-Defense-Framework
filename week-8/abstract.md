# Week 8 — Abstract

---

## Abstract

Artificial intelligence-based intrusion detection systems (IDS) have achieved strong performance on standard network traffic benchmarks, yet their resilience under adversarial conditions remains insufficiently studied for non-differentiable classifiers such as Random Forest. This study evaluates the adversarial vulnerability of a Random Forest binary classifier trained on the NSL-KDD dataset and the effectiveness of adversarial training as a defense mechanism. A feature-space evasion attack was simulated by applying Gaussian noise (mean=0, std=0.3) to the five most important features (`src_bytes`, `dst_bytes`, `same_srv_rate`, `dst_host_same_srv_rate`, `flag`) of attack-class test samples; adversarial training was implemented by augmenting the training set with perturbed attack samples — labels preserved as attack=1 — and retraining an identical classifier. Three experimental conditions were evaluated: clean baseline (C1), under adversarial attack (C2), and post-defense (C3). The baseline classifier achieved accuracy of 0.7707, recall of 0.6188, and AUC-ROC of 0.9620; under adversarial attack (C2), recall dropped to 0.4621 — a reduction of 0.1567. Following adversarial training (C3), recall recovered to 0.9995 and F1-score reached 0.9886, substantially exceeding the clean baseline. These findings demonstrate that feature-space perturbation measurably degrades Random Forest IDS detection capability, and that adversarial training provides full recovery and significant improvement beyond baseline — likely due to improved generalization from the augmented attack-class training set. This work contributes a controlled experimental evaluation to the comparatively under-studied area of adversarial robustness for tree-based network intrusion detection systems.

---

**Word count:** ~220 words  
**Key metrics included:** C1 recall (0.6188), C2 recall (0.4621), C3 recall (0.9995), C3 F1 (0.9886)

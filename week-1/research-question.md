# Week 1 — Research Question, Objectives, Hypothesis & Scope

---

## Research Question

**Finalized:**
> *To what extent does adversarial training improve the robustness of a Random Forest-based intrusion detection system against feature-space evasion attacks, as evaluated on the NSL-KDD dataset?*

**Evaluation:** This question is specific (names the model, attack type, dataset, and defense), answerable (the three-condition experiment directly produces the answer), and realistic within 24 hours (no neural networks, no real traffic, no deployment required). No changes needed.

---

## Supporting Research Questions

1. What is the baseline detection performance of a Random Forest classifier trained and evaluated on clean NSL-KDD data, as measured by accuracy, recall, F1-score, and AUC-ROC?

2. How significantly does detection performance degrade when attack-class test samples are subjected to simulated feature-space evasion (Gaussian noise on the model's top-5 most important features)?

3. Does augmenting the training set with adversarial examples (adversarial training) measurably recover detection performance when the defended model is re-evaluated on the same adversarial test set?

4. What are the key limitations of using Gaussian feature perturbation as a proxy for real-world adversarial evasion, and what do they imply for interpreting the experimental results?

---

## Research Objectives

1. **To evaluate the baseline intrusion detection performance** of a Random Forest classifier on NSL-KDD under clean conditions, establishing a reference benchmark across accuracy, precision, recall, F1-score, and AUC-ROC.

2. **To quantify performance degradation** when the trained classifier is subjected to simulated feature-space evasion attacks (Gaussian noise at three magnitude levels: std = 0.1, 0.3, 0.5) applied to the top-5 features identified by `feature_importances_`.

3. **To evaluate whether adversarial training recovers detection performance** by retraining the classifier on a dataset augmented with adversarial examples, and measuring the change in recall and F1-score on the same adversarial test set used in Objective 2.

---

## Hypothesis

A Random Forest classifier trained on clean NSL-KDD data will exhibit a measurable reduction in recall and F1-score when evaluated on adversarially perturbed attack samples (Gaussian noise, std = 0.3). Retraining the classifier on a dataset augmented with adversarial examples will partially or fully recover this performance loss, with the degree of recovery depending on the noise magnitude used during augmentation.

---

## Scope

### In Scope — What this project WILL do

This case study will train a Random Forest binary classifier (scikit-learn, 100 trees, random_state=42) on the NSL-KDD dataset to distinguish normal traffic from attack traffic. It will simulate a feature-space evasion attack by applying Gaussian noise to the top-5 most important features of attack-class test samples at three noise levels. It will apply adversarial training as a defense mechanism and evaluate performance recovery across three conditions: clean baseline (C1), under attack (C2), and post-defense (C3). All experiments will be conducted in Google Colab using public data only. The project will produce a structured academic case study report of approximately 4,000–5,000 words.

### Out of Scope — What this project will NOT do

This project will not build, deploy, or test any production cybersecurity system. It will not implement gradient-based adversarial attacks (FGSM, PGD, C&W) — these require differentiable models and significantly exceed the 24-hour time budget. It will not use neural networks or deep learning. It will not test on real network traffic or attack any real system. It will not build a real-time adaptive defense mechanism, a dashboard, or any user interface. It will not survey more than 10–12 papers or write a full academic journal submission. Any feature beyond what is described in the in-scope section is explicitly excluded.

---

## Week 1 Complete

**Files created this week:**
- [week-1/glossary.md](glossary.md) — 6-entry personal glossary + ASCII pipeline diagram
- [week-1/papers-list.md](papers-list.md) — 9 candidate papers across 3 themes with verification status
- [week-1/research-question.md](research-question.md) — this file

**Next week (Week 2):** Deep dive into the literature. Days 1 and 2 will examine the papers identified this week in detail. Day 3 will finalize the research gap and produce a 400-word literature review draft.

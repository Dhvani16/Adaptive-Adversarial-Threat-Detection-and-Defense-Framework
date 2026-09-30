# Week 3 — Framework Design

---

## 1. Framework Component Descriptions

### Component 1 — Data Input Layer
**Name:** NSL-KDD Data Loader  
**Input:** Raw CSV files — `KDDTrain+.txt` (training) and `KDDTest+.txt` (test), no header row  
**Function:** Loads both files into pandas DataFrames using the standard NSL-KDD 43-column schema (41 features + label + difficulty score)  
**Output:** Two DataFrames: `train_df` and `test_df`

---

### Component 2 — Preprocessing Module
**Name:** Feature Preprocessor  
**Input:** Raw `train_df` and `test_df`  
**Function:**
1. Drop the `difficulty` column (not a feature)
2. Encode 3 categorical features (`protocol_type`, `service`, `flag`) with `LabelEncoder`
3. Map binary labels: `normal` → 0, all attack types → 1
4. Separate features (`X`) from labels (`y`)
5. Fit `StandardScaler` on `X_train` only; transform both `X_train` and `X_test`

**Output:** `X_train`, `X_test`, `y_train`, `y_test` — all numeric, normalized

---

### Component 3 — Baseline Detection Model
**Name:** Random Forest Classifier (Baseline)  
**Input:** `X_train`, `y_train`  
**Function:** Trains a `RandomForestClassifier(n_estimators=100, random_state=42)` on clean training data; captures `feature_importances_` for use in the attack module  
**Output:** Trained model object; `feature_importances_` array

---

### Component 4 — Adversarial Attack Module
**Name:** Feature-Space Perturbation Engine  
**Input:** `X_test` (attack-class rows only), `feature_importances_` from baseline model  
**Function:**
1. Identify the top-5 feature indices by importance
2. For noise levels `std ∈ {0.1, 0.3, 0.5}`: add Gaussian noise (`np.random.normal(0, std)`) to only those 5 features in attack-class test samples
3. Combine perturbed attack rows with unmodified normal rows to form 3 adversarial test sets

**Output:** Three adversarial test sets: `X_test_adv_01`, `X_test_adv_03`, `X_test_adv_05`

---

### Component 5 — Evaluation Layer
**Name:** Performance Evaluator  
**Input:** Trained model + test set (clean or adversarial)  
**Function:** Computes accuracy, precision, recall, F1-score, and AUC-ROC against the true labels; generates confusion matrix and ROC curve  
**Output:** Metrics dictionary; PNG figures

---

### Component 6 — Defense Module
**Name:** Adversarial Training Engine  
**Input:** `X_train`, `y_train` (clean), + adversarial training samples generated from attack-class rows in `X_train` at `std=0.3`  
**Function:**
1. Apply Gaussian noise (`std=0.3`) to top-5 features of attack-class rows in `X_train`
2. Label these perturbed rows as attack (1) — same label as the originals
3. Concatenate: `X_train_augmented = [X_train + perturbed attack rows]`
4. Retrain `RandomForestClassifier(n_estimators=100, random_state=42)` on augmented data

**Output:** Defended model object

---

### Component 7 — Comparison Output
**Name:** Three-Condition Comparator  
**Input:** Metrics from C1 (baseline), C2 (under attack), C3 (post-defense)  
**Function:** Compiles comparison table; generates grouped bar chart comparing F1/recall/accuracy across three conditions  
**Output:** Comparison table (Markdown); bar chart PNG

---

## 2. ASCII Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    DATA INPUT LAYER                             │
│  KDDTrain+.txt ──────────────────────── KDDTest+.txt            │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│                   PREPROCESSING MODULE                          │
│  1. Drop difficulty column                                      │
│  2. LabelEncode: protocol_type, service, flag                   │
│  3. Binary labels: normal=0, attack=1                           │
│  4. Separate X / y                                              │
│  5. StandardScaler fit on X_train, transform X_train + X_test   │
│                                                                 │
│  OUTPUT: X_train, X_test, y_train, y_test                       │
└───────────────────────────┬─────────────────────────────────────┘
                            │
                            ▼
┌─────────────────────────────────────────────────────────────────┐
│              BASELINE DETECTION MODEL                           │
│  RandomForestClassifier(n_estimators=100, random_state=42)      │
│  Trained on: X_train (clean)                                    │
│  Extracts: feature_importances_ → top 5 features identified     │
└─────────────────┬───────────────────────┬───────────────────────┘
                  │                       │
                  ▼                       ▼
    ┌─────────────────────┐   ┌─────────────────────────────┐
    │  C1 — BASELINE      │   │  ADVERSARIAL ATTACK MODULE  │
    │  Test: X_test clean │   │  Gaussian noise (std=0.1,   │
    │  → Accuracy, F1,    │   │  0.3, 0.5) on top-5 feats   │
    │    Recall, AUC      │   │  of attack-class test rows  │
    └─────────────────────┘   └─────────────┬───────────────┘
                                            │
                                            ▼
                              ┌─────────────────────────┐
                              │  C2 — UNDER ATTACK      │
                              │  Test: X_test_adv_03    │
                              │  → Drop in F1, Recall   │
                              └─────────────┬───────────┘
                                            │
                                            ▼
                              ┌─────────────────────────────┐
                              │  DEFENSE MODULE             │
                              │  Generate adv. training     │
                              │  samples (std=0.3 on        │
                              │  X_train attack rows)       │
                              │  Augment & retrain RF       │
                              └─────────────┬───────────────┘
                                            │
                                            ▼
                              ┌─────────────────────────┐
                              │  C3 — POST-DEFENSE      │
                              │  Test: X_test_adv_03    │
                              │  → Recovery in F1,      │
                              │    Recall               │
                              └─────────────┬───────────┘
                                            │
                  ┌─────────────────────────┘
                  │
                  ▼
    ┌─────────────────────────────────────────┐
    │         COMPARISON OUTPUT               │
    │  Three-condition table: C1 / C2 / C3    │
    │  Bar chart: F1, Recall, Accuracy        │
    │  Attack curve: Recall vs. noise level   │
    └─────────────────────────────────────────┘
```

---

## 3. Three-Condition Experimental Structure

| Condition | Name | Training data | Test data | Purpose |
|---|---|---|---|---|
| **C1** | Baseline | Clean `X_train` (NSL-KDD training set, preprocessed) | Clean `X_test` (NSL-KDD test set, preprocessed) | Establish reference performance of Random Forest on unperturbed data |
| **C2** | Under Attack | Same model as C1 — no retraining | `X_test_adv_03` — attack-class rows perturbed with Gaussian noise (std=0.3) | Measure performance degradation caused by feature-space evasion attack |
| **C3** | Post-Defense | Augmented training set: `X_train` + adversarially perturbed attack-class training rows (std=0.3) → retrain RF | Same `X_test_adv_03` as C2 | Measure whether adversarial training recovers detection performance |

---

## 4. [AI DRAFT — VERIFY] Proposed Framework Section (for Report)

[AI DRAFT — VERIFY]

### 6. Proposed Framework

This case study proposes a controlled experimental framework — the **Adaptive Adversarial Detection and Defense (AADD) Framework** — designed to evaluate the adversarial vulnerability of a machine learning-based intrusion detection system and to measure the effectiveness of adversarial training as a defense mechanism. The framework is not a production system; it is a structured experimental pipeline designed to produce measurable, comparable results across three controlled conditions.

As illustrated in Figure 1, the framework consists of seven components arranged in a sequential pipeline. The **Data Input Layer** ingests the NSL-KDD benchmark dataset, comprising a training file (KDDTrain+.txt, approximately 125,973 records) and a test file (KDDTest+.txt, approximately 22,544 records), each with 41 network traffic features. The **Preprocessing Module** performs feature encoding, binary label creation, and normalization, ensuring that all inputs to the classifier are in a consistent numerical format. StandardScaler is fitted exclusively on the training set to prevent data leakage.

The **Baseline Detection Model** is a Random Forest classifier (100 estimators, random_state=42) trained on the clean, preprocessed training data. This establishes the reference benchmark for Condition 1 (C1). The **Adversarial Attack Module** then applies Gaussian noise at three magnitude levels (std = 0.1, 0.3, 0.5) to the top-5 most important features of attack-class test samples, simulating an adversary who partially knows which features the model relies on. Performance under this attack is recorded as Condition 2 (C2).

The **Defense Module** implements adversarial training: the same perturbation strategy (std = 0.3) is applied to attack-class rows in the training set, generating adversarial training examples. The Random Forest is retrained on this augmented dataset. Performance of the defended model on the same adversarial test set defines Condition 3 (C3). Finally, the **Comparison Output** module compiles all three conditions into a comparison table and visualization, directly answering the primary research question. This framework maps one-to-one to the three research objectives defined in Section 3.

*[AI DRAFT — VERIFY: Ensure Figure 1 reference matches your actual diagram numbering. Confirm all component descriptions match your final implementation.]*

---

*Artifact created: Week 3, Day 1*  
*Next session (Day 2): Set up Google Colab and download NSL-KDD*

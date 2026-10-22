# Week 9 — Agentic Extension: Design Document

**Project**: Adaptive Adversarial Threat Detection and Defense Framework
**Notebook**: `code/agentic-adversarial-ids.ipynb`
**Builds on**: `code/adversarial-ids-complete.ipynb` (Phase 1)

---

## Overview

Phase 1 of this project used a static 3-condition experiment:
C1 (baseline RF) → C2 (one-shot Gaussian noise attack) → C3 (one-shot adversarial training defense).

Phase 2 replaces both the attack and the defense with **intelligent agents** that act
autonomously across multiple rounds. This transforms the experiment from a static
measurement into a dynamic adversarial game.

| Dimension | Phase 1 | Phase 2 |
|---|---|---|
| Attack mechanism | One-shot Gaussian noise | Agentic coordinate-descent (iterative, adaptive) |
| Defense mechanism | One-shot adversarial training | Adaptive monitoring + on-demand retraining |
| Interaction | Single pass | 4-round closed-loop game |
| Primary metric | Recall drop magnitude | Evasion rate, recall trajectory, convergence round |

---

## Agent Architecture

### RedAgent — Black-Box Coordinate Descent Attack

**Objective**: Cause the model to misclassify an attack-class sample as normal traffic.

**Algorithm**:
```
Input: sample x (attack class), model M, step_size, max_iter
Output: x_adv (perturbed sample), evasion_achieved, n_queries, n_iterations

1. x_adv ← copy(x)
2. For iteration in 1..max_iter:
   a. Query M.predict_proba(x_adv) → prob_attack
   b. If M.predict(x_adv) == 0: return (x_adv, evaded=True, n_queries)
   c. For each feature in top5_idx, for each direction in {-1, +1}:
      - x_try ← x_adv with feature nudged by ±step_size
      - Query M.predict_proba(x_try) → p
      - If p < best_prob: update best_prob, best_x ← x_try
   d. If no improvement found: break  (local minimum)
   e. x_adv ← best_x
3. Return (x_adv, evaded=False, n_queries)
```

**Key design decisions**:
- Black-box only: uses `predict_proba()` queries, no gradient access
- Operates on top-5 features only (same feature set as Phase 1)
- Fixed step_size=0.3 (matches Phase 1 noise std for comparability)
- max_iter=50 (budget cap to avoid infinite query loops)
- Coordinate descent (one feature at a time) — greedy, efficient

**Metrics produced**:
| Metric | Definition |
|---|---|
| evasion_rate | Fraction of attacked samples misclassified as normal |
| avg_queries | Mean queries used per successful evasion |
| avg_l2_dist | Mean L2 perturbation magnitude for evaded samples |
| n_iter | Iterations used (proxy for difficulty) |

**Hyperparameters**:
| Parameter | Value | Rationale |
|---|---|---|
| step_size | 0.3 | Matches Phase 1 noise std for fair comparison |
| max_iter | 50 | Sufficient to find evasion; caps query budget |
| max_samples | 500 | Subset of attack-class test rows; balances coverage vs runtime |

---

### BlueAgent — Adaptive Recall Monitor

**Objective**: Maintain recall ≥ 0.80 on adversarial test data by retraining when degradation is detected.

**Algorithm**:
```
Input: current model M, recall_threshold, X_train, y_train
Per round:
1. Evaluate recall on X_adv (red agent's output)
2. If recall < threshold:
   a. Generate adversarial training copies using create_adversarial_train()
   b. Augment training set: X_aug = [X_train | X_adv_copies]
   c. Retrain identical RF: new_model.fit(X_aug, y_aug)
   d. Re-evaluate recall on X_adv with new model
   e. Update self.model ← new_model
3. Log (round, recall_before, recall_after, retrained)
```

**Key design decisions**:
- Recall is used as the trigger metric, not accuracy — recall is the primary IDS metric
  (false negatives are intrusion misses; false positives are false alarms)
- Retraining uses the same `create_adversarial_train()` as Phase 1 — both phases
  use the same defense mechanism, making Phase 1 vs Phase 2 defense directly comparable
- The model is only retrained when needed (recall < 0.80), not every round —
  simulates a realistic IDS that avoids unnecessary overhead

**Hyperparameters**:
| Parameter | Value | Rationale |
|---|---|---|
| recall_threshold | 0.80 | Common IDS minimum acceptable detection rate |
| noise_std | 0.3 | Same as Phase 1 defense; ensures consistency |

---

## Multi-Round Game Loop

The game runs for N_ROUNDS = 4 iterations:

```
Round 0:
  - Red Agent attacks rf_baseline (the Phase 1 undefended model)
  - Blue Agent evaluates recall on adversarial examples
  - If recall < 0.80: Blue Agent retrains

Round 1:
  - Red Agent attacks blue_agent.model (the current defender, possibly retrained)
  - Blue Agent evaluates and adapts

... repeat for rounds 2 and 3 ...
```

The red agent always targets the **current** blue model, so if blue retrains in round 0,
red must evade a stronger model in round 1. This creates genuine strategic pressure
and tests whether the defense holds against a persistent intelligent attacker.

**Expected dynamics**:
- Round 0: High evasion rate (attacker vs undefended model), blue triggers retraining
- Round 1–2: Evasion rate drops (model now trained on adversarial examples), recall recovers
- Round 3: Possible re-escalation if attacker finds new evasion paths with same step_size

---

## New Figures

| Figure | Description | What it shows |
|---|---|---|
| Figure 8 | Bar chart: evasion rate comparison | Red Agent vs Gaussian noise Phase 1 baseline |
| Figure 9 | Line chart: recall trajectory across rounds | Recall before and after Blue Agent response per round, with retraining events marked |
| Figure 10 | Histogram: queries per evasion + L2 distribution | Red Agent query efficiency and perturbation magnitude |

---

## Phase 1 vs Phase 2 Comparison

| | Phase 1 | Phase 2 |
|---|---|---|
| **Attack** | Gaussian noise (random) | Coordinate-descent (adaptive, goal-directed) |
| **Defense** | Static adversarial training (once) | On-demand retraining (when recall < 0.80) |
| **Attack intelligence** | None — random perturbation | Full — iterative optimization toward evasion |
| **Defense intelligence** | None — one-shot | Full — monitors, detects, retrains autonomously |
| **Rounds** | 1 (single condition) | 4 (iterative game) |
| **Attack metric** | Recall drop | Evasion rate, avg_queries, avg_l2_dist |
| **Defense metric** | Final recall (C3) | Recall trajectory, convergence round, retrain count |
| **Primary finding (expected)** | Adversarial training recovers and improves recall | Adaptive defense stabilizes against intelligent attacker |

### Phase 1 reference metrics (from adversarial-ids-complete.ipynb)
| Condition | Accuracy | Recall | F1-Score |
|---|---|---|---|
| C1 Baseline | 0.7707 | 0.6188 | 0.7544 |
| C2 Under Attack (std=0.3) | 0.6815 | 0.4621 | 0.6229 |
| C3 Post-Defense | 0.9868 | 0.9995 | 0.9886 |
| Phase 1 Gaussian evasion rate | — | — | ~25% |

*(Phase 2 empirical values to be filled after running the notebook.)*

---

## New Metrics Defined in Phase 2

| Metric | Formula | Interpretation |
|---|---|---|
| evasion_rate | evaded / total_attacked | Fraction of attack samples that fooled the model |
| avg_queries | mean(n_queries for evaded) | Query budget needed per successful evasion |
| avg_l2_dist | mean(‖x_adv − x‖₂ for evaded) | Perturbation magnitude — smaller = more subtle |
| convergence_round | first round where recall ≥ threshold for all subsequent rounds | Speed of defense stabilization |

---

## Implementation Notes

### Reuse from Phase 1
- `create_adversarial_train()`: BlueAgent uses this directly (imported from same notebook)
- `RandomForestClassifier(n_estimators=100, random_state=42, n_jobs=-1)`: identical config
- `top5_idx`: same top-5 feature indices from rf_baseline.feature_importances_
- Preprocessing pipeline: StandardScaler, LabelEncoder (fitted on combined vocab)

### Standalone design
`agentic-adversarial-ids.ipynb` is fully self-contained — it reproduces Phase 1
preprocessing and baseline training rather than importing from Phase 1 notebook.
This ensures the notebook runs clean on any Colab session.

### Runtime estimate
- Phase 1 cells (preprocessing + baseline train): ~3 minutes
- RedAgent batch (500 samples × up to 50 iters × 10+1 queries/iter): ~6–8 minutes per round
- BlueAgent retraining: ~2 minutes per event
- Total (4 rounds, ~2 retraining events): ~35–45 minutes on Colab free CPU

---

## Limitations

1. **Fixed step_size**: The Red Agent uses a constant step_size=0.3. A stronger version
   could adapt step_size based on estimated boundary distance (e.g., exponential decay).

2. **Fixed defense augmentation**: The Blue Agent always generates training adversarial
   examples with noise_std=0.3. An enhanced version could observe the Red Agent's
   actual perturbation magnitude and match it.

3. **Shared test set across rounds**: All 4 rounds use the same 500-sample subset from
   X_test. In a production setting, each round would represent live traffic with fresh
   attack samples.

4. **No communication between agents**: The agents interact only through the model —
   the Red Agent cannot observe the Blue Agent's retraining, and the Blue Agent cannot
   observe the Red Agent's strategy. Real arms races would involve observation of
   each other's decisions.

5. **NSL-KDD limitations**: The dataset represents 1999-era attack traffic. Modern
   attacks (ransomware, APTs, zero-day exploits) are not represented.

---

## Week 9 Checklist

- [x] `code/agentic-adversarial-ids.ipynb` created
- [x] RedAgent class implemented (coordinate descent, black-box)
- [x] BlueAgent class implemented (recall monitoring + on-demand retrain)
- [x] 4-round game loop implemented
- [x] Figure 8 (evasion comparison), Figure 9 (recall trajectory), Figure 10 (queries histogram)
- [x] `week-9/agentic-design.md` written
- [ ] Run notebook end-to-end on Colab and record actual metrics
- [ ] Fill Phase 2 empirical values into comparison table above

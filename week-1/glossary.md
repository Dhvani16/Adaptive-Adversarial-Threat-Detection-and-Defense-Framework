# Week 1 — Personal Glossary
*6 core concepts explained in plain language*

---

## 1. AI-based Intrusion Detection System (IDS)

A software system that uses a machine learning model to automatically watch network traffic and decide whether each connection is normal or an attack — similar to a security guard who has studied thousands of past incidents and can spot a threat without being told what to look for every time.

---

## 2. Adversarial Attack on a Machine Learning Model

A deliberate attempt to trick a trained ML model by feeding it inputs that have been carefully modified to cause the wrong prediction — like subtly altering a stop sign so a self-driving car reads it as a speed limit sign, even though a human would still see a stop sign.

---

## 3. Evasion Attack

An adversarial attack that happens **at inference time** (after the model is already deployed) — the attacker modifies malicious input so it slips past the model undetected. This is different from a **poisoning attack**, which corrupts the *training data* before the model is even built. This project studies **evasion attacks only**.

---

## 4. Feature-Space Perturbation

A way to simulate an evasion attack on a non-differentiable model (like Random Forest) by adding small amounts of random noise to the numerical features that the model relies on most. Instead of mathematically computing the "perfect" tweak (which requires gradients), you nudge the values slightly — mimicking an attacker who roughly knows which traffic features trigger the detector and tries to disguise them.

---

## 5. Adversarial Training

A defense technique where you deliberately create adversarial examples, label them correctly, mix them into the original training data, and retrain the model. The idea: if the model has already seen "disguised" attacks during training, it becomes harder to fool with the same tricks later — like a security guard who has practiced spotting disguised intruders and is no longer fooled by common costumes.

---

## 6. Robustness in AI Security

A model is "robust" if its performance (accuracy, recall, F1) does not degrade significantly when attackers deliberately try to fool it. Robustness is measured by comparing performance under **clean conditions** (Condition 1) versus **adversarial conditions** (Condition 2), and then measuring how much a defense recovers that performance (Condition 3). A model that drops from 95% recall to 40% recall under attack is not robust; one that drops only to 88% is considered robust.

---

## ASCII Pipeline Diagram — How the 6 concepts connect

```
[NSL-KDD Network Traffic Data]
            │
            ▼
[AI-based IDS — Random Forest Classifier]   ← Concept 1
  trained on clean historical data
            │
    ┌───────┴────────┐
    │                │
    ▼                ▼
[Clean Test Data]  [Adversarially Perturbed Test Data]
                         │
                    Feature-Space Perturbation  ← Concept 4
                    (Gaussian noise on top features)
                         │
                         ▼ (Evasion Attack ← Concept 3)
              [Adversarial Attack on Model]  ← Concept 2
              Model misclassifies attacks as normal
                         │
                         ▼
              [Performance Drop Measured]
              (recall drops: model is NOT robust ← Concept 6)
                         │
                         ▼
              [Adversarial Training Defense]  ← Concept 5
              Retrain on clean + adversarial examples
                         │
                         ▼
              [Defended Model Re-evaluated]
              (recall recovers: model IS more robust ← Concept 6)
```

---

*Artifact created: Week 1, Day 1*
*Next session (Day 2): Search for research papers*

# Week 5 — Day 1
**Topic:** Adversarial Attack Theory and Design
**Role of AI today:** Teacher and experiment designer
**Estimated time:** ~60 minutes

---

## Copy-Paste Prompt

---

You are helping me with an 8-week academic cybersecurity case study. I am a beginner/intermediate student with approximately 1 hour available today.

---

**PROJECT TITLE:**
"Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems"

**PROJECT SUMMARY:**
Controlled academic experiment:
- Dataset: NSL-KDD binary classification (normal=0, attack=1)
- Model: Random Forest classifier (trained, baseline metrics recorded)
- Attack plan: Add Gaussian noise to the top 5 features of attack-class test samples at 3 noise levels
- Defense plan: Adversarial training (augmented retraining)
- Three conditions: C1 baseline / C2 under attack / C3 post-defense
- Tools: Python, Google Colab, scikit-learn, numpy, matplotlib

---

**CURRENT STAGE:**
Week 5, Day 1.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–4 complete:
  - Research question, literature review, framework design
  - Full preprocessing pipeline working (X_train, X_test, y_train, y_test ready)
  - Random Forest trained and evaluated — baseline (C1) metrics recorded in `week-4/results-baseline.md`
  - Top 5 most important feature indices identified and saved (`top5_idx`)
  - Three PNG figures saved: confusion matrix, ROC curve, feature importance chart

---

**TODAY'S OBJECTIVE:**
Understand the theory behind the adversarial attack I am about to implement, so I can explain and justify it in my methodology. Then design the attack precisely (what to do, which features, what noise levels, and what to measure).

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Teacher and experiment designer. Today is about understanding and planning — no coding yet. Help me understand the attack deeply enough to implement it tomorrow and defend it in writing.

---

**TODAY'S TASKS:**

**Task 1 — Explain the theory of evasion attacks (15 minutes):**

1. What is a feature-space evasion attack? How does an attacker manipulate input features to fool a classifier?
2. Why does Gaussian noise on important features simulate an evasion attack on a Random Forest? What is the underlying assumption this models?
3. What are the limitations of using Gaussian noise instead of a real adversarial example crafted by an attacker? (I need to include this honestly in my limitations section.)
4. Why do we only perturb attack-class samples (not normal traffic samples) in this experiment?
5. Why do we use `feature_importances_` to choose which features to perturb?

Keep explanations at beginner/intermediate level. Use an analogy if helpful.

**Task 2 — Explain the three noise levels (10 minutes):**

I plan to test three noise levels: std=0.1, std=0.3, std=0.5.

1. What does the standard deviation parameter control in Gaussian noise?
2. Why is it important to test multiple noise levels rather than just one?
3. How should I describe the "attack intensity" concept in my report?
4. Which noise level will I use for the defense phase, and how should I choose it? (Hint: the level that causes meaningful but not total degradation — why?)

**Task 3 — Design the attack experiment precisely (15 minutes):**

Help me write a precise, step-by-step attack procedure:

1. Start with the already-preprocessed test set (X_test, y_test) from Week 4
2. Identify which rows in X_test are attack-class (y_test == 1)
3. Make a copy of those rows
4. Add Gaussian noise (mean=0, std=X) to only the top 5 feature columns
5. Replace the attack rows in a new test array with the perturbed versions
6. Run the trained baseline model on this new test array
7. Record Accuracy, Recall, F1-score at this noise level
8. Repeat for std=0.1, 0.3, 0.5

Write this as a numbered procedure I can follow tomorrow when coding.

**Task 4 — Write the adversarial attack methodology subsection (15 minutes):**

Write a 150-word [AI DRAFT — VERIFY] paragraph explaining the adversarial attack design for my report's Methodology section. It should:
- Name the attack type (feature-space perturbation)
- Explain why it is a valid proxy for evasion
- Describe the noise parameter and the three levels tested
- State which features are perturbed and why
- Note the limitation (simulated, not a real attacker)

Mark it [AI DRAFT — VERIFY].

**Task 5 — Prepare tomorrow's session (5 minutes):**
Give me a brief checklist of what I need to have open/ready at the start of Day 2 (tomorrow) before I begin coding the attack.

---

**IMPORTANT CONSTRAINTS:**
- This is a theory and design session — no code today
- Do not fabricate statistics about how much attacks "typically" degrade models
- Be honest about the limitations of Gaussian noise as an attack proxy
- Keep everything within ethical bounds — this is a simulation, not an attack on any real system

**EXPECTED OUTPUT BY END OF SESSION:**
- Answers to all 5 theory questions (Task 1)
- Noise level explanation and selection rationale (Task 2)
- 8-step attack procedure written out (Task 3)
- 150-word [AI DRAFT] methodology paragraph (Task 4)
- Tomorrow's preparation checklist (Task 5)

**AT THE END OF THIS SESSION, PROVIDE:**
1. Everything formatted for `week-5/attack-design.md`
2. Reminder: "Next session (Day 2) we code and run the attack at all 3 noise levels."

---

## Definition of Done

- [ ] Can explain feature-space perturbation in my own words
- [ ] Can explain why we perturb only attack-class samples
- [ ] 8-step attack procedure written out
- [ ] Noise level selection rationale documented
- [ ] 150-word [AI DRAFT] methodology paragraph saved
- [ ] `week-5/attack-design.md` created

### Expected artifacts
- `week-5/attack-design.md` — theory notes + attack procedure + methodology paragraph

### Estimated time
~60 minutes

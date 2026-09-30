# Week 6 — Day 1
**Topic:** Adversarial Training Theory and Defense Design
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
- Dataset: NSL-KDD binary classification
- Baseline model: Random Forest (trained on clean data — C1 complete)
- Attack: Gaussian noise (std=DEFENSE_NOISE_STD) on top 5 features of attack-class samples (C2 complete)
- Defense: Adversarial training — retrain on augmented dataset (clean + adversarial training samples)
- Goal: Show whether adversarial training recovers detection performance (C3)
- Tools: Python, Google Colab, scikit-learn, numpy, matplotlib

---

**CURRENT STAGE:**
Week 6, Day 1.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–5 complete:
  - Research question, literature review, framework design
  - Preprocessing pipeline, baseline model (C1 metrics in `week-4/results-baseline.md`)
  - Adversarial attack at 3 noise levels (C2 metrics in `week-5/attack-results.md`)
  - Attack curve + confusion matrix for C2 saved
  - Defense noise level selected: `DEFENSE_NOISE_STD`
- I now know: the model's performance drops under attack. Today I design the defense.

---

**TODAY'S OBJECTIVE:**
Understand adversarial training theory in depth. Design the defense experiment precisely. End the session with a complete defense plan and a clear understanding of what to expect from the results.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Teacher and experiment designer. Today is theory and design only — coding begins Day 2. Help me understand adversarial training well enough to implement it, interpret results, and write about it accurately.

---

**TODAY'S TASKS:**

**Task 1 — Explain adversarial training theory (15 minutes):**

1. What is adversarial training in plain language? What is the core idea?
2. How does adding adversarial examples to the training set help the model generalize to adversarial inputs?
3. What assumption does adversarial training make about the attacker? (That the attacker will use the same type of perturbation seen during training)
4. What are the known failure modes of adversarial training? When does it NOT work?
5. Why is adversarial training considered a "basic" defense? What more sophisticated defenses exist that I am NOT implementing (and why I'm not)?

**Task 2 — Explain what "augmented training set" means in my experiment (10 minutes):**

Walk me through exactly how the augmented training set is created:
1. Start with the original clean training set: X_train, y_train
2. Take only the attack-class training samples (y_train == 1)
3. Apply the same perturbation (Gaussian noise, std=DEFENSE_NOISE_STD) to their top 5 features
4. Add these perturbed samples back to X_train WITH THEIR ORIGINAL LABELS (still label=1)
5. The augmented training set = original samples + adversarial copies

Why do we keep the labels as 1 (attack) for the adversarial training samples? What would happen if we mislabeled them?

**Task 3 — Predict what the results might show (10 minutes):**

Based on the theory, help me understand what different outcomes could mean:

| Outcome | What it means |
|---|---|
| C3 recall = C1 recall | Full recovery — defense worked perfectly |
| C3 recall > C2 but < C1 | Partial recovery — defense helped but did not fully solve the problem |
| C3 recall = C2 recall | No improvement — defense did not work at this noise level |
| C3 recall < C2 recall | Defense made things worse — would indicate a significant problem |

Which outcome is most likely? Which is most academically interesting to discuss?

**Task 4 — Write the defense methodology subsection (15 minutes):**

Write a 150-word [AI DRAFT — VERIFY] paragraph for the Methodology section describing the adversarial training defense. Include:
- What the augmented dataset contains
- How the defended model differs from the baseline
- Why this approach is expected to improve robustness
- The limitation: defense is specific to the type of perturbation seen during training

Mark [AI DRAFT — VERIFY].

**Task 5 — Prepare tomorrow's coding session (10 minutes):**

Give me a precise checklist of what to have ready in Colab at the start of Day 2:
- What variables must be loaded (X_train, y_train, X_test, y_test, top5_idx, DEFENSE_NOISE_STD, rf_baseline metrics)
- What code cells to re-run from previous notebooks
- What the first code cell of Day 2 will do

---

**IMPORTANT CONSTRAINTS:**
- Today is theory and planning only — no code
- Do not overclaim what adversarial training can achieve
- Be honest about its limitations
- Do not suggest more complex defenses (ensemble methods, certified defenses) for implementation — only mention them as future work

**EXPECTED OUTPUT BY END OF SESSION:**
- Answers to all 5 theory questions (Task 1)
- Augmented dataset construction explained clearly (Task 2)
- Outcome prediction table (Task 3)
- 150-word [AI DRAFT] defense methodology paragraph (Task 4)
- Day 2 preparation checklist (Task 5)

**AT THE END OF THIS SESSION, PROVIDE:**
1. Everything formatted for `week-6/defense-design.md`
2. Reminder: "Next session (Day 2) we implement adversarial training and evaluate C3."

---

## Definition of Done

- [ ] Can explain adversarial training in own words without notes
- [ ] Understand exactly how augmented dataset is constructed
- [ ] Outcome prediction table understood
- [ ] 150-word [AI DRAFT] defense methodology paragraph saved
- [ ] `week-6/defense-design.md` created

### Expected artifacts
- `week-6/defense-design.md` — theory notes + augmentation procedure + methodology paragraph

### Estimated time
~60 minutes

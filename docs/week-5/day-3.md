# Week 5 — Day 3
**Topic:** Attack Visualization and Documentation
**Role of AI today:** Programmer and writing assistant
**Estimated time:** ~60 minutes

---

## Copy-Paste Prompt

---

You are helping me with an 8-week academic cybersecurity case study. I am a beginner/intermediate student with approximately 1 hour available today. I am working in Google Colab.

---

**PROJECT TITLE:**
"Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems"

**PROJECT SUMMARY:**
Controlled academic experiment:
- Dataset: NSL-KDD binary classification
- Model: Random Forest (baseline metrics from Week 4)
- Attack: Gaussian noise on top 5 features of attack-class test samples at std=0.1, 0.3, 0.5
- Defense noise level selected: `DEFENSE_NOISE_STD` (chosen in Day 2)
- Tools: Python, Google Colab, matplotlib, seaborn

---

**CURRENT STAGE:**
Week 5, Day 3. Final session of Week 5.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–4 complete: research, framework, preprocessing, baseline model
- Week 5 Days 1–2 complete:
  - Attack theory understood and documented
  - Attack implemented at std=0.1, 0.3, 0.5
  - Real metrics recorded at all 3 noise levels in `week-5/attack-results.md`
  - Defense noise level selected (`DEFENSE_NOISE_STD`)
  - Comparison table (C1 vs. C2) complete

---

**TODAY'S OBJECTIVE:**
Generate two key visualizations: (1) the attack curve showing how recall drops as noise increases, and (2) a confusion matrix for Condition 2 (the selected attack noise level). Then write a short findings document describing what the attack demonstrated.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Programmer and writing assistant. Provide visualization code, help me interpret the graphs, and help me write the attack findings.

---

**TODAY'S TASKS:**

**Task 1 — Attack curve: recall vs. noise magnitude (20 minutes):**

Provide code to plot the attack curve:

```python
import matplotlib.pyplot as plt

noise_levels_plot = [0.0, 0.1, 0.3, 0.5]   # Include 0.0 = baseline

# I will fill in my actual values here:
recall_values = [rec_c1,   # noise=0.0 (baseline)
                 RECALL_01, # noise=0.1 (paste my actual value)
                 RECALL_03, # noise=0.3
                 RECALL_05] # noise=0.5

f1_values = [f1_c1,
             F1_01,
             F1_03,
             F1_05]

plt.figure(figsize=(8, 5))
plt.plot(noise_levels_plot, recall_values, marker='o', color='crimson',
         linewidth=2, label='Recall (Attack Detection Rate)')
plt.plot(noise_levels_plot, f1_values, marker='s', color='steelblue',
         linewidth=2, linestyle='--', label='F1-Score')
plt.axvline(x=DEFENSE_NOISE_STD, color='gray', linestyle=':', label=f'Selected defense level (std={DEFENSE_NOISE_STD})')
plt.xlabel('Gaussian Noise Standard Deviation', fontsize=12)
plt.ylabel('Score', fontsize=12)
plt.title('Attack Curve: Model Performance vs. Adversarial Noise Level', fontsize=13)
plt.ylim(0, 1.05)
plt.legend()
plt.grid(True, alpha=0.3)
plt.tight_layout()
plt.savefig('attack-curve.png', dpi=150)
plt.show()
print("Saved: attack-curve.png")
```

After I replace the placeholder values with my actual numbers and run the code, explain:
- What does this graph tell a reader about the model's vulnerability?
- How would I describe this graph in 2 sentences for the report?

**Task 2 — Confusion matrix for Condition 2 (10 minutes):**

Provide code to plot the confusion matrix for the selected attack level:

```python
X_adv_selected = create_adversarial_test(X_test, y_test, top5_idx,
                                          noise_std=DEFENSE_NOISE_STD)
y_pred_adv_selected = rf_baseline.predict(X_adv_selected)

cm_attack = confusion_matrix(y_test, y_pred_adv_selected)

plt.figure(figsize=(6, 5))
sns.heatmap(cm_attack, annot=True, fmt='d', cmap='OrRd',
            xticklabels=['Normal', 'Attack'],
            yticklabels=['Normal', 'Attack'])
plt.title(f'Confusion Matrix — Condition 2: Under Attack (std={DEFENSE_NOISE_STD})')
plt.ylabel('True Label')
plt.xlabel('Predicted Label')
plt.tight_layout()
plt.savefig('confusion-matrix-attack.png', dpi=150)
plt.show()
```

Compare this confusion matrix to the baseline one from Week 4. What changed?

**Task 3 — Write the attack findings document (20 minutes):**

Using my actual numbers, help me write a 250-word findings document for `week-5/attack-findings.md`:

**Section: Adversarial Attack Results (Condition 2)**

Structure:
1. Opening sentence: what the attack did
2. Results at each noise level (table format, actual numbers)
3. What the attack curve shows (reference the figure)
4. The specific noise level chosen for defense and why
5. What this demonstrates about Random Forest vulnerability to feature perturbation
6. One honest caveat: this is simulated noise, not a real attacker

Mark it [AI DRAFT — VERIFY].

**Task 4 — Week 5 wrap-up (10 minutes):**

Summarize:
- What Week 5 accomplished
- All artifacts created
- What variables must remain available in my notebook for Week 6 (notably: `DEFENSE_NOISE_STD`, `X_adv_selected`, `y_pred_adv_selected`)
- Preview: Week 6 will implement adversarial training and compare all 3 conditions

---

**IMPORTANT CONSTRAINTS:**
- All graphs must use my actual experimental values — not placeholder numbers
- Results paragraph must use my real numbers, not invented ones
- Save both PNG files with descriptive names
- Do not start the defense implementation today

**EXPECTED OUTPUT BY END OF SESSION:**
- `attack-curve.png` saved
- `confusion-matrix-attack.png` saved
- 250-word [AI DRAFT] attack findings document
- Week 5 complete

**AT THE END OF THIS SESSION, PROVIDE:**
1. Both figure-saving code cells
2. The [AI DRAFT] attack findings document
3. List of Week 5 artifacts
4. Reminder: "Week 5 complete. Week 6: implement adversarial training and compare all 3 conditions."

---

## Definition of Done

- [ ] Attack curve PNG saved (recall + F1 vs. noise level, with selected level marked)
- [ ] Confusion matrix for C2 saved
- [ ] 250-word attack findings document written with actual numbers
- [ ] All artifacts saved to `week-5/`

### Expected artifacts
- `week-5/attack-curve.png`
- `week-5/confusion-matrix-attack.png`
- `week-5/attack-findings.md` — findings with actual numbers
- `week-5/notebook-attack.ipynb` — all attack code

### Week 5 is complete when you have
- `week-5/attack-design.md`
- `week-5/attack-results.md` (actual numbers)
- `week-5/attack-findings.md`
- Two PNG figures saved

### Estimated time
~60 minutes

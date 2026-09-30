# Week 6 — Day 3
**Topic:** Three-Condition Comparison Visualization and Experiment Wrap-Up
**Role of AI today:** Programmer and analyst
**Estimated time:** ~60 minutes

---

## Copy-Paste Prompt

---

You are helping me with an 8-week academic cybersecurity case study. I am a beginner/intermediate student with approximately 1 hour available today. I am working in Google Colab.

---

**PROJECT TITLE:**
"Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems"

**PROJECT SUMMARY:**
Controlled academic experiment — all three conditions now complete:
- C1 Baseline: Random Forest on clean data (metrics in `week-4/results-baseline.md`)
- C2 Under Attack: Same model on adversarially perturbed data (metrics in `week-5/attack-results.md`)
- C3 Post-Defense: Defended model (adversarial training) on same adversarial data (metrics in `week-6/defense-results.md`)
- Tools: Python, Google Colab, matplotlib, seaborn

---

**CURRENT STAGE:**
Week 6, Day 3. This is the final experimental session — all coding ends today.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–5 complete: research, framework, preprocessing, C1 baseline, C2 attack
- Week 6 Days 1–2 complete:
  - Adversarial training theory understood
  - Defended model trained on augmented dataset
  - C3 metrics recorded in `week-6/defense-results.md`
  - Three-condition summary table created

---

**TODAY'S OBJECTIVE:**
Generate the final comparison visualizations (grouped bar chart and confusion matrix for C3). Write a concise comparison summary. Officially close the experimental phase — no more coding after today.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Programmer and analyst. Provide visualization code, help me interpret the three-condition comparison, and help me close the experimental record cleanly.

---

**TODAY'S TASKS:**

**Task 1 — Three-condition grouped bar chart (20 minutes):**

I will provide my actual C1, C2, C3 numbers. Provide code to generate a publication-quality grouped bar chart:

```python
import matplotlib.pyplot as plt
import numpy as np

# Replace with my actual values:
metrics_labels = ['Accuracy', 'Precision', 'Recall', 'F1-Score', 'AUC-ROC']
c1_vals = [ACC_C1, PREC_C1, REC_C1, F1_C1, AUC_C1]
c2_vals = [ACC_C2, PREC_C2, REC_C2, F1_C2, AUC_C2]
c3_vals = [ACC_C3, PREC_C3, REC_C3, F1_C3, AUC_C3]

x = np.arange(len(metrics_labels))
width = 0.25

fig, ax = plt.subplots(figsize=(10, 6))
bars1 = ax.bar(x - width, c1_vals, width, label='C1: Baseline',     color='steelblue')
bars2 = ax.bar(x,         c2_vals, width, label='C2: Under Attack',  color='crimson')
bars3 = ax.bar(x + width, c3_vals, width, label='C3: Post-Defense',  color='forestgreen')

ax.set_xlabel('Metric', fontsize=12)
ax.set_ylabel('Score', fontsize=12)
ax.set_title('Three-Condition Performance Comparison\n(Baseline vs. Attack vs. Defense)', fontsize=13)
ax.set_xticks(x)
ax.set_xticklabels(metrics_labels)
ax.set_ylim(0, 1.1)
ax.legend()
ax.grid(axis='y', alpha=0.3)

# Add value labels on bars
for bar in [bars1, bars2, bars3]:
    for b in bar:
        ax.annotate(f'{b.get_height():.2f}',
                    xy=(b.get_x() + b.get_width()/2, b.get_height()),
                    xytext=(0, 3), textcoords="offset points",
                    ha='center', va='bottom', fontsize=8)

plt.tight_layout()
plt.savefig('comparison-barchart.png', dpi=150)
plt.show()
print("Saved: comparison-barchart.png")
```

After I fill in my actual numbers and run the code, help me describe this chart in 2–3 sentences for the report.

**Task 2 — Confusion matrix for Condition 3 (10 minutes):**

```python
cm_defense = confusion_matrix(y_test, y_pred_defended)

plt.figure(figsize=(6, 5))
sns.heatmap(cm_defense, annot=True, fmt='d', cmap='Greens',
            xticklabels=['Normal', 'Attack'],
            yticklabels=['Normal', 'Attack'])
plt.title(f'Confusion Matrix — Condition 3: Post-Defense (std={DEFENSE_NOISE_STD})')
plt.ylabel('True Label')
plt.xlabel('Predicted Label')
plt.tight_layout()
plt.savefig('confusion-matrix-defense.png', dpi=150)
plt.show()
```

Compare this to the C2 confusion matrix. What changed in the False Negative count?

**Task 3 — Write the three-condition comparison table (10 minutes):**

Help me create a clean final comparison table using my actual values:

```
=== FINAL THREE-CONDITION COMPARISON ===
Noise level used for attack and defense: std=DEFENSE_NOISE_STD

| Condition        | Accuracy | Precision | Recall | F1-Score | AUC-ROC |
|------------------|----------|-----------|--------|----------|---------|
| C1: Baseline     | X.XXXX   | X.XXXX    | X.XXXX | X.XXXX   | X.XXXX  |
| C2: Under Attack | X.XXXX   | X.XXXX    | X.XXXX | X.XXXX   | X.XXXX  |
| C3: Post-Defense | X.XXXX   | X.XXXX    | X.XXXX | X.XXXX   | X.XXXX  |

Change C1→C2: Recall dropped by X.XX points
Change C2→C3: Recall recovered by X.XX points
Net change C1→C3: Recall difference of X.XX points
```

Fill this in with my actual numbers after I provide them.

**Task 4 — Write a 3-paragraph experiment summary (15 minutes):**

Using my actual results, write a 3-paragraph [AI DRAFT — VERIFY] experiment summary:

- **Paragraph 1 (C1):** Baseline performance — what the model achieved on clean data
- **Paragraph 2 (C2):** Attack results — how much performance dropped and why
- **Paragraph 3 (C3):** Defense results — how much adversarial training helped (or didn't), and what this means

Mark [AI DRAFT — VERIFY]. I will verify every number and claim.

**Task 5 — Close the experimental record (5 minutes):**

Provide a final checklist of everything I must have saved before moving to Week 7 writing:
- List all notebook files
- List all PNG figures
- List all results markdown files
- Confirm all actual numbers are saved (not just in Colab memory)

---

**IMPORTANT CONSTRAINTS:**
- Use only my actual experimental numbers — no suggested or invented values
- After today, the experimental phase is CLOSED — Week 7 and 8 are writing only
- Do not suggest running additional experiments or testing more noise levels
- All figures must be saved as PNG with descriptive names

**EXPECTED OUTPUT BY END OF SESSION:**
- `comparison-barchart.png` saved
- `confusion-matrix-defense.png` saved
- Final three-condition comparison table (with actual numbers)
- 3-paragraph [AI DRAFT] experiment summary
- Complete experimental record confirmed

**AT THE END OF THIS SESSION, PROVIDE:**
1. Both figure-saving code cells
2. Three-condition table with my actual numbers
3. The 3-paragraph [AI DRAFT] summary
4. Complete artifact checklist
5. Reminder: "Experiments are complete. Week 7 is writing and analysis. Do NOT add new experiments."

---

## Definition of Done

- [ ] Grouped bar chart PNG saved (C1/C2/C3 comparison)
- [ ] Confusion matrix for C3 PNG saved
- [ ] Final three-condition comparison table complete with actual numbers
- [ ] 3-paragraph experiment summary written
- [ ] All experiment artifacts confirmed saved

### Expected artifacts
- `week-6/comparison-barchart.png`
- `week-6/confusion-matrix-defense.png`
- `week-6/comparison-table.md` — final 3-condition table
- `week-6/experiment-summary.md` — 3-paragraph summary

### Week 6 is complete when you have
- `week-6/defense-design.md`
- `week-6/defense-results.md` (actual numbers)
- `week-6/comparison-table.md`
- `week-6/experiment-summary.md`
- Two PNG figures saved
- ALL experimental work complete (no more coding from Week 7 onward)

### Estimated time
~60 minutes

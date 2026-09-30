# Week 4 — Day 3
**Topic:** Baseline Visualizations and Documenting Results
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
- Dataset: NSL-KDD binary classification (normal=0, attack=1)
- Model: Random Forest (100 trees, random_state=42)
- Three conditions: C1 baseline / C2 under attack / C3 post-defense
- Tools: Python, Google Colab, scikit-learn, matplotlib, seaborn

---

**CURRENT STAGE:**
Week 4, Day 3. Final session of Week 4.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–3 complete: research question, literature review, framework, environment setup
- Week 4 Days 1–2 complete:
  - Full preprocessing pipeline working
  - Random Forest trained on clean data
  - Baseline metrics recorded in `week-4/results-baseline.md`:
    - Accuracy, Precision, Recall, F1-Score, AUC-ROC (actual numbers from my experiment)
  - Top 5 feature indices identified and saved (needed for Week 5 attack)
  - Results table started (C1 filled in, C2/C3 as TBD)

---

**TODAY'S OBJECTIVE:**
Generate the baseline visualizations (confusion matrix, ROC curve, feature importance bar chart), save them as PNG files, and write a short Results subsection describing the baseline performance for the report.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Programmer and writing assistant. Provide visualization code, help me save figures correctly, and help me write the baseline results description.

---

**TODAY'S TASKS:**

**Task 1 — Confusion matrix (15 minutes):**

Provide code to plot and save a confusion matrix:

```python
from sklearn.metrics import confusion_matrix
import seaborn as sns

cm = confusion_matrix(y_test, y_pred_baseline)

plt.figure(figsize=(6, 5))
sns.heatmap(cm, annot=True, fmt='d', cmap='Blues',
            xticklabels=['Normal', 'Attack'],
            yticklabels=['Normal', 'Attack'])
plt.title('Confusion Matrix — Condition 1: Baseline')
plt.ylabel('True Label')
plt.xlabel('Predicted Label')
plt.tight_layout()
plt.savefig('confusion-matrix-baseline.png', dpi=150)
plt.show()
print("Saved: confusion-matrix-baseline.png")
```

After I run this, explain how to read the confusion matrix:
- What are True Positives, True Negatives, False Positives, False Negatives in IDS terms?
- What does a large number in the False Negative cell mean for security?

**Task 2 — ROC curve (15 minutes):**

Provide code to plot and save the ROC curve:

```python
from sklearn.metrics import roc_curve

fpr, tpr, _ = roc_curve(y_test, y_prob_baseline)

plt.figure(figsize=(6, 5))
plt.plot(fpr, tpr, color='steelblue', lw=2,
         label=f'Baseline ROC (AUC = {auc_c1:.4f})')
plt.plot([0, 1], [0, 1], color='gray', linestyle='--', label='Random classifier')
plt.xlabel('False Positive Rate')
plt.ylabel('True Positive Rate')
plt.title('ROC Curve — Condition 1: Baseline')
plt.legend()
plt.tight_layout()
plt.savefig('roc-baseline.png', dpi=150)
plt.show()
print("Saved: roc-baseline.png")
```

Explain: what does AUC-ROC tell me about this classifier? How do I describe this graph in my report?

**Task 3 — Feature importance bar chart (10 minutes):**

Provide code to plot the top 10 feature importances:

```python
top10_names  = [feature_names[i] for i in top10_idx]
top10_values = importances[top10_idx]

plt.figure(figsize=(8, 5))
plt.barh(top10_names[::-1], top10_values[::-1], color='steelblue')
plt.xlabel('Importance Score')
plt.title('Top 10 Feature Importances — Random Forest Baseline')
plt.tight_layout()
plt.savefig('feature-importance-baseline.png', dpi=150)
plt.show()
print("Saved: feature-importance-baseline.png")
```

Explain: why are these features important? How will the top 5 be used in the adversarial attack?

**Task 4 — Write the baseline results sub-section (15 minutes):**

Using MY actual metric numbers (which I will paste here), write a 200-word [AI DRAFT — VERIFY] paragraph for the Results section describing Condition 1 (Baseline):

The paragraph should:
- State the metrics achieved (with actual numbers)
- Note which metric is most important for IDS (recall — why?)
- Reference the confusion matrix and ROC curve figures
- Set up what comes next (adversarial attack in the next condition)

Mark it [AI DRAFT — VERIFY]. I will review every number before including it in the report.

**Task 5 — Week 4 wrap-up (5 minutes):**

Summarize what Week 4 accomplished:
- List all artifacts created this week
- Confirm what variables I need to keep available in my notebook for Week 5
- Preview what Week 5 will do (adversarial attack simulation)

---

**IMPORTANT CONSTRAINTS:**
- All figures must be saved as PNG files with descriptive names
- The results paragraph must use MY actual numbers — not suggested numbers
- Do not start the adversarial attack code today
- If my confusion matrix shows unexpected results (e.g. very high false negatives), flag it and help me interpret rather than dismiss

**EXPECTED OUTPUT BY END OF SESSION:**
- `confusion-matrix-baseline.png` saved
- `roc-baseline.png` saved
- `feature-importance-baseline.png` saved
- 200-word [AI DRAFT] baseline results paragraph
- Week 4 complete summary

**AT THE END OF THIS SESSION, PROVIDE:**
1. All three figure-saving code cells in one block
2. The [AI DRAFT] results paragraph with my actual numbers
3. List of Week 4 artifacts
4. Reminder: "Week 4 complete. Week 5: simulate the adversarial evasion attack."

---

## Definition of Done

- [ ] Confusion matrix PNG saved
- [ ] ROC curve PNG saved
- [ ] Feature importance chart PNG saved
- [ ] 200-word baseline results paragraph written with actual numbers
- [ ] Figures moved to `week-4/` folder
- [ ] `week-4/results-baseline.md` updated with paragraph + figure filenames

### Expected artifacts
- `week-4/confusion-matrix-baseline.png`
- `week-4/roc-baseline.png`
- `week-4/feature-importance-baseline.png`
- `week-4/results-baseline.md` — metrics + interpretation paragraph

### Week 4 is complete when you have
- `week-4/notebook-baseline.ipynb` (all preprocessing + training + eval + viz cells)
- `week-4/results-baseline.md` (actual metric values + results paragraph)
- Three PNG figures saved

### Estimated time
~60 minutes

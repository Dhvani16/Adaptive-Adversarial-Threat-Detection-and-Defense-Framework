# Week 8 — Day 2
**Topic:** Report Integration and Formatting
**Role of AI today:** Academic writing assistant and editor
**Estimated time:** ~60 minutes

---

## Copy-Paste Prompt

---

You are helping me with an 8-week academic cybersecurity case study. I am a beginner/intermediate student with approximately 1 hour available today. This is the penultimate session — everything is written, now I need to combine and polish.

---

**PROJECT TITLE:**
"Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems"

**PROJECT SUMMARY:**
Completed academic experiment:
- Dataset: NSL-KDD binary classification
- Model: Random Forest (adversarially trained)
- Attack: Gaussian feature perturbation
- Defense: Adversarial training
- Three conditions: C1 Baseline / C2 Under Attack / C3 Post-Defense
- Report target: ~4,000–5,000 words

---

**CURRENT STAGE:**
Week 8, Day 2.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–7 fully complete, all experiments done
- Week 8 Day 1 complete:
  - Abstract drafted
  - Conclusion drafted
  - Future Work drafted
  - Experimental Setup drafted
  - Reference list compiled and formatted
  - All saved in `week-8/` folder

- `week-7/report-draft.md` contains:
  - Introduction, Problem Statement, Objectives, Hypothesis
  - Background / Literature Review
  - Methodology
  - Results
  - Discussion
  - Limitations

---

**TODAY'S OBJECTIVE:**
Combine all sections into one complete, coherent final report document. Fix flow, transitions, figure numbering, and section numbering. Check word count. The output is `week-8/final-report.md` — the complete draft that will be reviewed in Day 3.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Academic writing assistant and editor. Help me integrate all sections, improve flow and transitions, ensure consistent formatting, and check the overall document structure.

---

**TODAY'S TASKS:**

**Task 1 — Define the final report structure (5 minutes):**

Confirm the exact section order and numbering:

```
Title Page
Abstract

1. Introduction
2. Problem Statement
3. Research Objectives
4. Background and Literature Review
   4.1 ML-Based Intrusion Detection Systems
   4.2 Adversarial Attacks on ML Cybersecurity Models
   4.3 Adversarial Training as Defense
5. Research Gap
6. Proposed Framework
7. Methodology
   7.1 Dataset
   7.2 Preprocessing
   7.3 Baseline Model
   7.4 Adversarial Attack Design
   7.5 Defense Mechanism
   7.6 Evaluation Metrics
8. Experimental Setup
9. Results
   9.1 Condition 1: Baseline Performance
   9.2 Condition 2: Performance Under Attack
   9.3 Three-Condition Comparison
10. Discussion
11. Limitations
12. Future Work
13. Conclusion
References
```

If anything is missing from my draft, flag it and tell me how to fill it quickly.

**Task 2 — Assemble the complete document (25 minutes):**

I will paste each section in sequence. For each one:
1. Check that it starts and ends cleanly (no orphan sentences)
2. Improve the transition to the next section (1–2 connecting sentences)
3. Check that the section achieves its purpose
4. Flag any sentence that contradicts another section

Work section by section. Do not rewrite everything — improve transitions and catch inconsistencies only.

**Task 3 — Figure and table numbering (10 minutes):**

Create a figure and table index:

| Number | File | Caption | Referenced in section |
|---|---|---|---|
| Figure 1 | confusion-matrix-baseline.png | Confusion matrix — C1 Baseline | Section 9.1 |
| Figure 2 | roc-baseline.png | ROC curve — C1 Baseline | Section 9.1 |
| Figure 3 | feature-importance-baseline.png | Top 10 feature importances | Section 9.1 |
| Figure 4 | attack-curve.png | Recall vs. noise magnitude | Section 9.2 |
| Figure 5 | confusion-matrix-attack.png | Confusion matrix — C2 Under Attack | Section 9.2 |
| Figure 6 | comparison-barchart.png | Three-condition comparison | Section 9.3 |
| Figure 7 | confusion-matrix-defense.png | Confusion matrix — C3 Post-Defense | Section 9.3 |
| Table 1 | (inline) | Three-condition comparison metrics | Section 9.3 |

Check that every figure is referenced at least once in the text. Flag any figure that is not referenced.

**Task 4 — Word count check (5 minutes):**

After I paste the assembled document, estimate the word count by section:
- If any section is significantly too short, tell me which sentence(s) to expand
- If any section is significantly over the target length, suggest what to trim
- Confirm the total is within 4,000–5,500 words

**Task 5 — Final consistency check (15 minutes):**

Check the assembled document for:
1. **Number consistency:** Every metric value in the Abstract, Introduction, Results, and Conclusion should match — flag any discrepancy
2. **Scope consistency:** Does any section claim something outside the defined scope? (Real-world deployment, neural networks, unsimulated attacks?)
3. **Citation consistency:** Are all cited papers in the reference list? Are all reference list papers cited in text?
4. **Tense consistency:** Results and methodology should be past tense; introduction and discussion can be present tense
5. **Objective coverage:** Is each of the 3 research objectives addressed somewhere in the report?

---

**IMPORTANT CONSTRAINTS:**
- Do not rewrite sections from scratch — only improve flow and transitions
- Do not add new experiments or claims not supported by existing data
- All numbers must remain consistent throughout the document
- Do not expand the scope of the report

**EXPECTED OUTPUT BY END OF SESSION:**
- `week-8/final-report.md` — complete integrated report
- Figure/table index
- Word count by section
- List of remaining issues to fix in Day 3

**AT THE END OF THIS SESSION, PROVIDE:**
1. Confirmation that `week-8/final-report.md` is assembled
2. Figure/table index
3. List of items flagged for Day 3 review (inconsistencies, gaps, [VERIFY] tags remaining)
4. Reminder: "Final session (Day 3) is proofread and final validation."

---

## Definition of Done

- [ ] All sections assembled into `week-8/final-report.md` in correct order
- [ ] All transitions between sections improved
- [ ] Figure numbering consistent throughout
- [ ] Word count checked (~4,000–5,500 words)
- [ ] Consistency check run (numbers, scope, citations, objectives)

### Expected artifacts
- `week-8/final-report.md` — complete assembled report (rough final)

### Estimated time
~60 minutes

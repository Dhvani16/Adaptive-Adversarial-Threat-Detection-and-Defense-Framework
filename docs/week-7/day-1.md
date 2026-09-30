# Week 7 — Day 1
**Topic:** Writing the Results Section
**Role of AI today:** Academic writing assistant
**Estimated time:** ~60 minutes

---

## Copy-Paste Prompt

---

You are helping me with an 8-week academic cybersecurity case study. I am a beginner/intermediate student with approximately 1 hour available today. The experimental phase is fully complete — today is writing only.

---

**PROJECT TITLE:**
"Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems"

**PROJECT SUMMARY:**
Completed academic experiment:
- Dataset: NSL-KDD binary classification (normal=0, attack=1)
- Model: Random Forest (100 trees, random_state=42)
- Attack: Gaussian noise (std=DEFENSE_NOISE_STD) on top 5 features of attack-class test samples
- Defense: Adversarial training (retrained on clean + adversarial training samples)
- Three conditions measured: C1 Baseline / C2 Under Attack / C3 Post-Defense
- Final output: Academic case study report (~4,000–5,000 words)

---

**CURRENT STAGE:**
Week 7, Day 1.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–6 fully complete:
  - Week 1: research question, objectives, hypothesis, scope
  - Week 2: literature review draft, research gap, reference list
  - Week 3: framework design, dataset exploration, methodology draft
  - Week 4: preprocessing, baseline model (C1) — metrics + 3 figures saved
  - Week 5: adversarial attack (C2) — metrics + 2 figures saved
  - Week 6: adversarial training defense (C3) — metrics + 2 figures saved, 3-condition comparison table complete
- All experimental results saved in markdown files in `week-4/`, `week-5/`, `week-6/`
- No more experiments will be run — writing phase begins today

---

**TODAY'S OBJECTIVE:**
Write the complete Results section of the case study report. The results section presents the experimental data clearly — what was measured, in what conditions, with what numbers. It describes but does not yet interpret (interpretation comes in the Discussion section).

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Academic writing assistant. You help me draft and structure the results section. I provide the actual numbers — you help me write about them clearly. All numbers must come from my experiments.

---

**TODAY'S TASKS:**

**Task 1 — Understand what a Results section is (5 minutes):**

Briefly explain:
- What belongs in a Results section vs. a Discussion section
- What the "present, don't interpret" principle means
- How to reference figures and tables in academic writing (e.g., "As shown in Figure 1...")

**Task 2 — Results section structure (5 minutes):**

Propose the structure of my Results section:
- 9.1 Condition 1: Baseline Performance
- 9.2 Condition 2: Performance Under Adversarial Attack
- 9.3 Three-Condition Comparison

Confirm this structure, or suggest a better one if needed.

**Task 3 — Draft 9.1: Baseline Performance (15 minutes):**

I will paste my actual C1 metrics here. Using those numbers, write a 150-word [AI DRAFT — VERIFY] paragraph that:
- States all 5 metrics clearly (Accuracy, Precision, Recall, F1, AUC)
- Notes which metric is most relevant to IDS evaluation and why (recall)
- References the confusion matrix and ROC curve figures by name (Figure 1, Figure 2)
- Ends with 1 sentence that leads into the next sub-section (the adversarial attack)

**Task 4 — Draft 9.2: Performance Under Adversarial Attack (20 minutes):**

I will paste my actual C2 metrics (at all 3 noise levels) here. Write a 200-word [AI DRAFT — VERIFY] sub-section that:
- Presents results at noise levels 0.1, 0.3, 0.5 in a table
- Describes the trend (increasing noise → increasing degradation)
- States which noise level was selected for the defense phase and the chosen metrics at that level
- References the attack curve figure
- Does NOT yet explain WHY this happened (that goes in Discussion)

**Task 5 — Draft 9.3: Three-Condition Comparison (10 minutes):**

I will paste the three-condition comparison table. Write a 150-word [AI DRAFT — VERIFY] sub-section that:
- Presents the comparison table (C1 / C2 / C3)
- States the metric changes numerically (e.g., "Recall dropped from X to Y in C2, and recovered to Z in C3")
- References the comparison bar chart
- Uses precise, factual language — no interpretation yet

**Task 6 — Assemble the complete Results section (5 minutes):**

Combine all three sub-sections into one clean Results section ready to paste into `week-7/report-draft.md`.

---

**IMPORTANT CONSTRAINTS:**
- Every number in the Results section must come from MY actual experiments — never from AI suggestion
- Use [VERIFY] tags next to any specific claim I should double-check against my notebook
- Results = presentation of data only. Save all interpretation for the Discussion section
- All figures must be referenced by number (Figure 1, Figure 2, etc.)
- Do not fabricate experimental outcomes

**EXPECTED OUTPUT BY END OF SESSION:**
- Complete Results section draft (~500 words total)
- Three sub-sections with actual numbers
- All figures referenced by number
- `week-7/report-draft.md` created with Results section inside

**HOW TO WORK WITH ME:**
- Ask me to paste my actual metric values before drafting
- Write one sub-section at a time
- Mark all drafted text [AI DRAFT — VERIFY]

**AT THE END OF THIS SESSION, PROVIDE:**
1. Complete Results section (formatted, ready to paste)
2. A list of figure numbers and what each figure is (for consistency across the report)
3. Reminder: "Next session (Day 2) we write the Discussion and Limitations sections."

---

## Definition of Done

- [ ] Results section drafted (~500 words)
- [ ] All 3 sub-sections present (9.1, 9.2, 9.3)
- [ ] All numbers verified as matching my experiment files
- [ ] All figures referenced by number
- [ ] `week-7/report-draft.md` created with Results section

### Expected artifacts
- `week-7/report-draft.md` — start this file today; it will grow across all 3 days this week

### Estimated time
~60 minutes

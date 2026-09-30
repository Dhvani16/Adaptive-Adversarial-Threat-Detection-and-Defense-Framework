# Week 8 — Day 3
**Topic:** Final Review, Validation, and Submission Checklist
**Role of AI today:** Critical reviewer and proofreader
**Estimated time:** ~60 minutes

---

## Copy-Paste Prompt

---

You are helping me finalize an 8-week academic cybersecurity case study. I am a beginner/intermediate student with approximately 1 hour available today. This is the FINAL session of the entire project.

---

**PROJECT TITLE:**
"Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems"

**PROJECT SUMMARY:**
Completed academic experiment:
- Dataset: NSL-KDD binary classification (normal=0, attack=1)
- Model: Random Forest (100 trees, random_state=42)
- Attack: Gaussian noise (std=DEFENSE_NOISE_STD) on top 5 features of attack-class test samples
- Defense: Adversarial training (augmented retraining)
- Three conditions: C1 Baseline / C2 Under Attack / C3 Post-Defense
- Report: ~4,000–5,500 words, 13 sections, 7 figures, 1 table, 8–12 references

---

**CURRENT STAGE:**
Week 8, Day 3. The very last session.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–8 Days 1–2 fully complete
- `week-8/final-report.md` contains the complete assembled report
- Figure/table index created
- Word count verified
- Consistency check partially complete
- Some [AI DRAFT — VERIFY] and [NEEDS CITATION] tags may remain

---

**TODAY'S OBJECTIVE:**
Final proofread, verification of all claims against experiment data, resolution of all remaining flags, and completion of the submission checklist. By the end of this session, the report is finished.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Critical reviewer and proofreader. Help me catch errors, verify consistency, and confirm academic quality. Be strict — this is the final pass.

---

**TODAY'S TASKS:**

**Task 1 — Academic integrity verification (15 minutes):**

I will paste the report (or key sections). Check for:

1. **Fabricated data:** Are there any statistics or results in the report that are NOT from my actual experiments? Flag every instance with [FABRICATED — REMOVE].

2. **Unverified citations:** Are there any in-text citations that do not have a corresponding entry in the reference list? Flag with [MISSING REFERENCE].

3. **AI-generated claims presented as facts:** Are there any unsourced claims about cybersecurity, ML, or performance that need either a citation or a qualifying phrase ("this study suggests...")?

4. **Scope violations:** Does any section claim something outside the defined scope (real-world deployment, production system, neural networks, attacking real systems)?

5. **Metric inconsistency:** Do the metric values in the Abstract, Results, and Conclusion all match exactly?

**Task 2 — Language and clarity check (15 minutes):**

Read through the following sections and check for:
- Unclear or ambiguous sentences (flag with [UNCLEAR])
- Overly complex jargon without explanation (flag with [SIMPLIFY])
- Repetition between sections (flag with [DUPLICATE])
- Missing subject or unclear pronoun reference (flag with [UNCLEAR])

Sections to check: Introduction, Discussion, Conclusion.

**Task 3 — Final [VERIFY] tag resolution (10 minutes):**

List all remaining [AI DRAFT — VERIFY] and [NEEDS CITATION] tags in the document. For each one:
- Tell me what specifically needs to be verified
- Tell me where to look (which experiment file, which paper)
- Give me a simple action: "Open `week-4/results-baseline.md` and confirm this number matches"

I will resolve each one during this session.

**Task 4 — Research objectives coverage check (5 minutes):**

Check that each research objective is explicitly addressed somewhere in the report:

- **Objective 1** (evaluate baseline performance): Is it answered in Section 9.1?
- **Objective 2** (quantify performance degradation under attack): Is it answered in Section 9.2?
- **Objective 3** (evaluate adversarial training recovery): Is it answered in Section 9.3 and Discussion?

If any objective is not adequately addressed, tell me exactly which sentence(s) to add.

**Task 5 — Run the final submission checklist (10 minutes):**

Work through this checklist with me item by item. For each item, I confirm it is done, and you note it as PASS or FLAG:

**Report completeness:**
- [ ] Abstract (~200 words, includes actual metrics)
- [ ] Introduction (~400 words, states research question and objectives)
- [ ] Problem Statement
- [ ] Research Objectives (3 numbered items starting with "To...")
- [ ] Background / Literature Review (400–600 words, 8–10 references)
- [ ] Research Gap (clearly stated)
- [ ] Proposed Framework (with diagram reference)
- [ ] Methodology (5 sub-sections)
- [ ] Experimental Setup
- [ ] Results (3 sub-sections, actual numbers)
- [ ] Discussion (5 paragraphs)
- [ ] Limitations (6 specific limitations)
- [ ] Future Work
- [ ] Conclusion
- [ ] References (8–12 verified, consistent format)

**Data integrity:**
- [ ] All metric values verified against notebook
- [ ] No fabricated results
- [ ] All citations verified on Google Scholar

**Figures:**
- [ ] All 7 figures saved as PNG
- [ ] All figures referenced in text
- [ ] All figures captioned

**Task 6 — Final words (5 minutes):**

After the checklist, give me:
1. A 3-sentence summary of what the final case study demonstrates
2. One honest statement of what the study cannot claim
3. A congratulatory note — the project is complete

---

**IMPORTANT CONSTRAINTS:**
- Do not suggest new experiments, new sections, or scope expansions at this late stage
- Any flagged items that cannot be fixed in 60 minutes should be noted as "acceptable known limitation" rather than causing a restart
- If a [VERIFY] item cannot be verified in this session, add a note in the Limitations section rather than guessing

**EXPECTED OUTPUT BY END OF SESSION:**
- All remaining [VERIFY] and [NEEDS CITATION] tags resolved
- Submission checklist completed (all items PASS or documented)
- `week-8/final-report.md` is the finished document
- Project is complete

**AT THE END OF THIS SESSION, PROVIDE:**
1. Submission checklist results (PASS / FLAG for each item)
2. List of any remaining known issues (acceptable limitations)
3. Final 3-sentence project summary
4. Confirmation: "The project is complete."

---

## Definition of Done

- [ ] All [AI DRAFT — VERIFY] tags resolved or documented
- [ ] All [NEEDS CITATION] items handled
- [ ] No fabricated data in report
- [ ] All 3 research objectives addressed
- [ ] Submission checklist completed
- [ ] `week-8/final-report.md` is the finished, submission-ready document

### Final artifacts — the complete project should contain

**Research documents:**
- `week-1/glossary.md`
- `week-1/papers-list.md`
- `week-1/research-question.md`
- `week-2/literature-notes.md`
- `week-2/lit-review-draft.md`
- `week-3/framework-design.md`
- `week-3/methodology-draft.md`

**Experiment files:**
- `week-4/notebook-baseline.ipynb`
- `week-4/results-baseline.md`
- `week-5/notebook-attack.ipynb`
- `week-5/attack-results.md`
- `week-6/notebook-defense.ipynb`
- `week-6/comparison-table.md`

**Figures (all PNG):**
- confusion-matrix-baseline.png
- roc-baseline.png
- feature-importance-baseline.png
- attack-curve.png
- confusion-matrix-attack.png
- comparison-barchart.png
- confusion-matrix-defense.png

**Final report:**
- `week-8/final-report.md` ← THE FINISHED CASE STUDY

### Estimated time
~60 minutes

---

*This is the final session. The project is complete after today.*

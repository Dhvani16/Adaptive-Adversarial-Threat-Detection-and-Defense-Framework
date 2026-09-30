# Week 7 — Day 2
**Topic:** Writing the Discussion and Limitations Sections
**Role of AI today:** Academic writing assistant and critical reviewer
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
- Dataset: NSL-KDD binary classification
- Model: Random Forest, adversarially trained
- Attack: Gaussian feature perturbation (std=DEFENSE_NOISE_STD)
- Defense: Adversarial training
- Three conditions: C1 Baseline / C2 Under Attack / C3 Post-Defense
- All metrics recorded and saved

---

**CURRENT STAGE:**
Week 7, Day 2.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Weeks 1–6 fully complete: all research, experiments, data
- Week 7 Day 1 complete:
  - Complete Results section drafted (~500 words)
  - All three sub-sections written with actual numbers
  - Figures referenced by number
  - Saved in `week-7/report-draft.md`

---

**TODAY'S OBJECTIVE:**
Write the Discussion section and the Limitations section. The Discussion interprets the results and connects them to the literature. The Limitations section honestly acknowledges what the experiment cannot claim.

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Academic writing assistant and critical reviewer. Help me write a Discussion that is intellectually honest — neither overclaiming nor underselling the findings.

---

**TODAY'S TASKS:**

**Task 1 — Explain what a Discussion section must do (5 minutes):**

Briefly explain:
- What is the difference between Results (what happened) and Discussion (what it means)?
- What 4 things a good Discussion typically does: interpret, connect to literature, acknowledge limitations, suggest future directions
- What "overclaiming" looks like and how to avoid it in my Discussion

**Task 2 — Draft the Discussion section (~600 words) (35 minutes):**

Using MY actual results (which I will paste), write a 600-word [AI DRAFT — VERIFY] Discussion section structured as follows:

**Paragraph 1 — Baseline performance interpretation (~100 words)**
- What the C1 metrics tell us about the Random Forest on NSL-KDD
- Connect to literature: does my baseline align with what prior studies reported on NSL-KDD? (Use my literature review from `week-2/lit-review-draft.md` — I will paste relevant excerpts)
- Do NOT claim "state-of-the-art" unless my results genuinely match what papers report

**Paragraph 2 — Why did the attack degrade performance? (~120 words)**
- Explain why Gaussian noise on important features causes detection failure
- Connect to the feature importance concept — the model relies heavily on a few features, so perturbing those features disrupts its decision boundaries
- Reference the attack curve: degradation increases with noise magnitude
- Connect to adversarial ML literature if I have relevant citations

**Paragraph 3 — Why did adversarial training help? (~120 words)**
- Explain the mechanism: by training on perturbed examples, the model learns a broader decision boundary around attack traffic
- Note that partial recovery is expected and acceptable — full recovery would require a perfect match between training perturbation and test perturbation
- Connect to papers on adversarial training from the literature review

**Paragraph 4 — What does this mean for adaptive IDS? (~120 words)**
- Connect the findings back to the research question
- What does this experiment demonstrate about the value of adaptive defenses?
- Be modest: this is a small, simulated study — do not overclaim applicability to real systems

**Paragraph 5 — Implications and broader significance (~120 words)**
- Who would care about these findings?
- What practical guidance (if any) can be drawn?
- What questions remain unanswered?

Mark all paragraphs [AI DRAFT — VERIFY].

**Task 3 — Draft the Limitations section (~200 words) (15 minutes):**

Write a 200-word [AI DRAFT — VERIFY] Limitations section that honestly addresses:

1. **Simulated attack:** Gaussian noise is a proxy for adversarial evasion, not a real adversary — real attackers would craft inputs using knowledge of the model
2. **Older dataset:** NSL-KDD is based on 1999 traffic data — modern network traffic looks very different
3. **Single model:** Only Random Forest was tested — results may differ for other classifiers (SVM, neural networks)
4. **Small scale:** Experiment is limited to one dataset, one model type, one defense method
5. **Defense specificity:** Adversarial training only helps against the type of perturbation seen during training — it would not generalize to unseen attack types
6. **No real-world validation:** All results are from a controlled, offline simulation

Keep the tone factual — limitations are not failures, they are honest acknowledgments of scope.

**Task 4 — Append to report draft (5 minutes):**
Append the Discussion and Limitations sections to `week-7/report-draft.md`.

---

**IMPORTANT CONSTRAINTS:**
- Every interpretation must be grounded in my actual results — do not add claims not supported by my data
- Do NOT say "our model outperforms all prior work" — I have not done a fair comparison
- Limitations must be honest and specific — generic statements like "more research is needed" are not sufficient
- Mark all AI-drafted text [AI DRAFT — VERIFY]

**EXPECTED OUTPUT BY END OF SESSION:**
- Discussion section (~600 words) with 5 paragraphs
- Limitations section (~200 words) with 6 specific limitations
- Both sections appended to `week-7/report-draft.md`

**HOW TO WORK WITH ME:**
- Ask me to paste relevant results and literature notes before drafting
- Flag any interpretive claims that go beyond what my data supports
- Push back if I try to overclaim

**AT THE END OF THIS SESSION, PROVIDE:**
1. Both sections formatted and ready to append to the report draft
2. A list of any claims that need citation verification (marked [NEEDS CITATION])
3. Reminder: "Next session (Day 3) we write Introduction, Background, and Methodology sections."

---

## Definition of Done

- [ ] Discussion section drafted (~600 words, 5 paragraphs)
- [ ] All interpretations grounded in actual results
- [ ] Limitations section drafted (~200 words, 6 specific points)
- [ ] Both sections appended to `week-7/report-draft.md`
- [ ] No overclaiming — scope is honest

### Expected artifacts
- `week-7/report-draft.md` — append Discussion + Limitations today

### Estimated time
~60 minutes

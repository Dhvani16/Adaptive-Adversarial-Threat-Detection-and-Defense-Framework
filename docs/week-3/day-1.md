# Week 3 — Day 1
**Topic:** Framework Design and Architecture
**Role of AI today:** System architect and designer
**Estimated time:** ~60 minutes

---

## Copy-Paste Prompt

---

You are helping me with an 8-week academic cybersecurity case study. I am a beginner/intermediate student with approximately 1 hour available today.

---

**PROJECT TITLE:**
"Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems"

**PROJECT SUMMARY:**
Controlled academic experiment using:
- Dataset: NSL-KDD (public network intrusion detection dataset, ~125k training records, 41 features)
- Model: Random Forest classifier (scikit-learn, 100 trees, random_state=42)
- Attack: Gaussian noise (std=0.1, 0.3, 0.5) added to top 5 features of attack-class test samples
- Defense: Adversarial training — retrain on original training data + perturbed attack training samples
- Three conditions: C1 (baseline), C2 (under attack), C3 (post-defense)
- Metrics: Accuracy, Precision, Recall, F1-score, AUC-ROC
- Output: Academic case study report (~4,000–5,000 words)

All work is simulated, ethical, uses only public data.

---

**CURRENT STAGE:**
Week 3, Day 1. Weeks 1 and 2 are complete.

**WHAT HAS ALREADY BEEN COMPLETED:**
- Week 1: glossary, verified paper list, research question, 3 objectives, hypothesis, scope
- Week 2: 7–10 paper summaries, literature review draft (400–500 words), research gap statement, reference list
- I understand the project at a conceptual level. Now I need to design it formally before coding.

---

**TODAY'S OBJECTIVE:**
Design the complete framework architecture on paper (before any coding). This means defining every component of the system, how they connect, and what each component's role is. Today I will also create the framework diagram description (for drawing in draw.io or PowerPoint).

**TODAY'S AVAILABLE TIME:**
Approximately 60 minutes.

**YOUR ROLE TODAY:**
Act as my system architect. Help me define and document the proposed framework clearly enough that someone reading my report can understand it without seeing my code.

---

**TODAY'S TASKS:**

**Task 1 — Describe the complete framework in plain language (15 minutes):**

Walk me through each component of the proposed framework from start to finish:

1. **Data Input Layer:** What goes in? (NSL-KDD dataset files)
2. **Preprocessing Module:** What transformations happen? (encoding, normalization, label creation, split)
3. **Baseline Detection Model:** What model? How trained? What does it output?
4. **Adversarial Attack Module:** How does feature perturbation work? What is changed, by how much?
5. **Evaluation Layer:** What metrics are computed? Across which test sets?
6. **Defense Module:** How does adversarial training augment the data? How is the model retrained?
7. **Comparison Output:** What final comparison does the framework produce?

For each component: give it a name, describe its input, its function, and its output.

**Task 2 — Create a text-based architecture diagram (15 minutes):**

Using ASCII or plain text, draw the architecture diagram showing the full pipeline with:
- All 7 components named and connected with arrows
- Labels showing data flow (what passes from one component to the next)
- The three evaluation branches (C1, C2, C3) clearly marked

This diagram will appear in my report. Make it clean enough to copy into a Word document.

**Task 3 — Define the three-condition experimental structure (10 minutes):**

Write a formal table defining the three experimental conditions:

| Condition | Name | Training data | Test data | Purpose |
|---|---|---|---|---|
| C1 | Baseline | ... | ... | ... |
| C2 | Under Attack | ... | ... | ... |
| C3 | Post-Defense | ... | ... | ... |

Fill this in completely based on my project setup.

**Task 4 — Write the "Proposed Framework" section draft (20 minutes):**

Write a 400-word [AI DRAFT — VERIFY] description of the proposed framework suitable for the report. This section should:
- Introduce the framework name and its purpose
- Describe each component (briefly)
- Reference the architecture diagram ("as shown in Figure 1")
- Connect the framework to the research objectives

Mark it [AI DRAFT — VERIFY] so I know to review it carefully.

---

**IMPORTANT CONSTRAINTS:**
- The framework must match exactly what I will implement (Random Forest, Gaussian noise, adversarial training)
- Do not add components I have not planned (no neural networks, no real-time components, no APIs)
- Keep the framework description honest — it is a small controlled experiment, not a production system
- Do not fabricate any technical claims

**EXPECTED OUTPUT BY END OF SESSION:**
- Plain-language description of all 7 framework components
- ASCII architecture diagram
- Three-condition experimental structure table
- 400-word [AI DRAFT] framework section for the report

**HOW TO WORK WITH ME:**
- Walk through each component before moving to the diagram
- Ask me to confirm each design decision before moving on
- Keep descriptions precise — not vague marketing language

**AT THE END OF THIS SESSION, PROVIDE:**
1. Everything above formatted and ready to copy into `week-3/framework-design.md`
2. Reminder: "Next session (Day 2) we set up Google Colab and download the NSL-KDD dataset."

---

## Definition of Done

- [ ] All 7 framework components named, described, with input/output defined
- [ ] ASCII architecture diagram created (clean, shows C1/C2/C3 branches)
- [ ] Three-condition table completed
- [ ] 400-word [AI DRAFT] framework section written
- [ ] `week-3/framework-design.md` saved

### Expected artifacts
- `week-3/framework-design.md` — framework description + diagram + table + draft section

### Estimated time
~60 minutes

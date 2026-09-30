# Adaptive Adversarial Threat Detection and Defense Framework
## Master Project Plan

**Project Title:** Adaptive Adversarial Threat Detection and Defense Framework for Robust AI-Based Cybersecurity Systems
**Duration:** 8 weeks | **Available Time:** 3 hours/week | **Total Time:** ~24 hours
**Skill Level:** Beginner/Intermediate | **AI Usage:** Extensive

---

## Part 1 — Project Overview

### What this project is

This is an 8-week academic case study exploring how machine learning-based cybersecurity systems can be made more resilient against adversarial attacks. You will:

1. Train a machine learning model to classify network traffic as normal or malicious using the public NSL-KDD dataset
2. Simulate an adversarial evasion attack that tricks the trained model into misclassifying attacks as normal traffic
3. Apply a defense mechanism (adversarial training) to improve the model's robustness
4. Measure and compare performance across three conditions: baseline, under attack, and after defense
5. Document the entire process in a structured academic case study report

### Why this problem matters

AI-based intrusion detection systems (IDS) are widely deployed to detect network attacks automatically. However, these ML models are vulnerable to adversarial manipulation — attackers can craft inputs that look benign to the AI but are actually malicious. This is called an evasion attack. Your case study addresses the question: can a simple adaptive defense mechanism (adversarial training) measurably improve a model's robustness against such attacks?

### Proposed solution

A small, controlled experimental study using:
- **Dataset:** NSL-KDD (public network intrusion detection dataset)
- **Model:** Random Forest classifier (scikit-learn)
- **Attack simulation:** Feature-space perturbation (Gaussian noise on key features of attack-class samples)
- **Defense:** Adversarial training (retraining on a mix of clean + adversarial samples)
- **Evaluation:** Comparing accuracy, recall, F1-score across three conditions

### Expected final outcome

A complete academic case study document (~4,000–5,000 words) containing:
- A literature review of 8–10 verified papers
- A clearly defined research question and methodology
- A framework architecture diagram
- Working Python code (Google Colab notebooks)
- Real experimental results from your own experiment
- Analysis, discussion, limitations, and honest conclusions

**This is NOT a production cybersecurity tool.** It is a controlled, ethical, simulated experiment for academic purposes only.

---

## Part 2 — Project Scope

### In scope — what you WILL do

- Targeted literature review on ML-based IDS and adversarial robustness (8–10 papers)
- Use the publicly available NSL-KDD dataset for all experiments
- Train a Random Forest classifier as the baseline intrusion detection model
- Simulate an evasion attack using feature-space perturbation (Gaussian noise on top features)
- Implement adversarial training as the defense mechanism
- Compare performance across exactly three conditions: baseline / under attack / post-defense
- Generate 4–5 graphs and at least 1 comparison table from real experiments
- Write a structured academic case study report (~4,000–5,000 words)
- Use AI extensively as research, coding, and writing assistant

### Out of scope — what you will NOT do

- Build a production or deployed cybersecurity system
- Test on real network traffic or real systems
- Implement gradient-based attacks (FGSM, PGD) — require neural networks and far more time
- Use deep learning or neural networks (too complex for 24 hours)
- Build a real-time adaptive system
- Conduct penetration testing or attack any real target
- Write a full research paper for submission to a conference or journal
- Survey more than 10–12 papers
- Build a front-end, dashboard, or user interface
- Introduce cloud infrastructure, databases, or APIs

---

## Part 3 — Research Question

### Main research question

*To what extent does adversarial training improve the robustness of a Random Forest-based intrusion detection system against feature-space evasion attacks, as evaluated on the NSL-KDD dataset?*

### Supporting research questions

1. What is the baseline performance of a Random Forest classifier on the NSL-KDD binary classification task under clean conditions?
2. How significantly does detection performance degrade when attack-class test samples are subjected to Gaussian feature perturbation?
3. Does augmenting the training set with adversarial examples (adversarial training) measurably recover detection performance?
4. What are the limitations of feature-space perturbation as a proxy for real-world adversarial evasion attacks?

### Research objectives

1. To evaluate the baseline intrusion detection performance of a Random Forest classifier on NSL-KDD under clean conditions
2. To quantify performance degradation when the model is subjected to simulated feature-space evasion attacks
3. To evaluate whether adversarial training recovers model performance after simulated attacks
4. To critically analyze the limitations of this experimental design and discuss implications for real-world adaptive defense

### Hypothesis

A Random Forest classifier trained on clean NSL-KDD data will show measurable performance degradation (reduction in recall and F1-score) when tested on adversarially perturbed attack samples. Retraining on a dataset augmented with adversarial examples will partially or fully recover this performance. The degree of recovery will depend on the noise magnitude used in the attack.

---

## Part 4 — Proposed Technical Approach

### Why these components were chosen

| Component | Chosen approach | Why chosen | Rejected alternative |
|---|---|---|---|
| Dataset | NSL-KDD | Small, clean, widely cited in IDS research, free, beginner-friendly | CICIDS2017 — larger and harder to preprocess in 24 hrs |
| Model | Random Forest | No deep tuning needed, trains in seconds, well-documented | Neural network — requires more setup, makes gradient-based attack necessary |
| Attack | Gaussian feature perturbation | No gradient computation, simple to implement, conceptually valid proxy | FGSM/PGD — require differentiable model, much more complex |
| Defense | Adversarial training | Simplest recognized defense, easy to implement, well-supported in literature | Certified defenses, ensemble methods — too complex for 24 hours |
| Metrics | Accuracy, Recall, F1, AUC | Standard IDS evaluation metrics, widely understood | Custom metrics — unnecessary complexity |

### What each component does

- **NSL-KDD Dataset** — Provides labeled network connection records (normal vs. attack). Source of training and test data.
- **Preprocessing** — Converts raw data into numeric format. Encodes categorical features, normalizes numeric features, creates binary labels.
- **Random Forest (Baseline)** — Learns to distinguish normal from attack traffic. Establishes your reference performance benchmark.
- **Feature Perturbation (Attack)** — Adds Gaussian noise to the features the model relies on most, simulating an attacker trying to make attack traffic look like normal traffic.
- **Adversarial Training (Defense)** — Augments the training data with adversarial examples (with correct labels) and retrains. Forces the model to recognize that perturbed attack traffic is still attack traffic.
- **Evaluation Pipeline** — Measures metrics across all three conditions and generates comparison visualizations.

---

## Part 5 — System Architecture

```
[NSL-KDD Dataset]
        ↓
[Data Preprocessing]
  - Encode categorical features (protocol_type, service, flag) via LabelEncoder
  - Normalize numerical features via StandardScaler
  - Create binary labels: normal=0, all attacks=1
  - Train/test split: 80% / 20%
        ↓
[Baseline Random Forest Classifier]
  - 100 trees, random_state=42
  - Trained on clean training set
        ↓
┌─────────────────────────────────┐
│  CONDITION 1: BASELINE          │
│  Test on clean test data        │
│  → Accuracy, Precision,         │
│    Recall, F1, AUC-ROC          │
└─────────────────────────────────┘
        ↓
[Adversarial Attack Simulation]
  - Identify top 5 features via feature_importances_
  - Add Gaussian noise (std = 0.1, 0.3, 0.5) to attack samples in test set
  - Three adversarial test sets created
        ↓
┌─────────────────────────────────┐
│  CONDITION 2: UNDER ATTACK      │
│  Test on adversarial data       │
│  (chosen noise level: std=0.3)  │
│  → Drop in recall and F1        │
└─────────────────────────────────┘
        ↓
[Adversarial Training Defense]
  - Apply perturbation (std=0.3) to attack samples in training set
  - Augment: original training + adversarial training samples
  - Retrain Random Forest on augmented dataset
        ↓
┌─────────────────────────────────┐
│  CONDITION 3: POST-DEFENSE      │
│  Test on same adversarial data  │
│  → Recovery in recall and F1    │
└─────────────────────────────────┘
        ↓
[Results and Evaluation]
  - Three-condition comparison table (C1 / C2 / C3)
  - Bar chart comparison, attack curve, confusion matrices
  - Academic case study report
```

---

## Part 6 — Technology Stack

| Tool | Purpose |
|---|---|
| Python 3.x | Primary programming language |
| Google Colab | Free cloud Jupyter notebook environment |
| pandas | Data loading and manipulation |
| scikit-learn | Random Forest, preprocessing, metrics |
| numpy | Numerical operations and noise generation |
| matplotlib | Graphs and visualizations |
| seaborn | Enhanced statistical plots (optional) |
| NSL-KDD dataset | Experimental data (public, free) |
| Claude / ChatGPT | AI research, coding, and writing assistant |

**You do NOT need:** TensorFlow, PyTorch, Docker, databases, cloud APIs, any paid tools.

---

## Part 7 — Dataset

### Primary dataset: NSL-KDD

**What it is:** NSL-KDD is a cleaned version of the KDD Cup 1999 dataset. It is one of the most widely used benchmarks in intrusion detection research. It contains labeled network connection records with 41 features.

**Why it is appropriate:**
- Widely cited in academic ML-based IDS literature
- Manageable size: training set ~125,973 records, test set ~22,544 records
- Clean and well-structured; no missing values after standard preprocessing
- Free and publicly available
- Includes attack types: DoS, Probe, R2L, U2R — binary classification is straightforward
- Feature-level attack simulation works naturally with this format

**Key features include:**
- `protocol_type` (categorical: tcp, udp, icmp)
- `service` (categorical: http, ftp, smtp, etc.)
- `flag` (categorical: connection status flags)
- 38 numerical features (duration, byte counts, error rates, etc.)
- `label` (target: "normal" or specific attack type name)

**Binary label mapping:**
- "normal" → 0
- All attack type labels → 1

**Files needed:** KDDTrain+.txt (training) and KDDTest+.txt (test). Both are under 20MB. Download from the official UNB-CIC source — verify the URL yourself before downloading.

**IMPORTANT:** Do not rely on AI-generated descriptions of the dataset as ground truth. Open the actual files and verify the column names and format yourself.

### Alternative considered and rejected
CICIDS2017 — More recent and realistic but significantly larger and harder to preprocess. Would consume too much of the 24-hour budget on data wrangling alone.

---

## Part 8 — Research Methodology

### Step-by-step methodology

**Step 1 — Literature Review (Weeks 1–2)**
Review 8–10 real, verifiable papers on: ML-based intrusion detection using NSL-KDD, adversarial attacks on ML cybersecurity models, and adversarial training as a defense. Identify the research gap your study addresses.

**Step 2 — Problem Definition (Week 1)**
Finalize the research question, supporting questions, objectives, and hypothesis. Define scope strictly. Write a 1-page problem definition document.

**Step 3 — Framework Design (Week 3)**
Design the conceptual framework and architecture diagram. Define the three-condition experimental structure. Plan preprocessing and evaluation pipelines before touching code.

**Step 4 — Dataset Preparation (Weeks 3–4)**
Download NSL-KDD. Explore features and structure. Preprocess: encode categorical features, normalize numeric features, create binary labels, split 80/20.

**Step 5 — Baseline Model (Week 4)**
Train Random Forest on clean training data. Evaluate on clean test data. Record Accuracy, Precision, Recall, F1, AUC-ROC. Generate confusion matrix and ROC curve.

**Step 6 — Adversarial Attack Simulation (Week 5)**
Identify top 5 features by `feature_importances_`. Apply Gaussian noise at three levels (std=0.1, 0.3, 0.5) to attack-class test samples. Evaluate model on each adversarial set. Record performance degradation. Select noise level for defense phase.

**Step 7 — Adaptive Defense (Week 6)**
Apply Gaussian noise (std=0.3) to attack-class training samples. Create augmented training set. Retrain Random Forest. Evaluate on the same adversarial test set used in Step 6. Record recovery metrics.

**Step 8 — Evaluation and Comparison (Weeks 6–7)**
Compile three-condition comparison table. Generate: comparison bar chart, attack curve, confusion matrices. All numbers must come from actual experiments — no invented results.

**Step 9 — Analysis and Writing (Weeks 7–8)**
Interpret results. Write all report sections. Cite only verified sources. Acknowledge limitations honestly.

**Step 10 — Final Review (Week 8)**
Compile complete report, proofread, format, verify all claims against experiment data, finalize reference list.

---

## Part 9 — 8-Week Roadmap

---

### Week 1 — Foundation and Problem Definition

**Objective:** Understand the topic deeply and establish a precise, scoped research problem.

**Why this week matters:** You cannot design a good experiment without understanding what you are studying. Week 1 ensures you start with a clear, narrow, achievable problem.

| Day | Task | Time |
|---|---|---|
| Day 1 | Understand core concepts: IDS, adversarial ML, evasion attacks, robustness | 60 min |
| Day 2 | Literature search — identify 8–10 real papers on the three key themes | 60 min |
| Day 3 | Finalize research question, objectives, scope statement | 60 min |

**AI assistance:** Teacher (Day 1), Research assistant (Day 2), Supervisor (Day 3)

**Personal work required:** Write scope in your own words, verify all papers on Google Scholar, finalize research question yourself

**Expected deliverables:**
- Personal glossary (6 terms)
- Candidate paper list (8–10 titles, verified on Google Scholar)
- 1-page document: research question + 3 objectives + scope

#### Week 1 — Definition of Done
- [ ] Can explain the research question without notes
- [ ] Have 8–10 candidate papers with verified titles on Google Scholar
- [ ] Have written: research question, 3 objectives, scope (in/out)
- [ ] Personal glossary created with 6 terms

**Artifacts:** `week-1/glossary.md`, `week-1/papers-list.md`, `week-1/research-question.md`
**Total expected time:** ~3 hours

---

### Week 2 — Literature Review

**Objective:** Build a structured understanding of existing research and identify the research gap.

**Why this week matters:** A literature review justifies why your study is needed. Without it, you cannot explain what problem you are solving or how your work relates to existing knowledge.

| Day | Task | Time |
|---|---|---|
| Day 1 | Deep dive into ML-based IDS papers; understand NSL-KDD usage | 60 min |
| Day 2 | Deep dive into adversarial attacks on cybersecurity ML models | 60 min |
| Day 3 | Identify research gap; write 400-word literature review draft | 60 min |

**AI assistance:** Research assistant + teacher (Days 1–2), Writing assistant (Day 3)

**Personal work required:** Read summaries critically, verify all citations, write gap statement yourself

**Expected deliverables:**
- Annotated summaries of 8–10 verified papers
- Research gap statement (2–3 sentences)
- 400–500 word literature review draft

#### Week 2 — Definition of Done
- [ ] Annotated summaries for 8–10 papers (all verified as real)
- [ ] Research gap clearly articulated
- [ ] 400-word literature review draft written

**Artifacts:** `week-2/literature-notes.md`, `week-2/lit-review-draft.md`
**Total expected time:** ~3 hours

---

### Week 3 — Framework Design and Environment Setup

**Objective:** Design the conceptual framework and prepare the technical environment before coding begins.

**Why this week matters:** Designing on paper before coding prevents wasted effort. Environment setup ensures there are no tool surprises in Week 4.

| Day | Task | Time |
|---|---|---|
| Day 1 | Design framework; draw architecture diagram; document each component | 60 min |
| Day 2 | Set up Google Colab; download NSL-KDD; explore dataset structure | 60 min |
| Day 3 | Plan preprocessing steps; write methodology draft | 60 min |

**AI assistance:** Architect (Day 1), Teacher/Programmer (Day 2), Writer (Day 3)

**Personal work required:** Draw the diagram yourself, physically open the dataset file and look at it, verify column count

**Contingency:** If dataset download fails, search for NSL-KDD on Kaggle as a backup mirror.

**Expected deliverables:**
- Framework architecture diagram
- Working Colab notebook with imports verified
- NSL-KDD dataset downloaded and readable
- 300-word methodology draft

#### Week 3 — Definition of Done
- [ ] Framework diagram exists (at minimum as a sketch)
- [ ] Colab notebook opens; pandas and scikit-learn import without errors
- [ ] NSL-KDD files downloaded; `df.shape` shows correct dimensions
- [ ] Methodology draft written (~300 words)

**Artifacts:** `week-3/framework-diagram.png`, `week-3/notebook.ipynb`, `week-3/methodology-draft.md`
**Total expected time:** ~3 hours

---

### Week 4 — Baseline Model Implementation

**Objective:** Build and evaluate the baseline intrusion detection model using clean data.

**Why this week matters:** The baseline is your reference point. Without solid baseline results, you have nothing to compare the attack and defense against.

| Day | Task | Time |
|---|---|---|
| Day 1 | Data preprocessing code: load, encode, normalize, split | 60 min |
| Day 2 | Train Random Forest; evaluate; record all baseline metrics | 60 min |
| Day 3 | Generate baseline visualizations; document results in writing | 60 min |

**AI assistance:** Programmer (Days 1–2), Programmer + Writer (Day 3)

**Personal work required:** Run every code cell yourself, record actual output numbers, understand each preprocessing step

**Contingency:** If accuracy < 70%, there is likely a preprocessing error. Ask AI to debug. Common issues: wrong label mapping, unstandardized features.

**Expected deliverables:**
- Working preprocessing pipeline
- Trained Random Forest model
- Baseline metrics: Accuracy, Precision, Recall, F1, AUC
- Confusion matrix PNG + ROC curve PNG
- 2-paragraph written results description

#### Week 4 — Definition of Done
- [ ] Preprocessing runs without errors
- [ ] Baseline metrics recorded in a table
- [ ] Confusion matrix and ROC curve saved as PNG files
- [ ] Results documented in `week-4/results-baseline.md`

**Artifacts:** `week-4/notebook-baseline.ipynb`, `week-4/results-baseline.md`, `week-4/confusion-matrix-baseline.png`, `week-4/roc-baseline.png`
**Total expected time:** ~3 hours

---

### Week 5 — Adversarial Attack Simulation

**Objective:** Demonstrate that the baseline model is vulnerable to simulated evasion attacks.

**Why this week matters:** This is the core of your research problem. You must show the vulnerability exists with measured evidence before you can defend against it.

| Day | Task | Time |
|---|---|---|
| Day 1 | Study evasion attack theory; understand feature importance; design the attack | 60 min |
| Day 2 | Implement feature perturbation at 3 noise levels; run experiments; record results | 60 min |
| Day 3 | Generate attack curve graph; document findings in writing | 60 min |

**AI assistance:** Teacher (Day 1), Programmer (Day 2), Programmer + Writer (Day 3)

**Personal work required:** Choose noise levels, run all experiments, interpret the drop in performance yourself

**Contingency:** If std=0.5 does not produce meaningful degradation, try std=1.0 or 2.0. If still no degradation, try perturbing all 10 top features instead of 5.

**Expected deliverables:**
- Feature perturbation code (3 noise levels)
- Results table: metrics at noise = 0.0, 0.1, 0.3, 0.5
- Attack curve graph (recall vs. noise magnitude)
- Selected noise level for defense phase
- 2-paragraph findings document

#### Week 5 — Definition of Done
- [ ] Attack code runs without errors at all 3 noise levels
- [ ] Performance drop measured and recorded
- [ ] Attack curve graph saved as PNG
- [ ] Noise level for defense phase chosen and documented

**Artifacts:** `week-5/notebook-attack.ipynb`, `week-5/attack-results.md`, `week-5/attack-curve.png`
**Total expected time:** ~3 hours

---

### Week 6 — Adaptive Defense Implementation

**Objective:** Apply adversarial training and measure whether it recovers detection performance.

**Why this week matters:** This is your proposed solution. Week 6 produces the evidence that answers your main research question.

| Day | Task | Time |
|---|---|---|
| Day 1 | Study adversarial training theory; design the augmented training strategy | 60 min |
| Day 2 | Implement adversarial training; retrain model; evaluate | 60 min |
| Day 3 | Compile three-condition comparison; generate comparison bar chart | 60 min |

**AI assistance:** Teacher (Day 1), Programmer (Day 2), Programmer + Analyst (Day 3)

**Personal work required:** Run retraining yourself, record genuine results, honestly describe what changed

**Contingency:** If adversarial training shows no improvement, try augmenting with a lower noise level (std=0.1). If still no improvement, report this honestly — a partial or null result is still academically valid and leads to a strong limitations section.

**Expected deliverables:**
- Adversarial training code
- Defended model metrics
- Three-condition comparison table (C1 / C2 / C3)
- Comparison bar chart PNG

#### Week 6 — Definition of Done
- [ ] Adversarial training implemented; model retrained
- [ ] Defended model evaluated on the same adversarial test set from Week 5
- [ ] Three-condition comparison table complete with real numbers
- [ ] Comparison bar chart saved as PNG

**Artifacts:** `week-6/notebook-defense.ipynb`, `week-6/comparison-table.md`, `week-6/comparison-barchart.png`
**Total expected time:** ~3 hours

---

### Week 7 — Results Analysis and Report Drafting

**Objective:** Interpret your experimental findings and draft the core sections of the report.

**Why this week matters:** Analysis transforms raw numbers into a defensible academic argument. Without clear interpretation, your data has no academic meaning.

| Day | Task | Time |
|---|---|---|
| Day 1 | Write results section with all real metrics, tables, figure references | 60 min |
| Day 2 | Write discussion and limitations sections | 60 min |
| Day 3 | Write introduction, background/literature review, methodology sections | 60 min |

**AI assistance:** Writing assistant throughout. You verify every factual claim.

**Personal work required:** Verify every number against notebooks, rewrite AI-drafted text in your own voice, write limitations honestly

**Important:** AI drafts — you verify and edit. No invented statistics. No fabricated citations.

**Expected deliverables:**
- Draft results section (all metrics + figure references)
- Draft discussion section
- Draft limitations section
- Draft introduction + background + methodology sections

#### Week 7 — Definition of Done
- [ ] Results section written with actual experimental numbers
- [ ] Discussion section written and honest
- [ ] Limitations section complete
- [ ] Introduction, background, methodology drafted

**Artifacts:** `week-7/report-draft.md`
**Total expected time:** ~3 hours

---

### Week 8 — Final Report, Polish, and Review

**Objective:** Complete, integrate, and finalize the academic case study document.

**Why this week matters:** The final document is what you actually submit or present. Week 8 converts your drafts into a complete, polished, academically defensible case study.

| Day | Task | Time |
|---|---|---|
| Day 1 | Write abstract, conclusion, compile and format references | 60 min |
| Day 2 | Integrate all sections; fix flow, formatting, figure numbering | 60 min |
| Day 3 | Final proofread; verify all numbers; complete submission checklist | 60 min |

**AI assistance:** Writing assistant (Days 1–2), Critical reviewer (Day 3)

**Personal work required:** Verify all numbers match notebooks, confirm all citations are real, check each objective is answered

**Expected deliverables:**
- Complete final report (4,000–5,000 words)
- Finalized references (8–12 verified citations)
- All figures labeled and captioned
- Completed submission checklist

#### Week 8 — Definition of Done
- [ ] Complete report in one document
- [ ] Every number verified against experiment notebooks
- [ ] All citations verified as real
- [ ] Each research objective answered in the report
- [ ] Abstract, introduction, conclusion complete
- [ ] Final checklist fully ticked

**Artifacts:** `week-8/final-report.md`
**Total expected time:** ~3 hours

---

## Part 10 — Final Deliverables

```
final-case-study/
├── report/
│   ├── final-report.md          ← Complete case study (~4,000–5,000 words)
│   └── references.md            ← 8–12 verified citations
├── code/
│   ├── notebook-baseline.ipynb  ← Preprocessing + Random Forest (Week 4)
│   ├── notebook-attack.ipynb    ← Adversarial attack simulation (Week 5)
│   └── notebook-defense.ipynb  ← Adversarial training defense (Week 6)
├── figures/
│   ├── framework-diagram.png    ← System architecture (Week 3)
│   ├── confusion-matrix-baseline.png  ← Baseline (Week 4)
│   ├── roc-baseline.png              ← Baseline ROC (Week 4)
│   ├── attack-curve.png              ← Recall vs noise (Week 5)
│   └── comparison-barchart.png       ← C1/C2/C3 comparison (Week 6)
└── results/
    ├── baseline-metrics.md      ← C1 results
    ├── attack-metrics.md        ← C2 results
    └── defense-metrics.md       ← C3 results
```

### What each deliverable should contain

| Deliverable | Contents | Finalized in |
|---|---|---|
| Final report | All 13 sections, ~4,000–5,000 words | Week 8 |
| References | 8–12 verified citations, consistent format | Week 8 |
| notebook-baseline.ipynb | Preprocessing + RF training + evaluation | Week 4 |
| notebook-attack.ipynb | Feature perturbation attack + results | Week 5 |
| notebook-defense.ipynb | Adversarial training + comparison | Week 6 |
| Framework diagram | Architecture drawing/diagram | Week 3 |
| Figures (5 total) | All labeled, titled, saved as PNG | Weeks 4–6 |
| Results tables | Real numbers only, no fabrication | Weeks 4–6 |

---

## Part 11 — Final Project Checklist

### Research
- [ ] Research question defined and scoped
- [ ] Supporting questions answered in the report
- [ ] Hypothesis stated and tested

### Literature
- [ ] 8–10 real papers identified
- [ ] All citations verified on Google Scholar
- [ ] Literature review written (400–600 words)
- [ ] Research gap clearly stated

### Dataset
- [ ] NSL-KDD downloaded from official source
- [ ] Dataset opened and explored in Python
- [ ] Feature structure understood
- [ ] Binary labels created (normal=0, attack=1)
- [ ] 80/20 train-test split applied

### Code
- [ ] Preprocessing pipeline working without errors
- [ ] Random Forest baseline trained and evaluated
- [ ] Feature perturbation attack implemented at 3 noise levels
- [ ] Adversarial training defense implemented
- [ ] All code reproducible (fixed random_state)

### Experiments
- [ ] Baseline evaluation complete (Condition 1)
- [ ] Adversarial attack evaluation complete (Condition 2) at 3 noise levels
- [ ] Defense evaluation complete (Condition 3)
- [ ] Noise level for defense chosen and documented

### Results
- [ ] All metrics recorded: accuracy, precision, recall, F1, AUC
- [ ] Three-condition comparison table complete
- [ ] All 5 graphs generated and saved
- [ ] No invented, fabricated, or AI-generated numbers in results

### Framework
- [ ] Architecture diagram created
- [ ] Framework described in the report

### Report sections
- [ ] Abstract (~200 words)
- [ ] Introduction (~400 words)
- [ ] Problem Statement (~200 words)
- [ ] Research Objectives (~150 words)
- [ ] Background / Literature Review (~600–800 words)
- [ ] Research Gap (~150 words)
- [ ] Proposed Framework (~500 words + diagram)
- [ ] Methodology (~500 words)
- [ ] Experimental Setup (~300 words)
- [ ] Results (~500 words + figures)
- [ ] Discussion (~600 words)
- [ ] Limitations (~200 words)
- [ ] Future Work (~200 words)
- [ ] Conclusion (~200 words)

### References
- [ ] All references formatted consistently (APA or IEEE)
- [ ] Every citation corresponds to a real, verified paper
- [ ] At least 8 references included

### Final validation
- [ ] Every factual claim supported by data or a citation
- [ ] Every number in the report matches the notebook output exactly
- [ ] Limitations are honest and specific
- [ ] No fabricated results, statistics, or citations anywhere
- [ ] Each of the 3 research objectives addressed in the report

---

## Part 12 — Project Risk Register

| Risk | Probability | Impact | Prevention | Fallback |
|---|---|---|---|---|
| Scope creep — project grows too large | High | High | Follow this plan strictly. Add nothing not listed in scope. | Return to Part 2 and cut anything not listed as in-scope |
| Adversarial attack shows no degradation | Medium | Medium | Use sufficient noise level; increase to std=1.0 if needed | Report as finding: "model showed robustness at this perturbation level" — still academically valid |
| Adversarial training shows no recovery | Medium | Medium | Reduce noise level for training augmentation (try std=0.1) | Report partial or null result honestly — leads to strong limitations section |
| Dataset loading / preprocessing errors | Low | Medium | Follow preprocessing steps exactly; ask AI to debug immediately | Use Kaggle-hosted NSL-KDD mirror as backup download source |
| AI generates fabricated citations | High | Critical | Verify EVERY paper on Google Scholar before citing. No exceptions. | Delete uncited claim; rephrase the point without citation |
| Coding takes too long | Medium | High | Use AI to generate code; limit debugging to 30 min per blocker | Simplify: fewer noise levels, smaller dataset subset if needed |
| Time runs out before writing | Medium | High | Do not exceed weekly time budget in Weeks 4–6 | Freeze coding at end of Week 6 regardless; write based on whatever results exist |
| Papers too difficult to understand | Medium | Low | Ask AI to explain in plain language; use abstract + conclusion only | Do not cite claims you do not understand even partially |
| Insufficient or unexpected results | Low | Medium | Follow exact experimental design; results do not need to be perfect | Honest null/partial result with strong discussion is academically acceptable |

---

*Plan version 1.0*
*Total budget: 8 weeks × 3 hours = 24 hours*
*Scope status: Locked — do not expand without removing something else*

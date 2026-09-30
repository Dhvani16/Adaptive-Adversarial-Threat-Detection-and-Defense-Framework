# Week 1 — Candidate Papers List
*8–10 candidate papers across 3 themes. Verify every entry on Google Scholar before citing.*

---

## VERIFICATION STATUS KEY
- ✅ HIGH CONFIDENCE — widely cited, author/title/year well established
- ⚠️ MEDIUM CONFIDENCE — paper likely exists but verify exact title/year/venue
- ❌ EXCLUDE — could not be confirmed; do not cite

---

## Theme A — ML-Based Network Intrusion Detection (NSL-KDD / IDS)

### Paper A1 ✅ HIGH CONFIDENCE
**Title:** A Detailed Analysis of the KDD CUP 99 Data Set  
**Authors:** Tavallaee, M., Bagheri, E., Lu, W., & Ghorbani, A. A.  
**Year:** 2009  
**Venue:** IEEE Symposium on Computational Intelligence for Security and Defense Applications (CISDA)  
**Description:** This is the foundational paper that introduced NSL-KDD as a cleaned replacement for the KDD Cup 1999 dataset. It documents the dataset's structure, addresses the known problems with the original KDD99 dataset (duplicate records, unbalanced attack distribution), and presents baseline performance of several classifiers.  
**Why relevant:** This is the primary citation for using NSL-KDD — you must cite this paper.

---

### Paper A2 ⚠️ MEDIUM CONFIDENCE
**Title:** A Detailed Analysis on NSL-KDD Dataset Using Various Machine Learning Techniques for Intrusion Detection  
**Authors:** Revathi, S., & Malathi, A.  
**Year:** 2013  
**Venue:** International Journal of Engineering Research & Technology (IJERT)  
**Description:** Compares multiple ML classifiers (Decision Tree, Naive Bayes, SVM, Random Forest) on NSL-KDD for binary and multi-class intrusion detection. Reports accuracy and F1 scores across classifiers.  
**Why relevant:** Provides baseline benchmarks for Random Forest on NSL-KDD — useful for comparing your results.  
**⚠️ Verify:** Search exact title on Google Scholar. Journal IJERT is indexed; confirm year and volume.

---

### Paper A3 ⚠️ MEDIUM CONFIDENCE
**Title:** Survey of Intrusion Detection Systems: Techniques, Datasets and Challenges  
**Authors:** Khraisat, A., Gondal, I., Vamplew, P., & Kamruzzaman, J.  
**Year:** 2019  
**Venue:** Cybersecurity (Springer)  
**Description:** A survey paper reviewing the landscape of network intrusion detection systems, covering signature-based, anomaly-based, and hybrid approaches. Discusses NSL-KDD and CICIDS2017 as benchmark datasets.  
**Why relevant:** Provides broad context for your literature review on IDS.  
**⚠️ Verify:** Search "Survey of intrusion detection systems Khraisat 2019" on Google Scholar.

---

### Paper A4 ⚠️ MEDIUM CONFIDENCE
**Title:** Evaluation of Machine Learning Algorithms for Intrusion Detection System  
**Authors:** Ingre, B., & Yadav, A.  
**Year:** 2015  
**Venue:** IEEE International Conference on Signal Processing and Communication Engineering Systems (SPACES)  
**Description:** Evaluates several ML algorithms including Random Forest and Naïve Bayes on the NSL-KDD dataset. Compares detection rate, false positive rate, and computational cost.  
**Why relevant:** Directly benchmarks Random Forest on NSL-KDD, supporting your model choice.  
**⚠️ Verify:** Search "Evaluation of Machine Learning Algorithms Intrusion Detection Ingre Yadav 2015" on Google Scholar. Confirm IEEE SPACES conference existence.

---

## Theme B — Adversarial Attacks on ML Models in Cybersecurity

### Paper B1 ✅ HIGH CONFIDENCE
**Title:** Explaining and Harnessing Adversarial Examples  
**Authors:** Goodfellow, I. J., Shlens, J., & Szegedy, C.  
**Year:** 2015  
**Venue:** International Conference on Learning Representations (ICLR 2015)  
**Description:** Introduces the Fast Gradient Sign Method (FGSM), the foundational gradient-based adversarial attack. Explains why linear models and deep networks are inherently vulnerable to small, imperceptible input perturbations.  
**Why relevant:** The theoretical foundation for adversarial attacks. Though FGSM is for neural networks (not Random Forest), this paper establishes the conceptual basis of adversarial vulnerability you are studying.

---

### Paper B2 ✅ HIGH CONFIDENCE
**Title:** Intriguing Properties of Neural Networks  
**Authors:** Szegedy, C., Zaremba, W., Sutskever, I., Bruna, J., Erhan, D., Goodfellow, I., & Fergus, R.  
**Year:** 2014  
**Venue:** International Conference on Learning Representations (ICLR 2014)  
**Description:** The paper that first identified adversarial examples in neural networks — showing that small, structured perturbations in input space can cause confident misclassifications. Introduced the concept that is central to all adversarial ML research.  
**Why relevant:** This is the origin paper of adversarial ML research — essential background context.

---

### Paper B3 ✅ HIGH CONFIDENCE
**Title:** Towards Evaluating the Robustness of Neural Networks  
**Authors:** Carlini, N., & Wagner, D.  
**Year:** 2017  
**Venue:** IEEE Symposium on Security and Privacy (S&P 2017)  
**Description:** Proposes the C&W attack, showing that many existing adversarial defenses (including adversarial training variants) can be broken with stronger attacks. Introduces rigorous evaluation methodology for adversarial robustness.  
**Why relevant:** Important context for the limitations of adversarial training as a defense — directly relevant to your Week 6 results discussion.

---

### Paper B4 ⚠️ MEDIUM CONFIDENCE
**Title:** Adversarial Attacks Against Intrusion Detection Systems: Taxonomy, Solutions and Open Issues  
**Authors:** Corona, I., Giacinto, G., & Roli, F.  
**Year:** 2013  
**Venue:** Information Sciences (Elsevier)  
**Description:** Provides a taxonomy of adversarial attacks specifically targeting intrusion detection systems. Distinguishes evasion vs. poisoning attacks in the IDS context and discusses defense strategies.  
**Why relevant:** Directly bridges adversarial ML and intrusion detection — highly relevant to your project framing.  
**⚠️ Verify:** Search "Adversarial attacks against intrusion detection systems Corona Giacinto Roli" on Google Scholar.

---

### Paper B5 ⚠️ MEDIUM CONFIDENCE
**Title:** The Limitations of Deep Learning in Adversarial Settings  
**Authors:** Papernot, N., McDaniel, P., Jha, S., Fredrikson, M., Celik, Z. B., & Swami, A.  
**Year:** 2016  
**Venue:** IEEE European Symposium on Security and Privacy (EuroS&P 2016)  
**Description:** Demonstrates that deep learning classifiers can be deceived by carefully crafted inputs with minimal perturbation. Introduces the Jacobian-based saliency map attack (JSMA) and discusses implications for security-critical systems.  
**Why relevant:** Supports the theoretical motivation for why ML-based IDS systems are vulnerable to adversarial manipulation.  
**⚠️ Verify:** Search "The limitations of deep learning in adversarial settings Papernot 2016 EuroS&P" on Google Scholar.

---

## Theme C — Adversarial Training as a Defense

### Paper C1 ✅ HIGH CONFIDENCE
**Title:** Towards Deep Learning Models Resistant to Adversarial Attacks  
**Authors:** Madry, A., Makelov, A., Schmidt, L., Tsipras, D., & Vladu, A.  
**Year:** 2018  
**Venue:** International Conference on Learning Representations (ICLR 2018)  
**Description:** Formulates adversarial training as a min-max optimization problem and proposes PGD (Projected Gradient Descent) adversarial training. Demonstrates that PGD-trained models are significantly more robust to adversarial examples than baseline models.  
**Why relevant:** The theoretical foundation for adversarial training as a defense — your Week 6 defense directly applies this concept.

---

### Paper C2 ✅ HIGH CONFIDENCE
**Title:** Ensemble Adversarial Training: Attacks and Defenses  
**Authors:** Tramèr, F., Kurakin, A., Papernot, N., Goodfellow, I., Boneh, D., & McDaniel, P.  
**Year:** 2018  
**Venue:** International Conference on Learning Representations (ICLR 2018)  
**Description:** Shows that augmenting training data with adversarial examples from multiple pre-trained models (ensemble) produces more robust classifiers than single-model adversarial training. Also discusses the transferability of adversarial examples.  
**Why relevant:** Supports the adversarial training approach. Note: your implementation uses single-model training (simpler) — cite this as the academic basis while acknowledging your approach is a simplified version.

---

## Verification Checklist

Use this for every paper before adding it to your reference list:

```
For each paper:
1. Go to scholar.google.com
2. Search: [first author surname] [first 4–5 words of title] [year]
   Example: "Tavallaee detailed analysis KDD CUP 99 2009"
3. Check:
   □ Title matches closely (exact or very close)
   □ Author names match (at least first author)
   □ Year matches (±1 year is acceptable for preprints)
   □ Venue/journal matches
   □ The paper has been cited by others (low citation count on a 2009 paper = suspicious)
4. If found:
   □ Note the DOI or direct link
   □ Mark as VERIFIED in your papers-list.md
5. If NOT found after 2–3 different search variations:
   □ Mark as NOT FOUND
   □ Do NOT include in your reference list
   □ Do NOT ask AI for an alternative without verifying the alternative too
```

---

## Preliminary Research Gap (to finalize in Week 2, Day 3)

Most existing studies on adversarial attacks against ML-based intrusion detection systems either (a) focus on neural network architectures where gradient-based attacks apply directly, or (b) evaluate only theoretical robustness without measuring real-world recovery under adversarial conditions. Fewer studies specifically demonstrate the effectiveness of adversarial training as a defense for tree-based classifiers (like Random Forest) on a controlled benchmark dataset (NSL-KDD) under a simulated feature-space evasion scenario. Your project addresses this precise gap — a measurable, end-to-end experimental evaluation of adversarial training for a Random Forest IDS on NSL-KDD under controlled Gaussian feature perturbation.

---

*Artifact created: Week 1, Day 2*
*Next session (Day 3): Finalize the research question and scope*

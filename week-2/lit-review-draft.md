# Week 2 — Literature Review Draft

---

## Research Gap Statement

While adversarial attacks on deep neural network-based classifiers have been extensively studied in the ML security literature (Goodfellow et al., 2015; Madry et al., 2018), comparatively little work evaluates the adversarial vulnerability of simpler tree-based classifiers — such as Random Forest — under controlled feature-space perturbation conditions using the NSL-KDD intrusion detection benchmark. Furthermore, most studies that address adversarial robustness in cybersecurity focus on gradient-based attacks, which are not directly applicable to non-differentiable models. This case study addresses this gap by providing a controlled, end-to-end experimental evaluation of feature-space evasion attack impact and adversarial training recovery for a Random Forest IDS on NSL-KDD.

---

## 4. Background and Related Work

[AI DRAFT — VERIFY ALL CITATIONS AND CLAIMS AGAINST ORIGINAL PAPERS]

### 4.1 ML-Based Intrusion Detection Systems

Machine learning-based intrusion detection systems (IDS) have been extensively studied using public benchmark datasets such as NSL-KDD (Tavallaee et al., 2009), which was developed specifically to address the class imbalance and redundancy issues present in the earlier KDD Cup 1999 dataset. Comparative studies have demonstrated that ensemble methods such as Random Forest consistently achieve high accuracy in binary and multi-class network traffic classification tasks on NSL-KDD (Revathi & Malathi, 2013). Broader surveys of the IDS landscape (Khraisat et al., 2019) confirm that anomaly-based ML classifiers offer strong detection capabilities against known attack categories including Denial of Service (DoS), Probe, Remote-to-Local (R2L), and User-to-Root (U2R) attacks. However, these evaluations are conducted exclusively under clean, unperturbed test conditions, leaving the adversarial robustness of such systems largely unaddressed.

### 4.2 Adversarial Attacks on ML-Based Security Systems

The susceptibility of machine learning models to adversarial manipulation was formally established by Szegedy et al. (2014), who demonstrated that imperceptibly small structured perturbations to input samples could reliably cause misclassification in deep neural networks. Goodfellow et al. (2015) subsequently proposed the Fast Gradient Sign Method (FGSM), explaining adversarial vulnerability through the linearity of high-dimensional models and providing a practical, efficient attack algorithm. In the cybersecurity domain, Corona et al. (2013) provided a taxonomy of adversarial threats targeting intrusion detection systems, distinguishing evasion attacks — which manipulate test inputs to bypass a deployed model — from poisoning attacks, which corrupt the training data. These works collectively establish that ML-based security systems face adversarial risks that are not captured by standard clean-data evaluation protocols, and that evasion attacks pose particular practical risk to deployed IDS.

### 4.3 Adversarial Training as a Defense

Adversarial training has emerged as one of the most widely studied and theoretically grounded defenses against adversarial attacks. Madry et al. (2018) formalized adversarial training as a min-max optimization problem, demonstrating that models trained on adversarially perturbed examples exhibit measurably greater robustness when subsequently tested under attack conditions. Tramèr et al. (2018) extended this approach through ensemble adversarial training, showing that augmenting training data with adversarial examples from multiple model architectures produces more generalizable defenses. Both works acknowledge that adversarial training introduces a trade-off between clean-data accuracy and adversarial robustness, and that robustness does not generalize unconditionally to all attack types. These findings directly inform the defense mechanism evaluated in this case study.

### 4.4 Research Gap

While adversarial attacks on deep neural network-based classifiers have been extensively studied in the ML security literature (Goodfellow et al., 2015; Madry et al., 2018), comparatively little work evaluates the adversarial vulnerability and recoverability of simpler tree-based classifiers under controlled feature-space perturbation on the NSL-KDD benchmark. Furthermore, most adversarial robustness studies in cybersecurity focus on gradient-based attacks, which are not directly applicable to non-differentiable models such as Random Forest. This case study addresses this gap by providing a controlled, end-to-end experimental evaluation of feature-space evasion impact and adversarial training recovery for a Random Forest IDS.

---

## Reference List (APA Format)
*Only include entries marked VERIFIED. Entries marked ⚠️ must be verified on Google Scholar before final submission.*

---

### Verified References ✅

Carlini, N., & Wagner, D. (2017). Towards evaluating the robustness of neural networks. *Proceedings of the IEEE Symposium on Security and Privacy (S&P)*, 39–57.

Goodfellow, I. J., Shlens, J., & Szegedy, C. (2015). Explaining and harnessing adversarial examples. *Proceedings of the International Conference on Learning Representations (ICLR 2015)*.

Madry, A., Makelov, A., Schmidt, L., Tsipras, D., & Vladu, A. (2018). Towards deep learning models resistant to adversarial attacks. *Proceedings of the International Conference on Learning Representations (ICLR 2018)*.

Szegedy, C., Zaremba, W., Sutskever, I., Bruna, J., Erhan, D., Goodfellow, I., & Fergus, R. (2014). Intriguing properties of neural networks. *Proceedings of the International Conference on Learning Representations (ICLR 2014)*.

Tavallaee, M., Bagheri, E., Lu, W., & Ghorbani, A. A. (2009). A detailed analysis of the KDD CUP 99 data set. *Proceedings of the IEEE Symposium on Computational Intelligence for Security and Defense Applications (CISDA)*, 1–6.

Tramèr, F., Kurakin, A., Papernot, N., Goodfellow, I., Boneh, D., & McDaniel, P. (2018). Ensemble adversarial training: Attacks and defenses. *Proceedings of the International Conference on Learning Representations (ICLR 2018)*.

---

### Pending Verification ⚠️

Corona, I., Giacinto, G., & Roli, F. (2013). Adversarial attacks against intrusion detection systems: Taxonomy, solutions and open issues. *Information Sciences*, 239, 201–225. [⚠️ VERIFY on Google Scholar]

Ingre, B., & Yadav, A. (2015). Performance analysis of NSL-KDD dataset using ANN. *IEEE International Conference on Signal Processing and Communication Engineering Systems (SPACES)*. [⚠️ VERIFY on Google Scholar]

Khraisat, A., Gondal, I., Vamplew, P., & Kamruzzaman, J. (2019). Survey of intrusion detection systems: techniques, datasets and challenges. *Cybersecurity*, 2(1), 20. [⚠️ VERIFY on Google Scholar]

Revathi, S., & Malathi, A. (2013). A detailed analysis on NSL-KDD dataset using various machine learning techniques for intrusion detection. *International Journal of Engineering Research & Technology (IJERT)*, 2(11). [⚠️ VERIFY on Google Scholar]

---

## Week 2 Summary

**What was accomplished this week:**
- Summarized 9 papers across 3 themes (ML-IDS, adversarial attacks, adversarial training)
- 5 papers are high-confidence verified; 4 require Google Scholar verification before citing
- Written synthesis paragraphs for each theme
- Assembled a 400–500 word literature review draft with 4 sub-sections
- Identified the research gap specific to this project
- Formatted an APA reference list

**Artifacts produced:**
- `week-2/literature-notes.md` — all paper summaries + synthesis + draft paragraphs
- `week-2/lit-review-draft.md` — this file

**Scope lock — do NOT change:**
- Number of papers: 9 candidates (5 verified + 4 to verify) — do not add more
- Literature review length: keep to 400–500 words in the final report
- Research gap statement is finalized — do not expand the scope

**Next week (Week 3):** Design the framework architecture diagram and set up the Google Colab coding environment. No new papers. No new scope additions.

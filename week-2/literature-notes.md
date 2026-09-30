# Week 2 — Literature Notes
*Running document for all paper summaries — Themes A, B, C*

---

## Paper Summary Template

| Field | Details |
|---|---|
| Citation | Author(s), Year, Title, Venue |
| Problem addressed | What research problem does this paper tackle? |
| Dataset used | Which dataset(s) were used? |
| Method/model | What classifier, algorithm, or technique? |
| Key result | The main finding, with numbers if available |
| Relevance to project | One sentence connecting to this case study |
| Limitation | One limitation the paper mentions or that is evident |

---

## THEME A — ML-Based Network Intrusion Detection

---

### A1 — Tavallaee et al. (2009) ✅ VERIFIED

| Field | Details |
|---|---|
| **Citation** | Tavallaee, M., Bagheri, E., Lu, W., & Ghorbani, A. A. (2009). A detailed analysis of the KDD CUP 99 data set. *IEEE Symposium on Computational Intelligence for Security and Defense Applications (CISDA)*. |
| **Problem addressed** | The KDD Cup 1999 dataset, widely used in IDS research, contains approximately 78% duplicate records in the training set and 75% in the test set, leading to biased classifier results and unreliable benchmarks. |
| **Dataset used** | KDD Cup 1999 (and the proposed NSL-KDD as replacement) |
| **Method/model** | Statistical analysis of dataset properties; comparison of classifier performance (NB Tree, Random Forest, J48) on both datasets |
| **Key result** | NSL-KDD eliminates redundant records, resulting in more balanced evaluation; classifiers trained on NSL-KDD produce more reliable and generalizable results than those on KDD99 |
| **Relevance to project** | Foundational justification for using NSL-KDD — this paper must be cited in the Dataset section of the methodology |
| **Limitation** | NSL-KDD itself is based on 1998–1999 traffic data and does not represent modern network attack patterns |

---

### A2 — Revathi & Malathi (2013) ⚠️ VERIFY BEFORE CITING

| Field | Details |
|---|---|
| **Citation** | Revathi, S., & Malathi, A. (2013). A detailed analysis on NSL-KDD dataset using various machine learning techniques for intrusion detection. *International Journal of Engineering Research & Technology (IJERT)*, 2(11). |
| **Problem addressed** | Evaluating and comparing multiple ML classifiers for network intrusion detection on the NSL-KDD benchmark |
| **Dataset used** | NSL-KDD |
| **Method/model** | Decision Tree (J48), Random Forest, Naïve Bayes, SVM — binary and multi-class classification |
| **Key result** | Random Forest achieves higher detection accuracy than Naïve Bayes and SVM on NSL-KDD; exact figures depend on the verified paper |
| **Relevance to project** | Directly supports the choice of Random Forest as the baseline classifier; provides a performance baseline to compare your results against |
| **Limitation** | Study does not evaluate model robustness under adversarial conditions — evaluates only clean data performance |

⚠️ *Verify: Search "Revathi Malathi NSL-KDD machine learning intrusion detection 2013" on Google Scholar. Confirm volume, page numbers, and whether journal is indexed.*

---

### A3 — Khraisat et al. (2019) ⚠️ VERIFY BEFORE CITING

| Field | Details |
|---|---|
| **Citation** | Khraisat, A., Gondal, I., Vamplew, P., & Kamruzzaman, J. (2019). Survey of intrusion detection systems: techniques, datasets and challenges. *Cybersecurity*, 2(1), 20. |
| **Problem addressed** | Comprehensive review of IDS techniques, benchmark datasets, and open challenges in network intrusion detection |
| **Dataset used** | Survey — covers NSL-KDD, CICIDS2017, and others |
| **Method/model** | Literature survey across signature-based, anomaly-based, and hybrid approaches |
| **Key result** | Anomaly-based ML approaches offer higher detection of zero-day attacks but suffer from higher false positive rates; NSL-KDD and CICIDS2017 are the most commonly used benchmarks |
| **Relevance to project** | Provides broad context for the IDS landscape; supports the statement that ML-based anomaly detection is an active area with known vulnerabilities |
| **Limitation** | Survey does not evaluate adversarial robustness of reviewed systems |

⚠️ *Verify: Search "Survey intrusion detection systems Khraisat 2019 Cybersecurity Springer" on Google Scholar.*

---

### A4 — Ingre & Yadav (2015) ⚠️ VERIFY BEFORE CITING

| Field | Details |
|---|---|
| **Citation** | Ingre, B., & Yadav, A. (2015). Performance analysis of NSL-KDD dataset using ANN. *International Conference on Signal Processing and Communication Engineering Systems (SPACES)*. IEEE. |
| **Problem addressed** | Comparing ML classifier performance on NSL-KDD with a focus on detection rate and false alarm rate |
| **Dataset used** | NSL-KDD |
| **Method/model** | ANN (Artificial Neural Network), compared against other classifiers |
| **Key result** | ANN achieves improved detection rates over simpler classifiers on NSL-KDD; false alarm rate varies across attack types |
| **Relevance to project** | Provides additional benchmark context for NSL-KDD performance; useful comparison point for your baseline results |
| **Limitation** | Uses neural network (ANN), not a tree-based approach; no adversarial robustness evaluation |

⚠️ *Verify: Search "Ingre Yadav NSL-KDD ANN SPACES 2015 IEEE" on Google Scholar. Confirm conference name and year.*

---

### Theme A — Synthesis Paragraph

The reviewed literature on ML-based intrusion detection systems shows consistent use of the NSL-KDD benchmark (Tavallaee et al., 2009) as the primary evaluation dataset, with Random Forest and tree-based classifiers frequently achieving strong detection accuracy under clean conditions (Revathi & Malathi, 2013; Ingre & Yadav, 2015). Survey work (Khraisat et al., 2019) confirms that anomaly-based ML approaches remain an active area with well-documented strengths in detecting novel attack patterns. A common thread across these studies is that model evaluation is performed exclusively under clean, attack-free test conditions — leaving open the question of how these classifiers behave when inputs are deliberately manipulated.

---

### Theme A — [AI DRAFT — VERIFY] Literature Review Paragraph

[AI DRAFT — VERIFY] Machine learning-based intrusion detection systems (IDS) have been extensively studied using public benchmark datasets such as NSL-KDD (Tavallaee et al., 2009), which was developed specifically to address the class imbalance and redundancy issues in the earlier KDD Cup 1999 dataset. Comparative studies have demonstrated that ensemble methods such as Random Forest consistently achieve high accuracy in binary and multi-class network traffic classification tasks on NSL-KDD (Revathi & Malathi, 2013). Broader surveys of the IDS landscape (Khraisat et al., 2019) confirm that anomaly-based ML classifiers offer strong detection capabilities against known attack categories including Denial of Service (DoS), Probe, Remote-to-Local (R2L), and User-to-Root (U2R) attacks. However, these evaluations are conducted exclusively under clean, unperturbed test conditions, leaving the adversarial robustness of such systems largely unaddressed.

---

---

## THEME B — Adversarial Attacks on ML Models in Cybersecurity

---

### B1 — Szegedy et al. (2014) ✅ VERIFIED

| Field | Details |
|---|---|
| **Citation** | Szegedy, C., Zaremba, W., Sutskever, I., Bruna, J., Erhan, D., Goodfellow, I., & Fergus, R. (2014). Intriguing properties of neural networks. *International Conference on Learning Representations (ICLR 2014)*. |
| **Problem addressed** | The existence of adversarial examples — imperceptibly small perturbations to inputs that cause deep neural networks to produce incorrect classifications with high confidence |
| **Dataset used** | ImageNet, MNIST |
| **Method/model** | Deep neural networks (convolutional); box-constrained L-BFGS to generate adversarial examples |
| **Key result** | Small structured perturbations to inputs (invisible to humans) cause consistent misclassification; adversarial examples transfer across different model architectures |
| **Relevance to project** | Establishes the foundational concept of adversarial vulnerability — used in the introduction and background to motivate why ML security systems can be fooled |
| **Limitation** | Focused on image classification; does not directly address network security or tabular/structured data |

---

### B2 — Goodfellow et al. (2015) ✅ VERIFIED

| Field | Details |
|---|---|
| **Citation** | Goodfellow, I. J., Shlens, J., & Szegedy, C. (2015). Explaining and harnessing adversarial examples. *International Conference on Learning Representations (ICLR 2015)*. |
| **Problem addressed** | Explaining why neural networks are vulnerable to adversarial examples and proposing a fast method (FGSM) to generate them |
| **Dataset used** | MNIST, CIFAR-10 |
| **Method/model** | Fast Gradient Sign Method (FGSM) — adds perturbation in the direction of the gradient of the loss function |
| **Key result** | Adversarial vulnerability arises from the linear nature of high-dimensional models; FGSM generates effective adversarial examples in a single forward-backward pass |
| **Relevance to project** | Provides the theoretical explanation for why adversarial attacks work — even though FGSM is not used in this project (it requires gradients), the principle of perturbing input features to cause misclassification is directly analogous to the feature-space perturbation approach used here |
| **Limitation** | FGSM requires a differentiable model; not directly applicable to Random Forest |

---

### B3 — Carlini & Wagner (2017) ✅ VERIFIED

| Field | Details |
|---|---|
| **Citation** | Carlini, N., & Wagner, D. (2017). Towards evaluating the robustness of neural networks. *IEEE Symposium on Security and Privacy (S&P 2017)*. |
| **Problem addressed** | Showing that popular adversarial defense techniques (including some forms of adversarial training) can be broken by a stronger, more carefully optimized attack |
| **Dataset used** | MNIST, CIFAR-10 |
| **Method/model** | C&W attack — optimization-based attack that directly minimizes perturbation magnitude |
| **Key result** | Many defenses that appeared to work against FGSM were broken by C&W; demonstrates that adversarial robustness must be evaluated against strong attacks, not just weak ones |
| **Relevance to project** | Important context for the limitations section — your defense (adversarial training with Gaussian noise) is a simple defense and may not hold against stronger, optimized attacks |
| **Limitation** | Focused on neural networks; gradient-based attacks do not directly apply to Random Forest |

---

### B4 — Corona et al. (2013) ⚠️ VERIFY BEFORE CITING

| Field | Details |
|---|---|
| **Citation** | Corona, I., Giacinto, G., & Roli, F. (2013). Adversarial attacks against intrusion detection systems: Taxonomy, solutions and open issues. *Information Sciences*, 239, 201–225. |
| **Problem addressed** | Provides a structured taxonomy of adversarial attacks specifically targeting intrusion detection systems — distinguishing evasion attacks, poisoning attacks, and causative attacks |
| **Dataset used** | Survey paper — no single dataset |
| **Method/model** | Taxonomy and literature analysis |
| **Key result** | Evasion attacks (at inference time) are the most practically threatening; most IDS defenses at the time were not designed with adversarial manipulation in mind |
| **Relevance to project** | Most directly relevant paper to your project framing — explicitly discusses adversarial evasion attacks on IDS; supports the motivation for studying adversarial robustness |
| **Limitation** | Survey from 2013; pre-dates the deep learning era of adversarial ML |

⚠️ *Verify: Search "Corona Giacinto Roli adversarial attacks intrusion detection 2013 Information Sciences" on Google Scholar.*

---

### Theme B — Synthesis Paragraph

The adversarial ML literature demonstrates that machine learning classifiers — from image recognizers to intrusion detection systems — are inherently vulnerable to deliberate input manipulation (Szegedy et al., 2014; Goodfellow et al., 2015). In the cybersecurity domain, Corona et al. (2013) show that evasion attacks, which occur at inference time, are among the most practically dangerous because they allow adversaries to bypass a deployed model without modifying the training data. Carlini & Wagner (2017) further demonstrate that many proposed defenses fail under stronger attack conditions, underscoring the need for robust evaluation methodology. The common focus of these works is on neural network architectures, leaving the adversarial behavior of simpler tree-based classifiers under feature-space perturbation comparatively understudied.

---

### Theme B — [AI DRAFT — VERIFY] Literature Review Paragraph

[AI DRAFT — VERIFY] The susceptibility of machine learning models to adversarial manipulation was formally established by Szegedy et al. (2014), who demonstrated that imperceptibly small structured perturbations to input samples could reliably cause misclassification in deep neural networks. Goodfellow et al. (2015) subsequently proposed the Fast Gradient Sign Method (FGSM), explaining adversarial vulnerability through the lens of model linearity and providing a practical attack algorithm. In the context of intrusion detection, Corona et al. (2013) provided a taxonomy of adversarial threats to IDS, distinguishing evasion attacks — which manipulate test inputs to bypass a deployed model — from poisoning attacks, which target the training process. These works collectively establish that ML-based security systems face adversarial risks that are not captured by standard clean-data evaluation protocols.

---

---

## THEME C — Adversarial Training as a Defense

---

### C1 — Madry et al. (2018) ✅ VERIFIED

| Field | Details |
|---|---|
| **Citation** | Madry, A., Makelov, A., Schmidt, L., Tsipras, D., & Vladu, A. (2018). Towards deep learning models resistant to adversarial attacks. *International Conference on Learning Representations (ICLR 2018)*. |
| **Problem addressed** | Formulating adversarial robustness as an optimization problem and proposing PGD-based adversarial training as a principled defense |
| **Dataset used** | MNIST, CIFAR-10 |
| **Method/model** | Projected Gradient Descent (PGD) adversarial training — models are trained on PGD-generated adversarial examples |
| **Key result** | PGD adversarial training produces models that are measurably more robust to adversarial inputs; robustness trades off slightly against clean-data accuracy |
| **Relevance to project** | Theoretical basis for the adversarial training defense used in this project; your Week 6 defense is a simplified version of this principle applied to a non-differentiable model |
| **Limitation** | Designed for neural networks with differentiable loss; also introduces a trade-off between adversarial robustness and clean-data accuracy |

---

### C2 — Tramèr et al. (2018) ✅ VERIFIED

| Field | Details |
|---|---|
| **Citation** | Tramèr, F., Kurakin, A., Papernot, N., Goodfellow, I., Boneh, D., & McDaniel, P. (2018). Ensemble adversarial training: Attacks and defenses. *International Conference on Learning Representations (ICLR 2018)*. |
| **Problem addressed** | Single-model adversarial training can overfit to one attack type; ensemble adversarial training (using adversarial examples from multiple pre-trained models) produces more generalizable robustness |
| **Dataset used** | MNIST, CIFAR-10, ImageNet |
| **Method/model** | Ensemble adversarial training — augment training with adversarial examples generated from multiple external models |
| **Key result** | Ensemble adversarial training reduces error on adversarial examples by up to 50% compared to single-model adversarial training; shows that attack transferability can be leveraged for stronger defenses |
| **Relevance to project** | Provides a theoretical upper bound — your project uses single-model adversarial training (simpler), so results may show partial but not maximal recovery; cite this to explain the limitation of your approach |
| **Limitation** | Requires access to multiple pre-trained models; computationally expensive; still breakable by adaptive attacks |

---

### Theme C — Synthesis Paragraph

Adversarial training — augmenting training data with adversarial examples and retraining the classifier — is the most studied and best-understood defense against adversarial attacks (Madry et al., 2018; Tramèr et al., 2018). The core principle is that by exposing the model to adversarial manipulations during training, it learns to classify them correctly rather than being fooled by them. Both papers demonstrate measurable improvements in adversarial robustness, though both note that single-model adversarial training does not guarantee full robustness against all attack types. For the purposes of this case study, single-model adversarial training using Gaussian feature perturbation is a valid and academically recognized approach, with known limitations that will be addressed in the discussion section.

---

### Theme C — [AI DRAFT — VERIFY] Literature Review Paragraph

[AI DRAFT — VERIFY] Adversarial training has emerged as one of the most widely studied and theoretically grounded defenses against adversarial attacks. Madry et al. (2018) formalized adversarial training as a min-max optimization problem, demonstrating that models trained on adversarially perturbed examples exhibit measurably greater robustness when subsequently tested under attack conditions. Tramèr et al. (2018) extended this approach through ensemble adversarial training, showing that augmenting training data with adversarial examples from multiple model architectures produces more generalizable defenses. Both works acknowledge that adversarial training introduces a trade-off between clean-data accuracy and adversarial robustness, and that robustness does not transfer unconditionally to all attack types. These findings directly inform the defense strategy used in this case study.

---

### Adversarial Training: Core Concept Explanation (for Methodology Section)

**Why adversarial training is a valid and simple defense:**
Adversarial training works on a straightforward principle: if the model has already seen "disguised" attack samples during training (with their correct labels), it is harder to fool with the same type of disguise at test time. The model learns that even noisy or slightly altered attack-class samples should still be classified as attacks. For a Random Forest, this means the tree structure adapts to create decision boundaries that capture both clean and perturbed versions of attack-class samples.

**Core assumption about the attacker:**
Adversarial training assumes the attacker uses a similar perturbation strategy to the one used during training augmentation. If the attacker uses a completely different attack type or a higher noise magnitude, the defense may not generalize. This is called the "assumption of bounded perturbation" — the defense is optimized for attacks within a certain range.

**Known limitations (for limitations section):**
1. The defense is only as good as the diversity of adversarial examples in the augmented training set — training on noise std=0.3 may not defend well against std=1.0
2. Adversarial training can reduce clean-data accuracy slightly (robustness–accuracy trade-off)
3. A more sophisticated attacker who knows the defense has been applied can craft stronger attacks to bypass it (Carlini & Wagner, 2017)
4. For non-differentiable models like Random Forest, the adversarial training defense is a heuristic approximation rather than a provably optimal solution

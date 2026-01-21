# 🌿 Plant-AI-Doctor: Bridging the Domain Gap
### Identifying Plant Damage using Synthetic Data Generation

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/15SIcFFvEeJNajn0oGCANytRk3ma9wmNt?usp=sharing)

This project addresses a critical gap in precision agriculture: the lack of labeled data for **Chemical Damage** in plants. By leveraging **Generative AI**, we created a robust diagnostic tool that distinguishes between biological diseases and chemical-induced stress.

---

## 📖 Project Overview
While biological diseases (fungi, bacteria) are well-documented, chemical damage (herbicide drift, fertilizer burn) lacks large-scale datasets. This project introduces a workflow to:
1.  **Generate** hyper-realistic synthetic data using **Stable Diffusion Inpainting, ControlNet and Vertex AI**.
2.  **Train** a Deep Learning model to recognize unique chemical damage patterns.
3.  **Validate** the model on **100% real-world field images**, proving the effectiveness of synthetic-to-real domain adaptation.

---

## 🚀 Key Innovations
* **Synthetic Data Pipeline:** Overcoming data scarcity by "painting" chemical burn textures onto healthy leaf structures.
* **Interpretability with Grad-CAM:** Visualizing the model's focus to ensure it identifies physiological symptoms rather than background noise.

---

## 📊 Performance Metrics (Real-World Data)
The model was tested on a ground-truth dataset of **751 real-world images** (690 Biological, 61 Chemical).

| Metric | Result | Formula |
| :--- | :--- | :--- |
| **Biological Specificity** | **100.00%** | $Spec = \frac{TN}{TN + FP}$ |
| **Chemical Recall** | **93.44%** | $Rec = \frac{TP}{TP + FN}$ |
| **F1-Score** | **~93%** | $2 \cdot \frac{Prec \cdot Rec}{Prec + Rec}$ |
| **Stress Test Consistency** | **86.89%** | (Center Crop Stability) |

---

## 🛠️ Methodology

### 1. Synthetic Data Generation Pipeline (GenAI)

To overcome the critical scarcity of labeled chemical damage data, we developed a high-fidelity generation pipeline:

* **Structural Integrity:** Leveraged **ControlNet (Canny Edge)** to lock the anatomical morphology of healthy tomato leaves, ensuring the AI modified only the health status, not the leaf structure.
* **Pathological Simulation:** Engineered dynamic prompts to simulate specific symptoms of **Chemical Necrosis** (browning) and **Interveinal Chlorosis** (yellowing) caused by herbicide drift.
* **Automated Diversity:** Scaled generation via **Vertex AI** to introduce variability in damage severity, lighting, and angles, preventing model overfitting to synthetic patterns.
* **Domain Adaptation:** Successfully transformed healthy leaf foundations into a balanced training set for "edge-case" chemical signatures that are rare in the field.

### 2. 📊 Train 
To ensure a robust evaluation, we implemented a three-way split of the hybrid dataset:

* **Training Set (70%):** Used to update model weights and learn features from both synthetic (GenAI) and real images.
* **Validation Set (15%):** Used during the training phase to monitor performance and tune hyperparameters (**Preventing Overfitting**).
* **Internal Test Set (15%):** Held out entirely from the training process for initial performance verification.
* **External Real-World Benchmark:** A final stress test performed on **61 ground-truth chemical field images** to validate sim-to-real generalization.

### 3. Stress Testing (Robustness)
We performed a **Center Crop Stress Test** to verify that the model relies on leaf texture rather than background shortcuts. The model maintained an **86.89% consistency rate**, proving its focus on the plant's health status.

---

## 🔍 Failure Analysis
The 6% error margin on chemical images was analyzed using Grad-CAM. Key challenges include:
* **Structural Epinasty:** Leaf twisting without significant color change.
* **Marginal Necrosis:** Damage at leaf edges that mimics biological nutrient deficiency.
* **Low Resolution:** Fine spotting that becomes indistinct at $224 \times 224$ pixels.

---


# 🌿 Plant-AI-Doctor: Bridging the Domain Gap
### Identifying Plant Damage using Synthetic Data Generation

This project addresses a critical gap in precision agriculture: the lack of labeled data for **Chemical Damage** in plants. By leveraging **Generative AI**, we created a robust diagnostic tool that distinguishes between biological diseases and chemical-induced stress.

---

## 📖 Project Overview
While biological diseases (fungi, bacteria) are well-documented, chemical damage (herbicide drift, fertilizer burn) lacks large-scale datasets. This project introduces a workflow to:
1.  **Generate** hyper-realistic synthetic data using **Stable Diffusion** and **ControlNet**.
2.  **Train** a Deep Learning model to recognize unique chemical damage patterns.
3.  **Validate** the model on **100% real-world field images**, proving the effectiveness of synthetic-to-real domain adaptation.

---

## 🚀 Key Innovations
* **Synthetic Data Pipeline:** Overcoming data scarcity by "painting" chemical burn textures onto healthy leaf structures.
* **Zero-Shot Baseline Comparison:** Proving that standard models are "blind" to chemical damage without this specialized training.
* **Interpretability with Grad-CAM:** Visualizing the model's focus to ensure it identifies physiological symptoms rather than background noise.

---

## 📊 Performance Metrics (Real-World Data)
The model was tested on a ground-truth dataset of **751 real-world images** (690 Biological, 61 Chemical).

| Metric | Result | Formula |
| :--- | :--- | :--- |
| **Biological Specificity** | **100.00%** | $Spec = \frac{TN}{TN + FP}$ |
| **Chemical Recall** | **86.89%** | $Rec = \frac{TP}{TP + FN}$ |
| **F1-Score** | **~93%** | $2 \cdot \frac{Prec \cdot Rec}{Prec + Rec}$ |
| **Stress Test Consistency** | **86.89%** | (Center Crop Stability) |

### 🔬 The Baseline Proof
To demonstrate the value of the synthetic data, we compared our model to a baseline trained only on biological/healthy data:
* **Baseline Recall (Chemical):** $0.00\%$
* **Our Model Recall (Chemical):** **$86.89\%$**
> **Impact:** The generative AI training provided the missing features required to identify chemical signatures that standard datasets lack.

---

## 🛠️ Methodology

### 1. Data Generation (Stable Diffusion)
Using **ControlNet** with Canny edge detection, we maintained the anatomical structure of tomato leaves while applying custom prompts to simulate chemical necrosis and chlorosis.

### 2. Deep Learning Architecture
A **ResNet18** backbone was fine-tuned on a multi-domain dataset. 
* **Training:** 80% Synthetic/Mix.
* **Validation:** 20% Synthetic/Mix.
* **Final Test:** 100% Real-world field images.

### 3. Stress Testing (Robustness)
We performed a **Center Crop Stress Test** to verify that the model relies on leaf texture rather than background shortcuts. The model maintained an **86.89% consistency rate**, proving its focus on the plant's health status.

---

## 🔍 Failure Analysis
The 13% error margin on chemical images was analyzed using Grad-CAM. Key challenges include:
* **Structural Epinasty:** Leaf twisting without significant color change.
* **Marginal Necrosis:** Damage at leaf edges that mimics biological nutrient deficiency.
* **Low Resolution:** Fine spotting that becomes indistinct at $224 \times 224$ pixels.

---

## 🛠️ Installation
```bash
# Clone the repository
git clone [https://github.com/YourUsername/Plant-AI-Doctor.git](https://github.com/YourUsername/Plant-AI-Doctor.git)

# Install dependencies
pip install -r requirements.txt

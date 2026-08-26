# Support Vector Machine (SVM) — Concepts, Kernel Trick & Hyperparameter Tuning

A hands-on, notebook-based project that builds intuition for **Support Vector Machines (SVM)** — from a real-world classification task to visually understanding the **kernel trick** and the effect of the **C** and **gamma** hyperparameters on the decision boundary.

---

## 📁 Repository Structure

```
├── SVM_classifier.ipynb                          # SVM on a real dataset (Breast Cancer classification)
├── SVM_Kernel_Trick.ipynb                        # Linear vs RBF kernel — visualizing the kernel trick
├── svm-c-gamma-hyperparameters-notebook.ipynb     # Effect of C & gamma on the decision boundary
├── images/                                        # Plots exported from the notebooks (used in this README)
└── README.md
```

> **Note:** The `.ipynb_checkpoints`-style duplicate files (auto-saved copies created by Jupyter) are excluded from this repo — see [`.gitignore`](#-gitignore) below.

---

## 📌 Project Overview

| Notebook | What it covers |
|---|---|
| [`SVM_classifier.ipynb`](#1-svm_classifieripynb--breast-cancer-classification) | End-to-end SVM classification pipeline on the Scikit-Learn Breast Cancer dataset |
| [`SVM_Kernel_Trick.ipynb`](#2-svm_kernel_trickipynb--visualizing-the-kernel-trick) | Why a linear kernel fails on non-linear data, and how the RBF kernel (kernel trick) fixes it |
| [`svm-c-gamma-hyperparameters-notebook.ipynb`](#3-svm-c-gamma-hyperparameters-notebookipynb--tuning-c--gamma) | How `C` and `gamma` individually and jointly reshape the SVM decision boundary |

---

## 1. `SVM_classifier.ipynb` — Breast Cancer Classification

**Goal:** Train and evaluate an SVM classifier on a real medical dataset to predict whether a tumor is malignant or benign.

**Workflow followed in the notebook:**
1. **Import libraries** — `pandas`, `numpy`, `matplotlib`, `scikit-learn`
2. **Load dataset** — `sklearn.datasets.load_breast_cancer()` (569 samples, 30 numeric features)
3. **Explore data** — shape, missing values (`isna().sum()`), data types
4. **Preprocess** — feature/target split, then `StandardScaler` to normalize all 30 features
5. **Train/test split** — 80/20 split with `stratify=y` to preserve class balance
6. **Model building & training** — `sklearn.svm.SVC()` (default RBF kernel), with training time measured
7. **Evaluation** — on both train and test sets using:
   - Confusion Matrix
   - Accuracy Score
   - Precision Score
   - Recall Score
   - Full `classification_report`

**Key takeaway:** A properly scaled, out-of-the-box SVM performs strongly on high-dimensional tabular medical data, and the notebook demonstrates the complete supervised-learning workflow — from raw data to evaluated model.

---

## 2. `SVM_Kernel_Trick.ipynb` — Visualizing the Kernel Trick

**Goal:** Build visual intuition for *why* SVMs use kernels — by comparing a **linear kernel** against an **RBF (non-linear) kernel** on data that isn't linearly separable in 2D.

**Workflow followed in the notebook:**
1. Custom helper functions to plot the **2D decision boundary** and a **3D projection** of the data
2. Load a small labeled 2D dataset (`SVM_Data.xlsx`)
3. Train a **linear-kernel SVM** → evaluate accuracy, confusion matrix, and decision boundary
4. Train an **RBF-kernel SVM** on the same data → compare accuracy, confusion matrix, and decision boundary
5. Visualize how the RBF kernel implicitly lifts the data into a higher dimension (3D plot) to make it linearly separable — the essence of the **kernel trick**

**Dataset (2D, red = class 0, green = class 1):**

![Dataset scatter](images/05_kernel_data_full.png)

**Linear kernel fails — a straight boundary cannot separate the classes:**

![Linear decision boundary](images/06_kernel_linear_boundary.png)

**The kernel trick — lifting the data into 3D reveals a clean separation:**

![3D kernel trick projection](images/07_kernel_trick_3d.png)

**RBF kernel — a curved (non-linear) boundary correctly separates the classes:**

![RBF decision boundary](images/08_kernel_rbf_boundary.png)

**Key takeaway:** When classes aren't linearly separable in the original feature space, the RBF kernel effectively maps points into a higher-dimensional space (without explicitly computing that transformation) where a clean separating boundary exists — that's the kernel trick.

---

## 3. `svm-c-gamma-hyperparameters-notebook.ipynb` — Tuning C & Gamma

**Goal:** Systematically vary the two most important SVM hyperparameters — **`gamma`** (kernel coefficient) and **`C`** (regularization strength) — and observe their effect on the decision boundary using a synthetic dataset (`make_classification`, 200 samples, poly kernel).

**Workflow followed in the notebook:**
1. Generate a synthetic 2-feature binary classification dataset
2. Define a reusable `generate_clf(gamma, C)` function that trains an `SVC(kernel="poly")` and reports training accuracy
3. Train and visualize **7 classifiers**, progressively changing gamma (`0.001 → 0.01 → 0.1 → 1`) with `C` fixed, then fixing `gamma=0.1` and varying `C` (`0.1 → 1 → 10`)
4. Record inline inferences after each experiment — connecting the visual boundary shape back to the theory

**Dataset used for all experiments:**

![Synthetic dataset](images/01_dataset_scatter.png)

**Very low gamma (0.001) — model underfits, everything classified as one class:**

![Low gamma underfit](images/02_gamma_low_underfit.png)

**Higher gamma (1) — a tighter, more flexible boundary starts fitting the true pattern:**

![Higher gamma boundary](images/03_gamma_high_boundary.png)

**Gamma = 0.1, C = 10 — high C forces stricter classification, boundary tightens further (risk of overfitting):**

![Gamma and C tuned](images/04_gamma_c_tuned.png)

**Key takeaways:**
- **Low gamma** → each point's influence spreads far → smoother/underfit boundary
- **High gamma** → each point's influence is very local → boundary hugs the training points closely (risk of overfitting)
- **Low C** → wider margin, tolerates some misclassification (better generalization)
- **High C** → narrower margin, penalizes misclassification heavily (higher training accuracy, but risk of overfitting)
- Choosing the right `C`–`gamma` combination is a **bias–variance trade-off**, best found via cross-validation / grid search in practice

---

## 🛠️ Tech Stack

- **Language:** Python 3
- **Libraries:** `pandas`, `numpy`, `matplotlib`, `scikit-learn`
- **Techniques:** Data preprocessing (`StandardScaler`), train/test split, SVM (`SVC` — linear, RBF, and polynomial kernels), model evaluation, decision-boundary visualization, hyperparameter analysis (`C`, `gamma`)

---

## ▶️ How to Run

```bash
# Clone the repository
git clone https://github.com/Tamilarasan123/<repo-name>.git
cd <repo-name>

# Install dependencies
pip install pandas numpy matplotlib scikit-learn openpyxl jupyter

# Launch Jupyter and open any notebook
jupyter notebook
```

> `SVM_Kernel_Trick.ipynb` requires the accompanying `SVM_Data.xlsx` file to be present in the same directory.

---

## 🚫 .gitignore

To keep the repository clean, exclude Jupyter's auto-generated checkpoint files:

```
.ipynb_checkpoints/
*-checkpoint.ipynb
__pycache__/
*.pyc
.DS_Store
```

---

## 👤 Author

**Tamilarasan K**
B.Tech, Artificial Intelligence & Data Science
🔗 [GitHub](https://github.com/Tamilarasan123) · [LinkedIn](https://linkedin.com/in/tamilarasan-k-03a27834b)

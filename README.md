# Machine Learning Study

A structured, hands-on record of my machine learning learning journey. Each folder covers one topic with its theory, Python implementation, and practice on real datasets, moving from basic regression to ensemble methods, clustering, recommendation systems and dimensionality reduction.

![Python](https://img.shields.io/badge/Python-3.x-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

---

## Table of Contents

- [About This Repository](#about-this-repository)
- [Learning Roadmap](#learning-roadmap)
- [Topics Covered](#topics-covered)
  - [Supervised Learning: Regression & Classification](#1-supervised-learning-regression--classification)
  - [Ensemble & Boosting Methods](#2-ensemble--boosting-methods)
  - [Data Preparation & Model Quality](#3-data-preparation--model-quality)
  - [Unsupervised Learning](#4-unsupervised-learning)
  - [Recommendation & Pattern Mining](#5-recommendation--pattern-mining)
  - [Dimensionality Reduction](#6-dimensionality-reduction)
- [Repository Structure](#repository-structure)
- [Tech Stack](#tech-stack)
- [Getting Started](#getting-started)
- [Typical Workflow Used in Every Topic](#typical-workflow-used-in-every-topic)
- [Key Learnings](#key-learnings)
- [Related Repositories](#related-repositories)
- [Author](#author)

---

## About This Repository

This repository is my personal study log for machine learning. The goals are:

- Understand the **intuition and math** behind each algorithm
- Implement algorithms in **Python** using scikit-learn and related libraries
- Learn **when to use which algorithm**, along with its strengths and limits
- Practise the full ML cycle: data cleaning, feature engineering, training, validation, tuning and interpretation

---

## Learning Roadmap

```
Regression → Classification → Trees → Ensembles → Validation
      ↓
Preprocessing → Imbalance & Tuning → Boosting (GB / XGB / LGBM)
      ↓
SVM → KNN → Regularization → Feature Engineering
      ↓
Clustering (K-Means, Hierarchical, DBSCAN)
      ↓
Association Rules → Recommendation Engine
      ↓
Dimensionality Reduction (PCA, t-SNE)
```

---

## Topics Covered

### 1. Supervised Learning: Regression & Classification

| # | Topic | What it covers |
|---|-------|----------------|
| 01 | [Linear Regression](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/01_Linear%20Regression) | Predicting continuous values, best-fit line, assumptions, R², MSE / RMSE / MAE |
| 02 | [Logistic Regression](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/02_Logistic_Regression) | Binary and multi-class classification, sigmoid function, odds, confusion matrix, ROC-AUC |
| 03 | [Decision Tree](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/03_Decision%20Tree) | Gini and entropy, information gain, tree depth, pruning, overfitting |
| 12 | [SVM](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/12_SVM) | Maximum-margin classifier, kernels (linear, polynomial, RBF), C and gamma tuning |
| 13 | [KNN](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/13_KNN) | Distance-based learning, choosing K, distance metrics, effect of feature scaling |

### 2. Ensemble & Boosting Methods

| # | Topic | What it covers |
|---|-------|----------------|
| 04 | [Ensemble Techniques](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/04_Ensamble_Tecniques) | Bagging, Random Forest, voting and stacking, bias-variance trade-off |
| 07 | [AdaBoost Script Understanding](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/07_AdaBoost_Script_Understanding) | Step-by-step walkthrough of AdaBoost: weak learners, sample re-weighting, final weighted vote |
| 09 | [Gradient Boosting](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/09_Gradient%20Boosting) | Sequential error correction, learning rate, number of estimators, loss functions |
| 10 | [EGB Classifier](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/10_EGB_Classifier) | Extreme gradient boosting classifier, regularized boosting, key hyperparameters |
| 11 | [LGBM & Feature Importance](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/11_LGBM%20%26%20Feature%20Importance) | LightGBM (leaf-wise growth, speed on large data) and interpreting feature importance |

### 3. Data Preparation & Model Quality

| # | Topic | What it covers |
|---|-------|----------------|
| 05 | [Model Validation Techniques](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/05_Model%20validation%20Techniques) | Train/test split, k-fold and stratified k-fold cross-validation, overfitting vs underfitting |
| 06 | [Data Preprocessing Techniques](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/06_Data_preprocessing_Techniques) | Missing values, outliers, encoding, scaling and normalization |
| 08 | [Handling Imbalance and Model Optimization](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/08_Handling%20Imbalance%20and%20Model%20Optimization) | Class imbalance (SMOTE, over/under-sampling, class weights), GridSearchCV and RandomizedSearchCV |
| 14 | [Regularization Techniques](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/14_Regularization%20Techniques) | Lasso (L1), Ridge (L2), Elastic Net, reducing overfitting |
| 15 | [Feature Engineering Techniques](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/15_Feature_Engineering_Techniques) | Creating, transforming and selecting features to improve model performance |

### 4. Unsupervised Learning

| # | Topic | What it covers |
|---|-------|----------------|
| 19.2 | [K-Means Clustering](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/19.2_K%20Mean%20Clustering) | Centroid-based clustering, elbow method, silhouette score |
| 19 | [Hierarchical Clustering](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/19_Clustering_Tecniques/Hierarchical%20Clustering) | Agglomerative clustering, linkage methods, dendrograms |
| 19.3 | [DBSCAN Techniques](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/19.3_DBScan%20Techniques) | Density-based clustering, eps and min_samples, noise and outlier detection |

### 5. Recommendation & Pattern Mining

| # | Topic | What it covers |
|---|-------|----------------|
| 20 | [Association Rules](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/20_Association%20Rules) | Market-basket analysis, Apriori, support, confidence, lift |
| 21 | [Recommendation Engine](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/21_Recommendation_Engine) | Content-based and collaborative filtering, similarity measures |

### 6. Dimensionality Reduction

| # | Topic | What it covers |
|---|-------|----------------|
| 22.2 | [PCA: Complete Theory and Scripting](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/22.2%20PCA%20Complete%20Theory%20and%20Scripting) | Variance, eigenvectors, principal components, explained variance ratio |
| 22.3 | [t-SNE](https://github.com/Tamilarsan123/Machine_learning_study/tree/main/22.3%20t-SNE) | Non-linear dimensionality reduction for visualizing high-dimensional data |

---

## Repository Structure

```
Machine_learning_study/
│
├── 01_Linear Regression/
├── 02_Logistic_Regression/
├── 03_Decision Tree/
├── 04_Ensamble_Tecniques/
├── 05_Model validation Techniques/
├── 06_Data_preprocessing_Techniques/
├── 07_AdaBoost_Script_Understanding/
├── 08_Handling Imbalance and Model Optimization/
├── 09_Gradient Boosting/
├── 10_EGB_Classifier/
├── 11_LGBM & Feature Importance/
├── 12_SVM/
├── 13_KNN/
├── 14_Regularization Techniques/
├── 15_Feature_Engineering_Techniques/
├── 19_Clustering_Tecniques/
│   └── Hierarchical Clustering/
├── 19.2_K Mean Clustering/
├── 19.3_DBScan Techniques/
├── 20_Association Rules/
├── 21_Recommendation_Engine/
├── 22.2 PCA Complete Theory and Scripting/
├── 22.3 t-SNE/
└── README.md
```

Each topic folder typically contains the notebook or script, the dataset used, and supporting notes.

---

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.x |
| Data handling | NumPy, Pandas |
| Machine learning | scikit-learn, XGBoost, LightGBM, imbalanced-learn, mlxtend |
| Visualization | Matplotlib, Seaborn |
| Environment | Jupyter Notebook / VS Code |
| Version control | Git, GitHub |

---

## Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/Tamilarsan123/Machine_learning_study.git
cd Machine_learning_study

# 2. (Optional) Create a virtual environment
python -m venv venv
source venv/bin/activate          # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install numpy pandas matplotlib seaborn scikit-learn xgboost lightgbm imbalanced-learn mlxtend jupyter

# 4. Launch Jupyter and open any topic folder
jupyter notebook
```

---

## Typical Workflow Used in Every Topic

1. **Problem understanding**: what are we predicting or discovering?
2. **Data loading and exploration (EDA)**: shape, types, distributions, correlations
3. **Preprocessing**: handle missing values and outliers, encode, scale
4. **Feature engineering / selection**
5. **Model building**: train the algorithm
6. **Validation**: cross-validation, appropriate metrics
7. **Tuning**: GridSearchCV / RandomizedSearchCV
8. **Interpretation**: feature importance, plots, business meaning

---

## Key Learnings

- No single algorithm wins everywhere. Choose based on data size, feature types and interpretability needs.
- Good preprocessing and feature engineering often matter more than switching algorithms.
- Accuracy alone misleads on imbalanced data, so use precision, recall, F1 and ROC-AUC.
- Always validate with cross-validation to catch overfitting early.
- Boosting methods (XGBoost, LightGBM) are strong on tabular data but need careful tuning.
- Unsupervised methods need domain judgement, since there is no single correct answer.

---

## Related Repositories

- [Deep Learning Study](https://github.com/Tamilarsan123/Deep_Learning_Study): the next step, neural networks, CNNs and real-time classification

---

## Author

**Tamilarasan K**
B.Tech, Artificial Intelligence & Data Science

- GitHub: [Tamilarsan123](https://github.com/Tamilarsan123)
- LinkedIn: [tamilarasan-k](https://linkedin.com/in/tamilarasan-k-03a27834b)

If this repository helped you, consider giving it a star.

# PCA – Dimensionality Reduction Technique

A hands-on notebook exploring **Principal Component Analysis (PCA)** — how it works, how it visually projects data into lower dimensions, and how it affects model performance on a real classification task (Breast Cancer Wisconsin dataset).

## Overview

This project demonstrates:

1. **Intuition for PCA** — a 2D → 1D toy visualization showing how points get projected onto the principal component (PC1) direction.
2. **Baseline model** — a Decision Tree Classifier trained on the *full* 30-feature breast cancer dataset.
3. **PCA-reduced model** — the same classifier trained after reducing the data to 2 principal components (X1, X2), to compare accuracy and see the trade-off between dimensionality and performance.
4. **Visualizations** — 2D scatter plot of the transformed components, and a 1D projection onto PC1.
5. **When PCA works** — a look at feature correlation to illustrate why PCA is effective on highly correlated features.

## Dataset

- **Source**: `sklearn.datasets.load_breast_cancer` (built into scikit-learn, no external download needed)
- **Samples**: 569
- **Features**: 30 numeric features (e.g., mean radius, mean texture, mean perimeter, etc.)
- **Target**: Binary — benign (1) vs malignant (0)

## Workflow

| Step | Description |
|------|-------------|
| 1. Import libraries | numpy, pandas, matplotlib, scikit-learn |
| 2. Load data | Load and frame the breast cancer dataset as a DataFrame |
| 3. Baseline model | Train/test split (80/20, stratified) → Decision Tree on all 30 features |
| 4. Evaluate baseline | Accuracy + confusion matrix on train and test sets |
| 5. Apply PCA | Standardize features (`StandardScaler`) → reduce to 2 principal components |
| 6. Retrain on PCA features | Same Decision Tree, same split, trained on the 2 components instead |
| 7. Evaluate PCA model | Accuracy + confusion matrix on train and test sets |
| 8. Visualize | 2D scatter of X1 vs X2; 1D projection onto PC1 |
| 9. Correlation check | Inspect feature correlation to show why PCA works well here |

## Results

| Model | Features Used | Train Accuracy | Test Accuracy |
|-------|---------------|-----------------|-----------------|
| Decision Tree (baseline) | 30 original features | 1.00 | 0.877 |
| Decision Tree (PCA) | 2 principal components | 1.00 | 0.868 |

**Explained variance**: PC1 and PC2 together capture ~63.2% of the total variance (PC1 ≈ 44.3%, PC2 ≈ 19.0%).

**Takeaway**: Reducing 30 features down to just 2 principal components retains almost the same test accuracy (~86.8% vs ~87.7%), showing PCA can dramatically cut dimensionality with minimal loss in predictive power — useful for visualization, speed, and reducing overfitting risk on correlated features.

## Requirements

```
numpy
pandas
matplotlib
scikit-learn
```

Install with:
```bash
pip install numpy pandas matplotlib scikit-learn
```

## How to Run

1. Install the dependencies above.
2. Open the notebook in Jupyter:
   ```bash
   jupyter notebook "PCA_-_Dimensionality_Reduction_Technique.ipynb"
   ```
3. Run all cells sequentially from top to bottom.

## Notebook Structure

- **Section 1**: 2D→1D PCA projection visualization (intuition builder)
- **Section 2**: Import libraries & data
- **Section 3**: Baseline Decision Tree model (all features)
- **Section 4**: Model evaluation (train/test accuracy, confusion matrix)
- **Section 5**: Apply PCA (standardization + 2-component reduction)
- **Section 6**: Retrain and evaluate Decision Tree on PCA-reduced data
- **Section 7**: Visualization of transformed features (2D and 1D)
- **Section 8**: Feature correlation check (why PCA works)

## Key Concepts Covered

- Standardizing data before PCA (critical since PCA is scale-sensitive)
- Principal components as directions of maximum variance
- Explained variance ratio and cumulative variance
- Trade-off between dimensionality reduction and model accuracy
- Why PCA is most effective on correlated features

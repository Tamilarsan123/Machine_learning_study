# Regularization Techniques in Linear Regression

A hands-on notebook comparing **Linear Regression**, **Ridge**, **Lasso**, and **ElasticNet** on the California Housing dataset — showing how each regularization technique affects model coefficients.

## Overview

This project demonstrates how L1 (Lasso), L2 (Ridge), and combined (ElasticNet) regularization impact linear regression coefficients compared to a plain linear model, using scikit-learn's California Housing dataset.

## Dataset

- **Source:** `sklearn.datasets.fetch_california_housing`
- **Samples:** 20,640
- **Features:** `MedInc`, `HouseAge`, `AveRooms`, `AveBedrms`, `Population`, `AveOccup`, `Latitude`, `Longitude`
- **Target:** Median house value (`Target`)

## Workflow

1. **Import Libraries** — pandas, scikit-learn (`LinearRegression`, `Ridge`, `Lasso`, `ElasticNet`), evaluation metrics
2. **Load Dataset** — fetch and inspect the California Housing data
3. **Train/Test Split** — split data using `train_test_split`
4. **Model Training** — fit all four models on the training set
5. **Prediction** — generate predictions on the test set
6. **Coefficient Comparison** — print and compare coefficients across models to observe the regularization effect (e.g., Lasso zeroing out weaker features)

## Requirements

```
pandas
scikit-learn
```

Install with:
```bash
pip install pandas scikit-learn
```

## Usage

```bash
jupyter notebook Regularization_Techniques_LinearRegression.ipynb
```

Run all cells in order to reproduce the model training and coefficient comparison.

## Key Takeaway

- **Linear Regression** uses all features with no penalty.
- **Ridge** shrinks coefficients but keeps all features.
- **Lasso** drives several coefficients to exactly zero — performing feature selection.
- **ElasticNet** blends L1 and L2, zeroing out some features while shrinking others.

## Author

**Tamilarasan K**
- GitHub: [@Tamilarasan123](https://github.com/Tamilarasan123)
- LinkedIn: [tamilarasan-k](https://linkedin.com/in/tamilarasan-k-03a27834b)

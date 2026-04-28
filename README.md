# 📊 Marketing ROI & Revenue Prediction Project

## Overview

This project explores the relationship between marketing spending, user engagement metrics, and revenue outcomes. The goal is to build predictive models that can:

* Forecast revenue (regression)
* Predict directional changes in revenue (classification)
* Identify which marketing channels and behaviors drive performance

While the project is still in progress, it demonstrates a full end-to-end machine learning workflow, including data preprocessing, feature engineering, model experimentation, and evaluation.

---

## 🎯 Objectives

* Understand how different marketing channels impact revenue
* Identify lag effects and delayed responses to spend
* Build models that can predict:

  * Whether revenue will increase (`target_up`)
  * Whether revenue will significantly increase (`target_big_up`)
* Evaluate tradeoffs between model accuracy and ranking ability (AUC)

---

## 📁 Data

The dataset consists of ~1,000 daily observations with features including:

* Marketing spend by channel:

  * Google Ads
  * Facebook Ads
  * Email Marketing
  * Influencer Spend
* Engagement metrics:

  * Organic traffic
  * Email sends
  * Site visits
  * Conversions
* Revenue (target variable)

---

## 🧪 Feature Engineering

A significant portion of the project focuses on extracting signal from relatively weak raw features.

### Key transformations:

#### 1. Log Transformations

* Applied to skewed spend variables to normalize distributions

#### 2. Lag Features

* Captures delayed effects of marketing spend (e.g., `lag1`, `lag3`, `lag7`)

#### 3. Rolling Statistics

* Moving averages (e.g., 7-day rolling mean)
* Momentum features (change over time)

#### 4. Interaction Terms

* Combines channels to capture joint effects
  (e.g., `google_ads * facebook_ads`)

#### 5. Derived Features

* Total spend
* Channel spend share
* Spend momentum and volatility

#### 6. Missing Data Strategy

* Median imputation initially used
* Iterated toward:

  * Zero imputation for spend-related features
  * Missing indicators for lagged variables

---

## 🤖 Models Explored

### Regression Models

* Linear Regression
* Feature selection via forward/backward selection
* Regularization (Ridge/Lasso considered)

👉 Result: Very low R² (< 0.05) across models
→ Indicates weak linear signal in raw revenue prediction

---

### Classification Models

#### Targets:

* `target_up`: binary indicator of revenue increase
* `target_big_up`: threshold-based large increase

#### Algorithms:

* Random Forest
* Gradient Boosting

#### Techniques:

* Time-based train/test split (no shuffling)
* Hyperparameter tuning:

  * `n_estimators`
  * `max_depth`
  * `min_samples_leaf`
* Threshold optimization (improves accuracy beyond default 0.5)

---

## 📈 Results Summary

| Model Type                      | Best AUC                                          | Best Accuracy |
| ------------------------------- | ------------------------------------------------- | ------------- |
| Random Forest (`target_up`)     | ~0.80                                             | ~0.70–0.75    |
| Gradient Boosting (`target_up`) | ~0.78                                             | ~0.70         |
| `target_big_up`                 | Lower AUC, higher accuracy due to class imbalance |               |

### Key Observations:

* Revenue is difficult to predict directly (low regression performance)
* Directional prediction is more feasible than exact forecasting
* Feature importance is diffuse (many weak predictors rather than a few strong ones)
* Threshold tuning significantly improves classification performance
* Class imbalance strongly affects accuracy vs AUC tradeoffs

---

## ⚠️ Challenges & Limitations

* **Weak signal-to-noise ratio** in features
* **Limited dataset size (~1000 rows)** restricts model complexity
* **Target definition sensitivity** (small changes in definition affect performance significantly)

---

## 🔍 Key Learnings

* Feature engineering is more impactful than model choice in this problem
* Tree-based models outperform linear models for this dataset
* Missing data handling strategy can materially impact model performance
* Time series structure must be respected (no random splits)
* AUC is often a more reliable metric than accuracy for imbalanced targets

---

## 🚀 Next Steps

This project is ongoing. Planned improvements include:

* More advanced feature engineering:

  * Relative changes (percent change, acceleration)
  * Cross-channel lag interactions
  * Volatility and trend features
* Improved target construction:

  * Smoothed revenue signals
  * Multi-class classification
* Feature selection refinement:

  * Automated pruning of low-importance features
* Model expansion:

  * XGBoost / LightGBM
  * Time-series specific models
* Validation improvements:

  * Walk-forward validation

---

## 💡 Takeaway

This project highlights a realistic machine learning scenario:

> Clean data and strong models do not guarantee strong predictive power.

Instead, success depends on:

* Understanding the data generating process
* Iterating on feature design
* Choosing appropriate evaluation metrics

---

## 👤 About

This project was built as part of a broader effort to develop practical, end-to-end machine learning skills, with a focus on real-world ambiguity, iteration, and model evaluation.

---

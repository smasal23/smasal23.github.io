---
layout: page
title: Diamond Dynamics Price & Market Predictor
description: ML pipeline for predicting diamond prices and identifying market tiers.
img: assets/img/projects/diamond/streamlit_home.png
importance: 1
category: Machine Learning & AI
---

**[View Source Code on GitHub](https://github.com/smasal23/projects/tree/547e3a5f08a3cd15e9b222b894328834ce784be2/Diamond%20Dynamics%20Price%20Prediction%20and%20Market%20Segmentation)**

## 1. Problem Statement & Real-World Applicability

Diamond valuation is notoriously complex. Small variations in carat, clarity, cut quality, or physical dimensions trigger non-linear, interacting impacts on market value. Consequently, manual price estimation is subjective, inconsistent, and difficult to scale.

**Business Impact:**
This project solves two critical business needs for retail merchants and pricing analysts:

1. **Automated Valuation:** A predictive regression system to generate accurate, data-driven price estimates.
2. **Product Segmentation:** An unsupervised clustering engine to group inventory into interpretable product tiers (e.g., premium, budget, quality-focused) for stock positioning and pricing strategy.

---

## 2. Dataset Profile

- **Source:** Historical diamond market dataset.
- **Size:** ~53,940 records.
- **Target Variable:** `price` (Continuous, right-skewed).
- **Predictor Variables:**
  - *Numeric:* `carat`, `depth`, `table`, `x` (length), `y` (width), `z` (depth).
  - *Categorical (Ordinal):* `cut`, `color`, `clarity`.

---

## 3. Tech Stack & Architecture

This repository was architected as a modular, production-ready system rather than a standard Jupyter Notebook experiment.

- **Languages & Core:** `Python`, `Pandas`, `NumPy`
- **Machine Learning:** `Scikit-Learn`, `XGBoost`, `Random Forest`, `PyTorch`, `Dimensionality Reduction`
- **Ops & Deployment:** `Streamlit`, `Joblib`, `PyYAML`, `Pytest`
- **Architecture:** Config-driven parameters (`configs/`), reusable modules (`src/data/`, `src/features/`, `src/modeling/`), and an isolated inference layer.

---

## 4. Engineering Workflow

### A. Exploratory Data Analysis (EDA) & Cleaning

- **Handling Impossible Data:** Detected and neutralized invalid geometry (e.g., physical dimensions `x`, `y`, `z` reported as zero) by marking them as missing and imputing via median strategies to preserve dataset integrity.
- **Distribution Handling:** Analyzed the heavy right-skew of the target variable, setting up `log1p(price)` transformations in the training pipeline to stabilize gradients.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/diamond/correlation_heatmap.png" title="Correlation Heatmap" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 1: Correlation heatmap revealing strong multicollinearity between physical dimensions and carat weight.
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/diamond/pairplot.png" title="Pairplot" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 2: Pairwise relationships highlighting the non-linear scaling of price against physical size parameters.
</div>

### B. Feature Engineering & Selection

- **Derived Metrics:** Engineered domain-specific features including `volume_proxy`, `length_width_ratio`, and `table_depth_interaction`.
- **Addressing Multicollinearity:** Evaluated VIF (Variance Inflation Factor) to manage the high correlation between raw dimensions and engineered volume.
- **Encoding Strategies:** Applied One-Hot Encoding for the regression branch, but switched to Ordinal Encoding + Scaling for the clustering branch to preserve the ordinal logic of quality grades.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/diamond/feature_importance.png" title="Feature Importance" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 3: Feature Importance breakdown showing 'Y' dimension and Volume Proxy as dominant price drivers.
</div>

---

## 5. Algorithms Used & Modeling

### Supervised Learning (Regression)

I trained and evaluated multiple model families to capture the non-linear pricing relationships: Linear Regression, Decision Trees, KNN, Random Forest, XGBoost, and a custom PyTorch Artificial Neural Network (ANN).

- **Selection:** `XGBoost` was selected as the final production model due to its superior handling of interacting categorical combinations and outlier resilience.

### Unsupervised Learning (Clustering)

Evaluated KMeans, Agglomerative Clustering, and DBSCAN using Silhouette Scores, Davies-Bouldin metrics, and Elbow Methods.

- **Selection:** `DBSCAN` proved highly effective at isolating dense market bands while rejecting outlier noise, allowing for the mapping of distinct commercial segments.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/diamond/pca_clusters.png" title="PCA Clusters" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 4: 3D PCA projection of the DBSCAN market segmentation.
</div>

---

## 6. Evaluation Metrics

The production XGBoost model achieved exceptional predictive accuracy across the test set:

- **R² Score: 0.981** — Explains 98.1% of the variance in market pricing.
- **RMSE: $542.38** — Average prediction error margin is competitive.
- **MAE: $274.76** — Median absolute error shows strong reliability.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/diamond/actual_vs_predicted.png" title="Actual vs Predicted" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 5: Actual vs. Predicted Price distribution showing strong linear adherence on the XGBoost model.
</div>

---

## 7. Deployment & Inference

To prove real-world applicability, I built an isolated inference API (`src/inference/`) that connects to a **Streamlit Web Dashboard**.

The app validates user input, dynamically computes the engineered features, and feeds the data through the saved artifact pipelines to instantly output:

1. Estimated Price (USD & INR conversions)
2. Identified Market Segment Cluster

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/projects/diamond/streamlit_home.png" title="Streamlit Deployment" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Figure 6: The interactive Streamlit Dashboard running live inference.
</div>

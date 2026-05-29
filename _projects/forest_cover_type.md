---
layout: page
title: Forest Cover Type Prediction
description: An end-to-end machine learning pipeline utilizing SMOTE and tuned ensemble models to classify forest cover from imbalanced geospatial data.
img: assets/img/projects/forest/Cover.jpg
importance: 2
category: Machine Learning & AI
---

### Real-World Problem
Understanding and predicting forest cover types across vast geographic areas is essential for ecological monitoring, resource management, and conservation planning. Traditional ground-survey methods are expensive and time-consuming. This project develops an automated, supervised machine learning pipeline to accurately classify 7 distinct forest cover types based solely on cartographic, topographic, and soil-derived geospatial data.

### Dataset
* **Source:** The standard Covertype Data Set (via UCI Machine Learning Repository / Kaggle).
* **Features:** Continuous geographic features (elevation, slope, horizontal/vertical distance to hydrology, roadways, and fire points) and binary indicators (wilderness areas, soil types).
* **Target:** 7 distinct forest cover classes (Lodgepole Pine, Spruce/Fir, Aspen, Cottonwood/Willow, Douglas-fir, Krummholz, Ponderosa Pine).
* **Challenges:** The dataset exhibits extreme class imbalance. Lodgepole Pine and Spruce/Fir dominate the sample space, while minority classes like Cottonwood/Willow are exceptionally scarce, threatening model bias.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/forest/class_distribution_bar.png" title="Class Distribution" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">Visualizing the severe class imbalance across the 7 forest cover types in the raw dataset.</div>

### Tech Stack
* **Data Engineering & ML:** Python (Scikit-learn, Pandas, NumPy, Imbalanced-learn)
* **Analysis & Visualization:** Matplotlib, Seaborn
* **Deployment:** Streamlit, Joblib (Model persistence)
* **Architecture:** Config-driven pipeline architecture (`.yaml` configurations) built for strictly reproducible runs.

### Engineering Workflow
1. **Data Ingestion & Validation:** Built configurable scripts to ingest raw data and run automated schema validation checks.
2. **Exploratory Data Analysis (EDA):** Analyzed feature distributions, extracted feature correlations, and mapped out preprocessing requirements.
3. **Preprocessing Pipeline:** Constructed a robust `ColumnTransformer` (scaling continuous numeric features while safely passing through binary indicators) wrapped natively into an `sklearn` Pipeline.
4. **Handling Class Imbalance:** To prevent bias toward the majority classes, **SMOTE** (Synthetic Minority Over-sampling Technique) was implemented. Crucially, SMOTE was embedded *strictly inside* the cross-validation pipeline to synthesize minority samples only on training folds, entirely eliminating data leakage into the validation sets.
5. **Baseline Modeling:** Benchmarked multiple classifiers. Ensembles (Random Forest and Extra Trees) significantly outperformed linear and boosting baseline models, establishing strong starting macro F1 metrics.
6. **Hyperparameter Tuning:** Conducted extensive grid/random search tuning on the top ensemble models.
7. **Deployment:** Packaged the end-to-end logic into a Streamlit web application.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/forest/correlation_heatmap.png" title="Feature Correlation Heatmap" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">Correlation heatmap used during the EDA phase to identify predictive cartographic features and multicollinearity.</div>

### Algorithms/Architecture
* **Baseline Selection:** Both Random Forest and Extra Trees proved highly resilient to the non-linear, multi-class nature of the topographic dataset. 
* **Tuning Strategy:** Hyperparameter tuning was explicitly optimized for **Macro F1** rather than pure accuracy. This penalized the models for neglecting minority classes, forcing a balanced learning approach across all 7 cover types.
* **Final Tuned Architecture:** A Random Forest classifier (optimized with `n_estimators=100`, `min_samples_split=2`, `max_features='sqrt'`, `max_depth=None`) was selected as the final model due to its high stability and peak test metrics.

### Metrics
* **Primary Metric (Macro F1):** Achieved a remarkable 0.9152 on the holdout test set, confirming that minority classes were successfully learned and preserved.
* **Overall Accuracy:** 95.94% total correctness across the unseen test data.
* **Weighted F1-Score:** 0.9590.
* **Minority Class Recall:** The SMOTE + Random Forest pipeline achieved exceptional recall on scarce classes (e.g., 95.3% for Cottonwood/Willow and 96.5% for Krummholz).
* **Generalization Check:** The test Macro F1 (0.9152) slightly exceeded the cross-validation Macro F1 (0.8949), indicating a highly robust, generalized model with zero overfitting.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/forest/random_forest_confusion_matrix.png" title="Final Confusion Matrix" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">Confusion matrix for the final tuned Random Forest model evaluating test set performance across all 7 classes.</div>

### Deployment/Inference
The final preprocessing rules, SMOTE transformations, and the tuned Random Forest classifier were serialized together as a single `joblib` artifact. This ensures that any incoming inference requests follow the exact same deterministic scaling and routing as the training environment. The model is actively served via an interactive **Streamlit** application, allowing users to input raw topographical values and receive instant, highly accurate forest cover predictions.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/forest/App_1.png" title="Streamlit Inference App" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">The Streamlit deployment interface allowing users to query the serialized pipeline for real-time ecological predictions.</div>

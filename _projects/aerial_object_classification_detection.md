---
layout: page
title: Aerial Object Classification & Detection
description: An end-to-end deep learning pipeline for classifying and detecting birds and drones in aerial imagery.
img: assets/img/projects/aerial/Detection_Overview.png
importance: 2
category: Computer Vision & Robotics
---

**[View Source Code on GitHub](https://github.com/smasal23/projects/tree/547e3a5f08a3cd15e9b222b894328834ce784be2/Aerial%20Object%20Classification%20%26%20Detection)**

### Real-World Problem
Birds and drones can visually resemble one another in long-range or aerial imagery. This visual ambiguity creates significant challenges for modern surveillance systems, airspace safety monitoring, and automated visual perception systems. This project aims to accurately disambiguate and locate these entities to enhance security and airspace management.

### Dataset
* **Classification:** Binary image dataset differentiating between Bird and Drone classes.
* **Detection:** Images annotated with bounding boxes in YOLO format.
* **Structure:** Data is systematically divided into Train, Validation, and Test splits.
* **Challenges:** Addressed data limitations related to small dataset size and high visual similarity between the two classes.

### Tech Stack
* **Deep Learning:** Custom CNNs, Transfer Learning (MobileNetV2, EfficientNetB0, ResNet50)
* **Object Detection:** Ultralytics YOLOv8
* **Deployment:** Streamlit
* **Environment:** Google Colab with Google Drive persistence for a modular, reproducible CV pipeline.

### Engineering Workflow
1. **Dataset Audit:** Initial data exploration and integrity checks.
2. **Data Cleaning & Preprocessing:** Formatting images, handling augmentations, and establishing the pipeline.
3. **Custom CNN Training:** Training a baseline classification network from scratch.
4. **Transfer Learning:** Implementing and fine-tuning pre-trained deep learning architectures.
5. **Model Evaluation & Selection:** Comparing model performance metrics to select the best classifier.
6. **Detection Training:** Training YOLOv8 for precise bounding-box detection.
7. **Deployment:** Wrapping the final inference logic into a user-friendly application.

### Algorithms & Architecture
* **Custom CNN Baseline:** Built from scratch to establish a clear, explainable baseline. The architecture consists of 4 convolution blocks. Each block applies a sequence of two `Conv2D` layers (utilizing L2 regularization, Batch Normalization, and ReLU activations), followed by `MaxPooling2D` and `Dropout`. The network concludes with a `GlobalAveragePooling2D` layer, a fully connected `Dense` feature layer with Dropout, and a final `Dense` classifier head with a sigmoid activation for binary output.
* **Transfer Learning:** Explored MobileNetV2, EfficientNetB0, and ResNet50 to extract robust features and improve classification accuracy.
* **Object Detection:** Utilized Ultralytics YOLOv8 to perform fast, single-stage bounding box regression.

### Training & Model Development
Training the custom baseline CNN provided a solid foundation, achieving a respectable test accuracy. During training, we utilized robust data augmentations—including rotations, horizontal flips, zoom, brightness variations, and spatial shifts—to improve the model's resilience to orientation and lighting changes. We subsequently applied transfer learning, training much deeper architectures to compare against the baseline.

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/aerial/custom_cnn_accuracy.png" title="Custom CNN Training Accuracy" class="img-fluid rounded z-depth-1" %}</div><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/aerial/resnet50_accuracy.png" title="ResNet50 Training Accuracy" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">Training and validation accuracy curves for the baseline Custom CNN alongside the final selected ResNet50 transfer learning model.</div>

### Evaluation Metrics & Selection
We evaluated the models on a held-out test set to determine generalization capabilities. Among the transfer learning options, **EfficientNetB0** demonstrated the best balance of efficiency, manageable model size, and accuracy (97.21%) during initial comparisons. However, after full test-set evaluation, **ResNet50** was ultimately selected as the final classifier due to its superior raw accuracy and perfect precision (zero false positives).

**Classification Metrics:**
* **Custom CNN (Baseline):** Accuracy: 82.79% | Precision: 82.76% | Recall: 76.60% | F1-Score: 79.56%
* **EfficientNetB0 (Best Transfer Balance):** Accuracy: 97.21% | Precision: 97.83% | Recall: 95.74% | F1-Score: 96.77%
* **ResNet50 (Final Selection):** Accuracy: 98.60% | Precision: 100.00% | Recall: 96.81% | F1-Score: 98.38%

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/aerial/model_comparison_barplot.png" title="Model Comparison" class="img-fluid rounded z-depth-1" %}</div><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/aerial/resnet50_confusion_matrix.png" title="ResNet50 Confusion Matrix" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">Performance comparison across all tested models and the confusion matrix for the final ResNet50 model showing zero false positives.</div>

### Detection Performance
For the detection pipeline, we trained a YOLOv8 network over 25 epochs to localize birds and drones. The final model handles variations in object scale, sky clutter, and background ambiguity effectively, generating tight bounding boxes around targets.

**Detection Metrics (YOLOv8):**
* **Precision:** 85.64%
* **Recall:** 79.21%
* **mAP@50:** 82.16%
* **mAP@50-95:** 53.54%

<div class="row"><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/aerial/yolo_val_preview.png" title="YOLO Validation Preview" class="img-fluid rounded z-depth-1" %}</div><div class="col-sm mt-3 mt-md-0">{% include figure.liquid loading="eager" path="assets/img/projects/aerial/yolo_test_predictions.png" title="YOLO Test Predictions" class="img-fluid rounded z-depth-1" %}</div></div><div class="caption">YOLOv8 detection results displaying localized bounding boxes and class confidence scores on validation and test datasets.</div>

### Deployment/Inference
The final machine learning pipeline is deployed via an interactive **Streamlit** web application. This allows users to upload new aerial imagery and instantly receive classification results from the ResNet50 model alongside YOLOv8 bounding-box detections. Future iterations aim to expand the underlying dataset and push the application toward real-time edge deployment.

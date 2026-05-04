<h1 align="center">Malaysian Food Image Classifier 🍛</h1>

<p align="center">
  <strong>A Deep Learning project comparing a Custom CNN and a fine-tuned ResNet-50 for recognizing popular Malaysian cuisine.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-blue.svg" alt="Python">
  <img src="https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?logo=PyTorch&logoColor=white" alt="PyTorch">
  <img src="https://img.shields.io/badge/Jupyter-F37626.svg?logo=Jupyter&logoColor=white" alt="Jupyter">
</p>

## 📖 Table of Contents
- [About the Project](#about-the-project)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Results & Performance](#results--performance)
- [Business Applications](#business-applications)
- [Author](#author)

---

## 🚀 About the Project

This repository contains the implementation of an image classification pipeline designed to identify 5 popular Malaysian dishes. It was developed as part of the WID3011 Deep Learning coursework. 

The project explores and compares two distinct architectural approaches:
1. **Custom CNN:** A 6-layer convolutional neural network (approx. 13.28M parameters) built from scratch utilizing a VGG-style pattern for fine-grained texture extraction.
2. **Transfer Learning (ResNet-50):** A pre-trained ResNet-50 model adapted via a two-stage fine-tuning strategy (head warm-up followed by end-to-end unfreezing).

## 📊 Dataset

The model is trained on a curated subset of the **IEEE DataPort MF-150 Multilabel Malaysian Foods Dataset** (Tahir & Loo, 2020). 

* **Classes (5):** Murtabak, Satay, Chicken Bak Kut Teh, Char Kuey Teow, and Hong Kong Wonton Noodles.
* **Size:** 979 total images.
* **Split:** Stratified 70% Training / 15% Validation / 15% Testing.
* **Imbalance Handling:** Class-weighted cross-entropy loss.

### 🔗 Data Sources

- **Original Dataset (IEEE DataPort):**  
  https://ieee-dataport.org/open-access/mf-150-multilabel-malaysian-foods-dataset  

- **Processed Dataset (used in this project):**  
  https://drive.google.com/drive/folders/1iKM2peSh0m8V5jHlJYXiMmRp0AwQkP9c

*Note: The dataset uses numeric folder IDs which are mapped to human-readable names via the included `foldernames.csv`.*

## 📂 Project Structure
```text
Malaysian-Food-CNN-Classifier/
│
├── notebook/
│   └── WID3011_Individual_Assignment.ipynb   # Main notebook (training, evaluation, visualization)
│
├── report/
│   └── Individual_Assignment_WID3011.pdf     # Full technical report
│
├── data/
│   └── processed/
│       ├── train.csv                         # Training split (70%)
│       ├── val.csv                           # Validation split (15%)
│       ├── test.csv                          # Testing split (15%)
│       └── meta.json                         # Dataset metadata
│
│
├── results/
│   ├── learning_curves.png
│   ├── confusion_matrix.png
│   ├── confusion_matrix_custom.png
│   ├── confusion_matrix_resnet.png
│   ├── confusion_matrix_comparison.png
│   └── misclassified_samples.png
│
├── foldernames.csv                           # Class ID → label mapping
├── .gitignore
└── README.md
```

## Model Architectures

### 1. Custom CNN
* **Structure:** A 5-stage convolutional neural network containing 6 convolutional layers built from scratch[cite: 1].
* **Parameters:** Approximately 13.28 million parameters[cite: 1].
* **Design:** Utilizes a VGG-style pattern for the first two stages (two $3\times3$ convolutions) to capture fine-grained textures, followed by single convolutions in deeper layers, max pooling, and dropout (0.5) for regularization[cite: 1].

### 2. ResNet-50 (Transfer Learning)
* **Structure:** A pre-trained ResNet-50 model adapted via a 2-stage training strategy[cite: 1].
* **Training:** Stage 1 involves a head warm-up with a frozen backbone (learning rate of $1\times10^{-3}$), while Stage 2 unfreezes all layers for full end-to-end fine-tuning (learning rate of $1\times10^{-4}$)[cite: 1].

## Results & Performance

Both models were evaluated on an unseen testing set of 147 images[cite: 1]. The fine-tuned ResNet-50 significantly outperformed the custom CNN in both accuracy and convergence speed[cite: 1].

| Metric | Custom CNN | ResNet-50 |
| :--- | :--- | :--- |
| **Total Parameters** | 13,281,765 | 23,518,277 |
| **Best Validation Accuracy** | 93.20% | 100.00% |
| **Test Accuracy** | 92.52% | 99.32% |
| **Total Training Time** | 380.3s | 265.2s |
| **Epochs Trained** | 46 (Early Stopping) | 28 |

*(Note: Ensure you have pushed the image files below to your repository for them to render correctly)*

### Learning Curves
![Learning Curves](learning_curves.png)

### Model Evaluation & Misclassification
The ResNet-50 model generalized exceptionally well, registering only 1 misclassification (Chicken Bak Kut Teh predicted as Char Kuey Teow)[cite: 1]. The Custom CNN produced 11 misclassifications, struggling primarily with bidirectional confusion between visually similar dishes like Hong Kong Wonton Noodles and Char Kuey Teow[cite: 1].

## Business Application Potential
This classification model holds practical value for Malaysian Small and Medium Enterprises (SMEs)[cite: 1]:
* **Auto-tagging for Delivery Apps:** Helping home-based businesses automatically categorize dishes uploaded to GrabFood or Foodpanda[cite: 1].
* **Snap-and-Order Kiosks:** Assisting tourists in identifying unfamiliar dishes and overcoming language barriers in food courts[cite: 1].
* **Calorie Tracking:** Pairing the classifier with the Malaysian Food Composition Database (MyFCD) to provide health app users with accurate nutritional estimations[cite: 1].
# Anatomically Guided Self-Supervised Representation Learning for Carotid Ultrasound

A self-supervised deep learning framework for learning meaningful feature representations from carotid ultrasound images using anatomically guided concentric ring extraction and contrastive learning.

---

## Overview

Carotid artery ultrasound is a widely used, non-invasive imaging modality for assessing vascular health and detecting atherosclerotic disease. Conventional deep learning approaches typically require extensive expert annotations, making them expensive and difficult to scale.

This project investigates whether meaningful ultrasound representations can be learned **without plaque labels** by combining anatomical domain knowledge with **self-supervised contrastive learning (SimCLR)**.

Rather than processing the complete ultrasound image, the proposed pipeline focuses on anatomically meaningful concentric regions derived from the carotid lumen. These regions are used to learn feature embeddings capable of capturing subtle variations in ultrasound texture through self-supervised learning.

---

## Motivation

The blood-filled carotid lumen typically appears largely **anechoic**, whereas ultrasound echo characteristics gradually change closer to the vessel wall.

The motivation behind this work was to investigate whether these spatial variations could be captured through learned feature representations.

To explore this idea, three concentric rings were extracted from the lumen using expert-annotated segmentation masks. The hypothesis was that differences in learned feature similarity between these concentric regions may reflect underlying structural changes and could serve as a useful exploratory representation for future plaque analysis.

> **Note:** This project investigates self-supervised representation learning and embedding similarity analysis. It does **not** claim to diagnose plaque or establish a clinically validated biomarker.

---

## Dataset

The project uses:

- 1100 grayscale carotid ultrasound B-mode images
- Corresponding expert-annotated lumen segmentation masks

The segmentation masks are used solely for anatomical preprocessing and concentric ring extraction.

The dataset is **not included** in this repository due to sharing restrictions.

---

## Methodology

### 1. Data Exploration

- Image visualization
- Mask verification
- Intensity distribution analysis
- Dataset quality inspection

---

### 2. Anatomically Guided Ring Extraction

Instead of processing the entire ultrasound image, the preprocessing pipeline focuses on the carotid lumen.

Using the expert lumen segmentation masks:

- Three concentric rings are generated within the lumen
- Ring regions are extracted
- Intensity normalization is performed
- Processed ring images are generated for representation learning

This anatomically motivated preprocessing reduces background variability while enabling investigation of texture differences across concentric regions.

---

### 3. Self-Supervised Representation Learning

Representation learning is performed using the SimCLR framework.

The model consists of:

- Modified ResNet18 encoder
- Single-channel grayscale input
- Contrastive learning objective
- Projection head
- Data augmentation pipeline

No plaque labels are used during training.

---

### 4. Embedding Similarity Analysis

The learned feature representations are evaluated using:

- Nearest-neighbour retrieval
- Top vs Bottom similarity comparisons
- Similarity score distributions
- Embedding-space visualization
- Statistical comparison of embeddings

These analyses provide insight into how well the learned representations organize anatomically related ultrasound regions.

---

## Project Pipeline

```text
Raw Ultrasound Images
            │
            ▼
 Expert Lumen Masks
            │
            ▼
 Three Concentric Ring Extraction
            │
            ▼
 Intensity Normalization
            │
            ▼
   SimCLR Representation Learning
            │
            ▼
      Feature Embeddings
            │
            ▼
 Similarity & Embedding Analysis
```

---

## Repository Structure

```text
carotid_project/
│
├── notebooks/
│   ├── 01_view_data.ipynb
│   ├── 02_data_preprocessing.ipynb
│   └── 03_representation_learning.ipynb
│
├── results/
│   ├── top_vs_bottom.png
│   ├── top10_grid.png
│   ├── score_distribution.png
│   ├── embedding_analysis.png
│   ├── statistical_comparison.png
│   └── anomaly_results.csv
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## Technologies Used

- Python
- PyTorch
- Torchvision
- OpenCV
- NumPy
- Matplotlib
- Pandas
- Scikit-learn
- Jupyter Notebook

---

## Results

The repository includes qualitative and quantitative evaluation of the learned representations through:

- Top vs Bottom similarity visualization
- Nearest-neighbour retrieval
- Similarity score distributions
- Embedding-space analysis
- Statistical comparison of learned embeddings

The results demonstrate that self-supervised contrastive learning can organize carotid ultrasound images into meaningful feature representations without requiring plaque annotations.

---

## Future Work

Potential future directions include:

- Downstream plaque classification using learned embeddings
- Vision Transformer (ViT) based representation learning
- Multi-scale anatomical feature extraction
- Integration with clinical metadata
- Validation on larger multi-center carotid ultrasound datasets

---

## Disclaimer

This repository is intended solely for research and educational purposes.

The proposed methodology is an exploratory self-supervised learning framework and **is not intended for clinical diagnosis or medical decision making.**

---

## Author

**Nandan Bhat**

Biomedical Engineering • Medical Imaging • Healthcare AI • Self-Supervised Learning
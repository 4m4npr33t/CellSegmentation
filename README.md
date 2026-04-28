# Cell Instance Segmentation with Pathology Foundation Models

## Overview
This notebook implements cell instance segmentation on the BCCD dataset using a pathology foundation model (Hibou-B) and compares it with a CNN-based baseline (ResNet50).

The workflow includes:
- Patch-based training
- Cross-validation for hyperparameter tuning
- Full-image inference using sliding window aggregation
- Evaluation using Dice, IoU, and Average Precision
- Visualization of best and worst predictions

---

## Models

### 1. Hibou-B (Foundation Model)
- Pretrained Vision Transformer for computational pathology
- Encoder kept frozen during training
- Custom segmentation decoder added

### 2. ResNet50 Baseline
- Pretrained ResNet50 encoder
- Lightweight decoder for segmentation
- Used as a baseline for comparison

---

## Dataset
- BCCD Dataset with Masks
- Blood cell microscopy images
- Pixel-level segmentation masks

---

## Methodology

### Data Processing
- Patch-based training (224×224)
- Random cropping
- Sliding window inference for full images

### Training Strategy
- 5-fold cross-validation
- Learning rate tuning: [1e-2, 1e-3, 1e-4]
- Loss function:
  - BCE + Dice Loss

### Augmentations
- Random cropping
- Optional stain normalization (Reinhard)
- Standard augmentation pipeline

---

## Evaluation

### Metrics
- Dice Score
- Intersection over Union (IoU)
- Average Precision (AP)

### Inference
- Full-image prediction using sliding window aggregation

---

## Results and Analysis
- Compared Hibou-B vs ResNet50 performance
- Observations:
  - Foundation model captures stronger features
  - Errors in overlapping cell regions
  - Boundary inconsistencies from patch-based inference

### Visualization
- Best predictions
- Worst predictions
- Overlays of:
  - Original image
  - Ground truth
  - Predicted mask

---

## Key Components
- Patch-based dataset classes for training and testing
- Training and validation loops
- Sliding window inference function
- Metric computation (Dice, IoU, AP)
- Visualization utilities

---

## Tech Stack
- Python
- PyTorch
- HuggingFace Transformers
- OpenCV / PIL
- NumPy / Matplotlib
- scikit-image

---

## Future Improvements
- Fine-tune the backbone instead of freezing
- Use instance-aware architectures (Mask R-CNN, DETR)
- Improve segmentation of overlapping cells
- Train on larger pathology datasets

# RSSI-Based Cell Localization with HMM Smoothing

## Overview

This project implements a Received Signal Strength Indicator (RSSI) based cell (zone) localization system using a two-stage approach:

1. **Machine Learning Classifier**  
   - Trains a Support Vector Machine (SVM) to predict the current cell/zone based on RSSI readings from multiple sensors.
2. **Hidden Markov Model (HMM) Smoothing**  
   - Applies a forward‐filtering HMM to the classifier’s sequence of predictions, leveraging transition and emission probabilities to reduce spurious jumps and improve temporal consistency.

By combining the discriminative power of SVMs with the temporal modeling capabilities of HMMs, this pipeline achieves higher localization accuracy on time‐series RSSI data.

---

## Dataset

The dataset consists of multiple CSV files (one per trial/room layout), each containing:

- **Sensor RSSI Columns**  
  - `O-DR`, `O-DL`, `O-E`, `O-M`, `I-DL`, `I-DR`, `I-E`, `I-T1`, `I-T2`, `I-T3`  
  - Readings from ten different sensors (external/internal)  
- **Label Column**  
  - `Cell` (integer codes 0, 1, 2 corresponding to distinct zones)

### Preprocessing

- Missing RSSI values coded as `-100` are forward‐filled and backward‐filled.
- Dataset files are merged into `combined.csv` for convenience.
- Features are standardized using `StandardScaler`.

---

## Results

- **Raw SVM Test Accuracy**: 0.9295  
- **Accuracy After Median Filtering**: 0.9471  
- **Accuracy After HMM Smoothing**: 0.9426  

> *Median filtering gives a quick one‐step smoothing boost, and the full HMM smoothing further enforces temporal consistency for strong overall performance.*

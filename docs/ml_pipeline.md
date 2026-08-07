# Machine Learning Pipeline

## Overview
Complete pipeline from raw sensor data to trained classifier, 
implemented in `notebooks/shm0.ipynb`.

## Pipeline Stages

### 1. Data Loading
Combined 4 CSV files (empty_normal, empty_cracked, 
flowing_normal, flowing_cracked) into single dataset — 1029 samples.

### 2. SNR Calculation (Before Preprocessing)
Signal-to-noise ratio computed per class to assess raw signal quality.

### 3. Data Cleaning
Removed outlier readings outside valid frequency (10kHz-490kHz) 
and amplitude (0-5) ranges.

### 4. Stratified Train/Val/Test Split (80/10/10)
Split before any synthetic data generation to keep validation 
and test sets fully real — prevents data leakage.

### 5. Feature Scaling
StandardScaler fit only on training data, applied to val/test 
using training statistics.

### 6. Feature Engineering
Derived 9-10 features from raw frequency and amplitude:
- freq_deviation, freq_normalized
- amp_mean, amp_std (rolling window, per-class)
- amp_ratio, amp_diff, amp_cv
- snr_db
- rms,kutrosis

`amp_cv` (coefficient of variation) proved most important — 
captures crack-induced signal instability independent of 
water pressure level.

### 7. SMOTE Balancing (Training Set Only)
Class imbalance (202–329 samples/class) balanced via SMOTE, 
generating synthetic samples only within the training set. 
balanced to 264 (all classes)
Validation and test sets remain 100% real data.

### 8. Model Training
Three models trained and compared:
- Random Forest
- XGBoost  
- PyTorch Neural Network (32-16-16, dropout 0.4, lr=0.002)

### 9. Evaluation
Models evaluated on held-out real test data using accuracy, 
classification report, and confusion matrix.

## Why This Order Matters
SMOTE and scaling were deliberately applied *after* the 
train/test split to avoid data leakage — a common mistake 
that inflates reported accuracy artificially.

See `notebooks/shm0.ipynb` for full implementation.

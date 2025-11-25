
# PhysioNet

This project focuses on developing machine learning models to extract time-series signals from Electrocardiogram (ECG) images as part of the PhysioNet Kaggle competition.
ECGs are foundational diagnostic tools in cardiology and exist in various formats—physical printouts, scanned copies, photographs, and digital signals. While clinical-grade ECG analysis tools are optimized for time-series data, a vast global archive of ECGs still exists only as images.

By building robust image-to-signal extraction models, this project aims to help bridge that gap. Converting ECG images into accurate time-series data can:

Unlock billions of historical ECG images for modern AI/ML analysis

Enable richer datasets for training diagnostic and prognostic models

Support better clinical decision-making and outcomes

This repository contains the end-to-end pipeline for experimenting with multiple models, cleaning data, training, evaluation, and generating predictions for the competition.


## Data Description

The goal of this competition is to reconstruct ECG time-series signals from ECG images, enabling modern digital ECG systems to process data originally produced by analogue or paper-based machines.

The dataset contains raw ECG signals, multiple image variations, and metadata describing sampling frequency, signal length, and lead information.

### 📘 Training Data
train.csv

Metadata for each training sample:

- id — Unique identifier for the ECG record
- fs — Sampling frequency of the signal
- sig_len — Length of the full time-series signal (always 10 seconds × fs for competition data)

Note: While competition data uses fixed 10-second durations, real clinical ECGs may vary. Robust code should account for variable lengths (not required for participation).
###
train/[id]/[id].csv

Raw time-series signal for 12 ECG leads, stored as a CSV file.
Columns include:

I, II, III, aVR, aVL, aVF, V1, V2, V3, V4, V5, V6
###
### 🖼️ ECG Image Variants

Each training sample contains multiple images representing different real-world acquisition conditions:
| File Name Pattern | Description                                             |
| ----------------- | ------------------------------------------------------- |
| `id-0001.png`     | Original color ECG generated digitally by ECG-image-kit |
| `id-0003.png`     | Printed in color → scanned in color                     |
| `id-0004.png`     | Printed in color → scanned in black & white             |
| `id-0005.png`     | Mobile photos of color-printed ECGs                     |
| `id-0006.png`     | Mobile photos of ECGs displayed on a laptop screen      |
| `id-0009.png`     | Mobile photos of stained/soaked printed ECGs            |
| `id-0010.png`     | Mobile photos of ECGs with extensive physical damage    |
| `id-0011.png`     | Scans of printed ECGs with mold (color)                 |
| `id-0012.png`     | Scans of printed ECGs with mold (black & white)         |

These variations ensure robustness against real-world noise, lighting issues, printing artifacts, and device differences.

### 🧪 Test Data
test.csv

Metadata for each test record:

- id — Unique test identifier
- lead — One of the 12 standard ECG leads
- fs — Sampling frequency
- number_of_rows — Required number of signal samples for prediction
###
test/[id].png

Each test sample contains one ECG image.
Around 1000 images are provided.
###


## Approach

1.  ***Sementic Segmentation***

The first step of the pipeline is semantic segmentation, where the goal is to identify and separate key components of the ECG image including the waveform traces, gridlines, text annotations, and background. This segmentation enables clean isolation of the ECG signal before converting it into time-series form.

For this task, we use a U-Net–based semantic segmentation model, chosen for its strong performance in medical imaging. U-Net’s encoder–decoder structure allows it to capture both high-level context and fine-grained details, making it well-suited for extracting ECG traces from noisy, scanned, or distorted images.

We explored multiple variations, but found that having a diverse training set mattered more than the specific architecture, so U-Net was retained as the primary segmentation model.
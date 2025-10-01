---
title: Autoencoder Anomaly Detection
permalink: /anomaly-detection/autoencoder/
parent: Anomaly Detection
nav_order: 2
---

## Overview

This report documents a reconstruction-based anomaly detector trained on regularly sampled InSAR time series. The intuition is that an autoencoder trained on nominal behaviour will struggle to reconstruct anomalous trajectories, producing large residuals that can be thresholded.

## Data Preparation

- **Input representation:** RANSAC regularised time series (see the [baseline report]({{ '/anomaly-detection/ransac/' | relative_url }})), normalised point-wise to zero mean and unit variance.
- **Windowing:** Fixed-length windows spanning the full observation period. Missing months are backfilled with the RANSAC interpolant before normalisation.
- **Train/validation split:** Hold out ROIs with known anomalies to validate threshold selection.

## Model Architecture

- Symmetric fully connected encoder/decoder with bottleneck dimension tuned via validation.
- ReLU activations and batch normalisation to stabilise training.
- Dropout applied in the bottleneck to encourage robust reconstructions.

## Training Details

- Optimiser: Adam (`lr = 1e-3`, weight decay `1e-5`).
- Loss: Mean squared error between input and reconstruction.
- Early stopping on validation reconstruction loss with patience of 25 epochs.

## Results Snapshot

| Metric | Value | Notes |
| --- | --- | --- |
| AUROC | _TBD_ | Evaluate on labelled anomalies, if available. |
| Precision@top1% | _TBD_ | Rank by reconstruction error across the catalogue. |
| Mean reconstruction error | _TBD_ | Compare against RANSAC residuals. |

Replace the placeholders with the actual numbers from experiments. Add plots showcasing reconstruction quality, per-point anomaly scores, and spatial maps highlighting flagged areas.

## Next Steps

1. Experiment with convolutional layers on the temporal axis to capture local trends.
2. Compare fixed global thresholds vs. ROI-specific thresholds derived from score distributions.
3. Integrate uncertainty estimates (e.g., Monte Carlo dropout) to modulate alerts by confidence.

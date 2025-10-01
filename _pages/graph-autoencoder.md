---
title: Graph Autoencoder Anomaly Detection
permalink: /anomaly-detection/graph-autoencoder/
parent: Anomaly Detection
nav_order: 3
---

## Overview

The graph autoencoder (GAE) extends reconstruction-based anomaly detection by encoding spatial relationships between neighbouring InSAR points. Nodes represent observation points, with edges defined by k-nearest neighbours in geographic space or by correlation in the RANSAC-regularised signals.

## Graph Construction

- **Nodes:** One per persistent scatterer or grid cell in the ROI.
- **Edges:** k-NN in latitude/longitude with radius cut-off to avoid long links; edge weights proportional to temporal correlation.
- **Features:** Normalised time-series embeddings (mean, trend, seasonal components) and optional static metadata (elevation, land cover).

## Model Architecture

- Encoder: Two-layer graph convolutional network (GCN) mapping node features to a latent representation.
- Decoder: Inner-product decoder reconstructing adjacency; a parallel MLP reconstructs node features for reconstruction loss.
- Regularisation: Edge dropout during training to encourage robustness to missing links.

## Training Objective

Combine adjacency reconstruction loss, node feature reconstruction loss, and a Kullback–Leibler divergence term if a variational GAE is used.

\[
\mathcal{L} = \lambda_A \cdot \mathcal{L}_\text{adj} + \lambda_X \cdot \mathcal{L}_\text{feat} + \lambda_{KL} \cdot \mathcal{L}_\text{KL}
\]

Set `λ_A`, `λ_X`, and `λ_{KL}` on a validation split to balance structure vs. attribute fidelity.

## Evaluation

- Score nodes via reconstruction error or latent norm.
- Compare anomaly rankings with the pure autoencoder baseline to quantify spatial smoothing benefits.
- Visualise high-scoring nodes on the map and inspect neighbourhood explanations.

## Open Items

- Experiment with graph attention networks (GAT) to weigh neighbours dynamically.
- Investigate inductive generalisation to new ROIs by training on multiple areas simultaneously.
- Document failure cases where the graph structure introduces artefacts or smooths out real anomalies.

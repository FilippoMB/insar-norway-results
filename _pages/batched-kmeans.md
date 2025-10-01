---
title: Batched K-means
permalink: /clustering/batched-kmeans/
parent: Clustering
nav_order: 1
---

## Overview

Mini-batch K-means provides a scalable baseline to partition the InSAR catalogue into coherent deformation regimes. By processing small batches, it keeps memory usage manageable while approximating the centroid updates of classic K-means.

## Feature Engineering

- Use statistics derived from the RANSAC-regularised time series (trend, seasonal amplitude, residual variance).
- Append spatial coordinates scaled to unit variance so that clusters remain geographically meaningful.
- Optionally include autoencoder latent representations to blend reconstruction-aware features.

## Training Procedure

1. Standardise features using running moments estimated on the training split.
2. Initialise centroids with k-means++ on a buffer of randomly sampled points.
3. Iterate through shuffled mini-batches (e.g., size 512) and update centroids with a decaying learning rate.
4. Monitor inertia on a validation buffer to detect convergence.

## Model Selection

- Evaluate a range of cluster counts $k \in \{4, 6, 8, 10, 12\}$.
- Use silhouette score, Davies–Bouldin index, and manual inspection of spatial maps to choose $k$.
- Document sensitivity to feature scaling and batch size.

## Results Checklist

- Confusion between clusters and known labelled categories (if available).
- Spatial visualisations showing cluster extents and transitions between regimes.
- Time-series exemplars per cluster to interpret deformation behaviour.

Populate this page with the metrics, plots, and qualitative analysis produced during experiments. Highlight strengths (speed, simplicity) and limitations (cluster shape assumptions) compared with the GNN-based approach.

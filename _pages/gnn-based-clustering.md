---
title: GNN-based Clustering
permalink: /clustering/gnn-based-clustering/
parent: Clustering
nav_order: 2
---

## Overview

This experiment investigates graph neural network (GNN) embeddings as a precursor to clustering. The goal is to derive node representations that capture spatial context and temporal dynamics before applying a clustering algorithm in latent space.

## Pipeline

1. **Graph construction:** Same neighbourhood graph as the [graph autoencoder]({{ '/anomaly-detection/graph-autoencoder/' | relative_url }}), ensuring consistent connectivity assumptions across methods.
2. **Node feature extraction:** Combine raw RANSAC residual summaries with autoencoder latent features.
3. **Representation learning:** Train a GNN (GraphSAGE or GAT) with unsupervised objectives such as Deep Graph Infomax or contrastive loss.
4. **Clustering:** Run K-means or density-based clustering on the learned embeddings.

## Training Notes

- Batch sampling strategy (neighbourhood sampling vs. full-batch) impacts runtime; document the chosen approach.
- Hyper-parameters: number of layers, hidden size, aggregator type, dropout, and learning rate.
- Include early stopping criteria based on embedding stability or proxy validation metrics.

## Evaluation

- Compare cluster consistency metrics (silhouette, modularity) against the batched K-means baseline.
- Inspect embedding t-SNE/UMAP plots for separation quality.
- Provide geographic cluster maps and representative time series per cluster.

## Discussion Points

- Does incorporating graph structure sharpen cluster boundaries or over-smooth fine details?
- How sensitive are embeddings to edge definitions and feature normalisation?
- Outline next steps such as incorporating positional encodings or hierarchical clustering.

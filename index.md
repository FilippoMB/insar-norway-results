---
layout: single
title: InSAR Norway Machine Learning
permalink: /
toc: false
---

Welcome to a curated set of reports covering machine learning experiments on InSAR data from Norway. Each section below groups related techniques so you can compare modelling choices and results side-by-side.

## Anomaly Detection

Explore baselines and deep-learning methods that surface abnormal displacement patterns.

- [Autoencoder]({{ '/anomaly-detection/autoencoder/' | relative_url }}) — reconstruction-based anomaly scoring on regularised time series.
- [Graph Autoencoder]({{ '/anomaly-detection/graph-autoencoder/' | relative_url }}) — relational modelling of neighbouring points to flag inconsistent behaviour.
- [RANSAC Baseline]({{ '/anomaly-detection/ransac/' | relative_url }}) — robust plane and trend fitting used for outlier detection and time-series resampling.

## Clustering

Compare approaches that partition the InSAR catalogue into coherent deformation regimes.

- [Batched K-means]({{ '/clustering/batched-kmeans/' | relative_url }}) — scalable mini-batch training for large point clouds.
- [GNN-based Clustering]({{ '/clustering/gnn-based-clustering/' | relative_url }}) — representation learning with graph neural networks prior to clustering.

## Semi-supervised Learning

Blend limited labels with graph structure to propagate deformation categories across Norway's monitoring network.

- [Graph-based SSL Method]({{ '/semi-supervised-learning/ss-method/' | relative_url }}) — label propagation using graph regularisation and confidence-aware pseudo-labelling.

If you are looking for a quick overview, use the navigation bar to jump directly to a method of interest.

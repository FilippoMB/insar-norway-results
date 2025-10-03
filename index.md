---
layout: single
title: 🛰️ InSAR Norway & Machine Learning 🤖
permalink: /
toc: false
---

Results obtained by applying different machine learning techniques on [InSAR data from Norway](https://insar.ngu.no/). Each section below groups related techniques so you can compare modelling choices and results side-by-side.

## Anomaly Detection

Approaches that aim at detecting abnormal displacement patterns.

- [RANSAC Baseline]({{ '/anomaly-detection/ransac/' | relative_url }}) — robust plane and trend fitting used for outlier detection and time-series resampling.
- [Autoencoder]({{ '/anomaly-detection/autoencoder/' | relative_url }}) — reconstruction-based anomaly scoring on regularised time series.
- [Graph Autoencoder]({{ '/anomaly-detection/graph-autoencoder/' | relative_url }}) — relational modelling of neighbouring points to detect inconsistent behaviour.

## Clustering

Approaches that partition the InSAR data into coherent groups.

- [Batched K-means]({{ '/clustering/batched-kmeans/' | relative_url }}) — partition the time series with a scalable mini-batch clustering approach for large data.
- [GNN-based Clustering]({{ '/clustering/gnn-based-clustering/' | relative_url }}) — leverages graph neural networks to form clusters accounting for both temporal dynamics and spatial patterns.

## Semi-supervised Learning

Combines information from a limited set of labels and structures in the data to put decision boundaries in low-desnity regions.

- [Graph-based SSL Method]({{ '/semi-supervised-learning/ss-method/' | relative_url }}) — label propagation using graph regularisation.

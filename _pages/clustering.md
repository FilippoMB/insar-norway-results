---
title: Clustering
permalink: /clustering/
nav_order: 2
has_children: true
toc: false
---

Clustering experiments aim to group points exhibiting similar deformation profiles. We contrast a scalable, centroid-based approach with graph neural network representations that better capture local context before clustering.

- [Batched K-means]({{ '/clustering/batched-kmeans/' | relative_url }}) compresses the dataset with mini-batches and incremental centroid updates.
- [GNN-based clustering]({{ '/clustering/gnn-based-clustering/' | relative_url }}) learns embeddings through message passing and applies clustering in the latent space.

Each report details the processing pipeline, hyper-parameters, evaluation metrics, and qualitative maps for the resulting clusters.

---
title: Graph-based Semi-supervised Method
permalink: /semi-supervised-learning/ss-method/
parent: Semi-supervised Learning
nav_order: 1
---

## Overview

We study a graph-based semi-supervised learning (SSL) approach that propagates sparse human annotations to unlabelled InSAR points. The method exploits spatial proximity and temporal similarity captured by the monitoring graph.

## Problem Setup

- **Labels:** A small subset of points annotated as stable, gradually deforming, or rapidly deforming.
- **Graph:** Nodes correspond to InSAR points; edges connect spatial neighbours with weights proportional to signal correlation.
- **Objective:** Infer labels for unannotated nodes while maintaining smoothness across the graph and respecting confident seeds.

## Method

1. Initialise node probabilities with one-hot vectors for labelled nodes and uniform priors elsewhere.
2. Run label propagation with a Laplacian regulariser:
   \[
   \min_{F} \; \|F - Y\|_F^2 + \alpha \cdot \text{tr}(F^\top L F) + \beta \cdot \|F\|_1
   \]
   where $F$ are soft labels, $Y$ encodes supervision, and $L$ is the graph Laplacian.
3. Apply confidence-aware pseudo-labelling by promoting high-probability predictions to the labelled set and repeating.

## Evaluation

- Hold out a validation set of labelled points to monitor macro-F1 and calibration.
- Produce precision–recall curves per class to detect bias towards majority labels.
- Map predicted classes and confidence scores to assess spatial smoothness and highlight edge cases.

## Integration Notes

- Downstream anomaly detectors can use predicted class probabilities as contextual features.
- When new manual annotations arrive, rerun the propagation to refresh the catalogue.
- Consider experimenting with graph neural network semi-supervised models (e.g., GCN, MixHop) as future baselines.

Document quantitative results, decision thresholds, and qualitative insights here as they become available.

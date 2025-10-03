---
title: Graph Autoencoder Anomaly Detection
permalink: /anomaly-detection/graph-autoencoder/
parent: Anomaly Detection
nav_order: 3
---

**🛠️ WORK IN PROGRESS**

## Overview

The graph autoencoder (GAE) extends reconstruction-based anomaly detection by encoding spatial relationships between neighbouring InSAR points. Nodes represent observation points, with edges defined by k-nearest neighbours in geographic space.

## Graph Construction

- **Nodes:** Individual time series.
- **Edges:** $k$-NN in latitude/longitude; edge weights proportional to the distance.
- **Features:** Normalised time-series embeddings and optional static metadata.

---
title: RANSAC Baseline
permalink: /anomaly-detection/ransac/
parent: Anomaly Detection
nav_order: 1
---

## Overview

Random Sample Consensus (RANSAC) is a robust estimation method that fits a model to data containing outliers. It iteratively samples minimal subsets of points (2D or 3D), fits a candidate model (e.g., a line or a plane), scores it by counting inliers within a residual threshold, and keeps the model with the largest consensus set. Unlike ordinary least squares (OLS), it tolerates a high fraction of outliers without being skewed by them.

![](/assets/figs/ransac/ransac_vs_ols.png)

We use RANSAC in two places:

- To detect outliers by fitting linear models (lines or planes) and classifying as outliers the points that are not explained by any consensus set. This serves as a **baseline** to compare more advanced deep-learning based methods later on.
- To resample irregular time series onto a regular grid by using the fitted line as a principled interpolant between observed timestamps.

## Outlier Detection

### Time-Series Line Fitting (point-wise)

For each time series $y(t)$, fit a line $y = m \cdot t + c$ using RANSAC on the irregular acquisition times. Timestamps whose vertical residuals $|y - (m \cdot t + c)| \leq \tau$ are considered inliers; others behave as outliers for that series. The slope/intercept summarise the local linear trend; large disagreements with OLS or unusually poor consensus highlight problematic series.

Below, the top $2.5\%$ time series with the highest disagreement between RANSAC and OLS are highlighted. Points are coloured according to the mean velocity. Outliers are depicted as larger squares.

![](/assets/figs/ransac/Lyngen-small-2D-outliers-map.png)

The top 24 time series with the highest discrepancy between RANSAC and OLS are shown in detail below, along with their PID.

![](/assets/figs/ransac/Lyngen-small-top-outlier-time-series.png)

### Spatial Plane Fitting (global)

We fit planes $z = a \cdot x + b \cdot y + c$ where $x = \text{lat}$, $y = \text{lon}$, and $z$ is the RANSAC slope from the time-series fit. This allows us to capture local planar trends. Points far from the plane are outliers. By using partially overlapping sliding windows of different sizes, it is possible to fit the data more accurately. For overlaps, aggregate per-point inlier “votes” and keep points with enough consensus as inliers.

![](/assets/figs/ransac/Lyngen-small-sliding-win.png)

**Problem:** how large should the tiles be? Too small $\rightarrow$ overfit noise; too large $\rightarrow$ assign points too far away to the same plane. See below an example of results for sliding windows of different size.

![](/assets/figs/ransac/RANSAC-plane-(win=1.0).png)

![](/assets/figs/ransac/RANSAC-plane-(win=0.50).png)

![](/assets/figs/ransac/RANSAC-plane-(win=0.25).png)

**Proposed solution:** iteratively run sliding-window RANSAC with progressively *larger* tiles and *looser* consensus ratio. At each iteration, peel their inliers, and continue until no plane gathers enough consensus. The remaining points after all plane extractions are flagged as spatial outliers.

![](/assets/figs/ransac/Lyngen-small-iterative-sliding-win.png)

## Nordnes

The results for the Nordnes ROI are reported below.

![](/assets/figs/ransac/Nordnes-2D-outliers-map.png)

![](/assets/figs/ransac/Nordnes-top-outlier-time-series.png)

![](/assets/figs/ransac/Nordnes-sliding-win.png)

![](/assets/figs/ransac/Nordnes-iterative-sliding-win.png)

## Resampling Irregular Time Series

To obtain better performance with the deep learning and clustering methods (to appear in the next reports), we transformed irregular time series into a regularly sampled series while preserving observed values and filling unobserved steps with a robust trend obtained from RANSAC fits. Without this procedure, there were large gaps in the time series that could create unwanted artefacts.

Procedure:

1. Fit RANSAC per series on $(t, y)$ to obtain slope $m$ and intercept $c$.
2. Build a regular time grid `t_reg` over `[t_min, t_max]`. The step was chosen as the difference in days.
3. For each series, fill the regular grid with $\hat{y}(t) = m \cdot t + c$. At timestamps where an observation exists, keep the original value and overwrite the prediction.

![](/assets/figs/ransac/ransac-regularization.png)

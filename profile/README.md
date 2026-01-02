# Whale Activity Index (WAI)

## Overview

The **Whale Activity Index (WAI)** is an open-source, on-chain indicator designed to quantify unusual activity of large Bitcoin market participants (“whales”).  
It transforms raw blockchain data into a robust, normalized index ranging from 0 to 100, enabling consistent comparison across different market regimes.

---

## Motivation

Raw on-chain metrics such as transaction count or volume suffer from a lack of historical context and strong outlier sensitivity  

WAI addresses these issues by measuring **relative activity** instead of absolute values and applying adaptive normalization and weighting.

---

## Methodology (High-Level)

### Input Metrics
- Whale Transaction Count
- Whale Transaction Volume (BTC)  
Aggregated on a daily basis.

### Adaptive Normalization
Metrics are normalized against a rolling baseline (SMA, EWMA, or Median) to account for long-term trends and structural shifts.

### Volatility-Aware Weighting
Metric weights are dynamically adjusted based on observed volatility, reducing noise from unstable inputs (e.g. volume spikes).

### Historical Scaling
The combined activity score is ranked using a rolling percentile window and linearly scaled to [0, 100], ensuring regime-independent interpretation.

---

## Interpretation

| WAI Range | Interpretation |
|---------|----------------|
| 0–20 | Very low whale activity |
| 20–40 | Below average |
| 40–60 | Normal range |
| 60–80 | Elevated activity |
| 80–100 | Extreme, rare activity |

WAI is a context indicator, not a standalone trading signal.

---

## Architecture (Conceptual)

- **Collector Service** – extracts and aggregates whale transactions  
- **Backend API** – computes WAI, exposes history and parameters  
- **Visualization Layer (optional)** – charts and dashboards  

All components are modular and containerized.

---

## Scope & Limitations

- Measures activity, not price direction  
- No predictive guarantees  
- Parameter choices are empirically motivated  
- Reduced statistical power in early data windows  

These limitations are explicitly documented.

---

## Open Source

WAI is fully open source and designed for auditability, extension, and academic or practical use.

---

## Status

- Index specification: stable  
- Backend: operational  
- Validation & extensions: ongoing

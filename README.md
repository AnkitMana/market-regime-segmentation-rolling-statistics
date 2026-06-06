# 📊 Streaming Market Regime Detection using Statistical Time-Series Analysis

## Overview

This project implements a **streaming-style market regime detection system** for financial time-series data using rolling statistical methods.

The system is designed to identify structural changes in market behavior by analyzing shifts in return distributions over time, while strictly maintaining a forward-only (no look-ahead) processing pipeline.

---

## Motivation

Financial time-series data is inherently:
- Non-stationary
- Noisy
- Regime-dependent

Traditional approaches such as global clustering or offline probabilistic models often rely on full dataset access, which can introduce look-ahead bias and limit real-time applicability.

This project explores a lightweight alternative based on **sequential statistical monitoring**.

---

## Methodology

### 1. Streaming Processing
- Data is processed sequentially in time order
- No future information is used in computations

### 2. Rolling Window Statistics
For each window:
- Mean
- Standard deviation
- Deviation from reference regime statistics

### 3. Regime Definition
A regime is defined using:
- Stable statistical behavior over time
- Persistence of mean and variance characteristics
- Controlled deviation thresholds

### 4. Transition Logic
A regime transition is detected when:
- The deviation from current regime statistics exceeds a threshold
- The deviation persists across consecutive observations (noise filtering)

---

## Key Features

- Forward-only streaming design (no look-ahead bias)
- Rolling statistical feature extraction
- Lightweight regime segmentation logic
- Noise-resistant transition filtering
- NumPy-based numerical implementation
- Numba acceleration (where applied)

---

## Tech Stack

- Python
- NumPy
- Numba
- Pandas (for data handling)
- Matplotlib (for visualization)

---

## Use Cases

This system is applicable to:

- Market regime segmentation
- Volatility structure analysis
- Risk regime monitoring
- Time-series structural shift detection

---

## Limitations

- No probabilistic modeling (e.g., Hidden Markov Models not yet integrated)
- Thresholds are empirically defined
- No formal backtesting framework implemented
- Focused on segmentation, not direct prediction

---

## Future Work

- Benchmarking against Hidden Markov Models
- LSTM-based sequential prediction extensions
- Formal backtesting on financial datasets
- Multi-asset regime correlation analysis
- Adaptive threshold learning methods

---



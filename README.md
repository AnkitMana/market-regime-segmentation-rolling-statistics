# 📊 Streaming Market Regime Detection using Statistical Time-Series Analysis

## Overview

This project implements a **streaming-style market regime detection system** for financial time-series data using rolling statistical methods.

The objective is to identify structural changes in market behavior by analyzing shifts in return distributions over time, while ensuring a strictly forward-only (no look-ahead) processing pipeline.

This makes the system suitable for simulating real-time risk monitoring or sequential analysis environments.

---

## Data Source

Market data is obtained using the `yfinance` Python library, which provides historical financial data from Yahoo Finance.

- Source: Yahoo Finance via `yfinance`
- Data type: Daily adjusted closing prices
- Assets: Equity time-series (configurable)
- Feature engineering: Log returns computed from price series

This project is intended for research and educational purposes only.

---

## Motivation

Financial time-series data is inherently:
- Non-stationary
- Noisy
- Regime-dependent

Traditional approaches such as global clustering or offline probabilistic models (e.g., full-sequence Hidden Markov Models) often assume access to the complete dataset, which can introduce look-ahead bias and limit real-time applicability.

This project explores a lightweight alternative using **sequential statistical monitoring**.

---

## Methodology

### 1. Streaming Processing
- Data is processed in strict chronological order
- No future information is used at any stage

### 2. Log Return Transformation
Market prices are converted into returns using:

log(Pₜ / Pₜ₋₁)

This stabilizes variance and makes statistical properties more consistent.

---

### 3. Rolling Window Statistics
For each local window:
- Mean
- Standard deviation
- Deviation from reference regime statistics

---

### 4. Regime Representation
Each regime is characterized by:
- Mean return
- Volatility (standard deviation)
- Temporal stability across observations

---

### 5. Transition Logic
A regime change is detected when:
- The deviation from the current regime exceeds a threshold
- The deviation persists across consecutive observations (to reduce noise sensitivity)

---

## Key Features

- Forward-only streaming design (no look-ahead bias)
- Rolling statistical feature extraction
- Noise-resistant regime segmentation logic
- Lightweight numerical implementation using NumPy
- Accelerated computation using Numba (where applicable)

---

## Tech Stack

- Python
- NumPy
- Pandas
- Numba
- Matplotlib (for visualization)
- yfinance (data acquisition)

---

## Use Cases

This system is applicable to:

- Market regime segmentation
- Volatility structure analysis
- Risk regime monitoring
- Time-series structural shift detection
- Research in statistical signal processing

---

## Limitations

- The model is based on heuristic statistical thresholds and does not learn regime boundaries directly from data.
- No probabilistic framework (e.g., Hidden Markov Models) is currently implemented for comparison.
- Sensitivity to threshold selection may affect segmentation stability across different datasets.
- No formal backtesting or predictive validation has been performed yet.
- The current implementation focuses on regime segmentation rather than forecasting.

---

## Future Work

- Benchmarking against Hidden Markov Models
- LSTM-based sequential modeling for regime prediction
- Formal backtesting framework for financial validation
- Multi-asset regime correlation analysis
- Adaptive threshold learning methods

---

## Repository Structure

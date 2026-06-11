# Unsupervised Market Regime Segmentation Engine

## Overview

Financial markets continuously transition between different behavioral states. Periods of low volatility, high volatility, strong trends, market crashes, and recoveries often exhibit distinct statistical characteristics. Identifying these changes can provide valuable insight into underlying market dynamics.

This project explores an unsupervised approach for detecting market regime transitions using rolling statistical analysis of financial time series. The framework segments historical market data into statistically similar regions without relying on labeled training data or predefined regime classifications.

The primary objective was to investigate whether simple statistical properties of streaming market returns could be used to identify structural changes in market behavior while maintaining an interpretable and computationally lightweight architecture.

---

## Objectives

The project was designed to:

- Detect changes in market behavior using only historical price data.
- Identify volatility-driven regime transitions.
- Segment financial time series into statistically coherent regions.
- Develop a streaming framework capable of adaptive boundary detection.
- Visualize market regimes through volatility-aware overlays.
- Explore unsupervised techniques commonly encountered in quantitative finance research.

---

## Methodology

### Data Collection

Historical market data is obtained using Yahoo Finance through the `yfinance` library.

### Return Transformation

Daily closing prices are transformed into logarithmic returns:

\[
r_t = \ln\left(\frac{P_t}{P_{t-1}}\right)
\]

Log returns are widely used in quantitative finance due to their additive properties and suitability for statistical analysis.

### Initial Regime Seeding

The algorithm begins by constructing an initial anchor regime using a fixed number of observations.

For the initial regime, the following statistics are computed:

- Mean return
- Standard deviation (volatility)

These values serve as the baseline profile for subsequent comparisons.

### Streaming Window Generation

New observations are continuously collected into a rolling analysis window.

The rolling window allows the algorithm to evaluate whether incoming market behavior remains statistically consistent with the active regime.

### Similarity Analysis

Incoming observations are compared against the active regime profile using a normalized statistical similarity signal.

The signal incorporates:

- Difference in mean returns
- Difference in volatility
- Standard error normalization

The resulting score provides a measure of similarity between the current regime and the incoming observations.

### Boundary Refinement

A progressive trimming process is applied to the rolling window.

The algorithm searches for a boundary location where the remaining observations regain similarity with the active regime.

This allows regime boundaries to emerge dynamically instead of relying on fixed segmentation intervals.

### Regime Creation

Depending on the similarity score:

- Similar observations are absorbed into the current regime.
- Dissimilar observations initialize a new regime.

This process enables fully unsupervised segmentation of the time series.

---

## Visualization

Detected regimes are visualized using cumulative log returns.

Background shading is used to represent regime volatility:

- Lighter regions indicate relatively stable periods.
- Darker regions indicate higher volatility environments.
- Vertical boundaries represent detected regime transitions.

This provides an intuitive view of how market behavior evolves over time.

---

## Results

The framework was evaluated across multiple large-cap equities using identical segmentation logic and parameter settings.

The generated outputs demonstrate:

- Identification of major volatility events.
- Segmentation of stable and unstable market periods.
- Adaptive regime lengths without manual labeling.
- Consistent behavior across different financial instruments.

### Example Output 1

![Ticker 1](images/ticker_1.png)

### Example Output 2

![Ticker 2](images/ticker_2.png)

### Example Output 3

![Ticker 3](images/ticker_3.png)

### Example Output 4

![Ticker 4](images/ticker_4.png)

---

## Key Observations

Several consistent patterns emerged during experimentation:

- Volatility spikes frequently coincide with regime transitions.
- Stable market periods tend to form longer homogeneous regimes.
- Different assets generate distinct segmentation structures despite identical parameters.
- The framework captures large-scale structural changes without requiring supervised labels.

---

## Repository Contents

```text
market-regime-segmentation-rolling-statistics/
│
├── market_regime_engine.ipynb
│   Research notebook containing development,
│   experimentation, and visualization workflows.
│
├── market_regime_engine.py
│   Standalone implementation of the complete
│   market regime segmentation pipeline.
│
├── README.md
│   Project documentation and methodology.
│
├── requirements.txt
│   Required Python dependencies.
│
└── images/
    ├── ticker_1.png
    ├── ticker_2.png
    ├── ticker_3.png
    └── ticker_4.png

    Example outputs from multiple assets.
```

---

## Installation

Clone the repository:

```bash
git clone https://github.com/AnkitMana/market-regime-segmentation-rolling-statistics.git
cd market-regime-segmentation-rolling-statistics
```

Install dependencies:

```bash
pip install -r requirements.txt
```

---

## Usage

Run the standalone implementation:

```bash
python market_regime_engine.py
```

Alternatively, explore the notebook version:

```bash
jupyter notebook market_regime_engine.ipynb
```

---

## Technologies Used

- Python
- NumPy
- Pandas
- Matplotlib
- Yahoo Finance (yfinance)
- Numba

---

## Limitations

This project is intended as an exploratory statistical framework and has several limitations:

- Regime boundaries are sensitive to window-size selection.
- Similarity thresholds require manual tuning.
- Only first-order return statistics are considered.
- No external ground-truth labels are available for validation.
- Market volume, macroeconomic factors, and market microstructure information are not incorporated.

---

## Future Work

Potential extensions include:

- Hidden Markov Models (HMMs)
- Bayesian Online Change Point Detection
- Adaptive threshold selection
- Multi-factor regime characterization
- Volatility clustering models
- Real-time streaming deployment
- Regime-aware portfolio allocation
- Risk management applications
- Cross-asset regime analysis

---

## Conclusion

This project demonstrates how simple statistical techniques can be used to construct an unsupervised market regime detection framework. While intentionally lightweight and interpretable, the methodology successfully identifies periods of changing market behavior and highlights the potential of statistical segmentation approaches for quantitative finance research.

The work also served as an exploration of streaming data analysis, adaptive boundary detection, and financial time-series modeling, providing a foundation for future development of more sophisticated regime identification systems.
---

## Repository Structure

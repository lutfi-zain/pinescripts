
# 📈 0xBujang IchiMMA Strategy

A Pine Script™ strategy designed for TradingView, combining **SMMA**, **Z-Score**, and **Ichimoku** filtering to generate systematic long and short trading signals. Built with a focus on price momentum measured against statistical thresholds, this system is intended for traders looking for a clean and data-driven approach to trend detection.

> ⚠️ This strategy is for educational and backtesting purposes only. Use at your own risk.

---

## 🔍 Overview

**0xBujang IchiMMA** follows 3 main steps:

1. ✅ **SMMA (Smoothed Moving Average) Calculation**
2. ✅ **Z-Score Normalization**
3. ⌚ **Ichimoku Filter Conditions (future improvement)**

---

## ⚙️ Strategy Logic

### 1. SMMA Calculation

The SMMA is calculated using a recursive formula:

```
SMMAₜ = α × Priceₜ + (1 − α) × SMMAₜ₋₁
```

Where:
- `α = 1 / length`
- `length` = input period
- `Priceₜ` = current bar close
- `SMMAₜ₋₁` = previous SMMA value

### 2. Z-Score Calculation

Once SMMA is calculated, we compute the **Z-Score** to measure price deviation:

```
Z = (SMMA - mean) / stdev
```

Where:
- `mean` = EMA(SMMA, lookback)
- `stdev` = standard deviation of SMMA over lookback period

### 3. Signal Conditions

- **Long Signal**:
  - `Z > longThreshold` (default = `0.1`)
  - Only triggered when not already long
- **Short Signal**:
  - `Z < shortThreshold` (default = `-0.1`)
  - Only triggered when not already short

Visual areas for extreme values are also plotted:
- `Z > 2` or `Z > 4` (Overbought)
- `Z < -2` or `Z < -4` (Oversold)

---

## 📊 Plot & Labels

- Z-Score with dynamic color:
  - Green for Long
  - Red for Short
  - Gray for Neutral
- Optional chart labels:
  - `LONG` and `SHORT` when signals are triggered
- Halving markers:
  - Displays historical BTC halving dates (2012, 2016, 2020, 2024)

---

## 🧪 Backtesting Controls

- Start date input (`backtestStartAt`) for performance testing from a specific time
- Position size based on `% of equity`

---

## 🧠 Advanced Logic (WIP)

The script also includes placeholders for future enhancements:

- **Exit Signals** based on:
  - Z-score peak detection
  - Ichimoku crossover (Kijun & Tenkan)
  - Time-based trailing exit confirmation

---

## 🧾 Example Settings

```text
SMMA Length: 18
Z-Score Lookback: 50
Long Threshold: 0.1
Short Threshold: -0.1
```

---

## 📅 BTC Halving Dates

Halving dates are hardcoded and labeled:

- 🟢 **2012**: Nov 28
- 🟢 **2016**: Jul 9
- 🟢 **2020**: May 11
- 🟡 **2024**: Apr 19 (estimated)

---

## 📜 License

This project is licensed under the [Mozilla Public License 2.0](https://www.mozilla.org/MPL/2.0/)

© 0xBujang

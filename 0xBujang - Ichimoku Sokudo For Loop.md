# 🧠 0xBujang - Ichimoku Sokudō For Loop

![PineScript](https://img.shields.io/badge/Built%20With-Pine%20Script%20v6-05bca9)
![Strategy Type](https://img.shields.io/badge/Type-Trend--Following-yellow)
![Sharpe Ratio](https://img.shields.io/badge/Sharpe%20Ratio-0.195-blue)
![Sortino Ratio](https://img.shields.io/badge/Sortino%20Ratio-2.282-blueviolet)
![Profit Factor](https://img.shields.io/badge/Profit%20Factor-11.101-success)
![Net Profit](https://img.shields.io/badge/Net%20Profit-%2B3%2C572.75%25-ff69b4)

A hybrid Pine Script strategy that fuses **Zero Lag EMA**, **loop-based scoring**, and **Ichimoku cloud logic** to dynamically identify market trends with refined entry signals. Developed by **0xBujang**, inspired by **QuantAlgo**'s framework.

---

## 📊 Strategy Performance (Sample Backtest)

> **Backtested with $10,000 initial capital**  
> *Note: Past performance does not guarantee future results.*

| Metric                    | Value                   |
|---------------------------|-------------------------|
| **Sharpe Ratio**          | 0.195                   |
| **Sortino Ratio**         | 2.282                   |
| **Profit Factor**         | 11.101                  |
| **Net Profit**            | $357,274.91 (+3,572.75%)|
| **Total Trades**          | 12                      |
| **Avg Winning Trade**     | $56,092.03 (103.12%)    |
| **Avg Losing Trade**      | $7,073.86 (11.57%)      |
| **Largest Win %**         | 322.76%                 |
| **Largest Loss %**        | 25.66%                  |

---

## 🧮 Core Formulas

### 🔹 Zero Lag EMA (ZLEMA)
Removes traditional EMA lag by adjusting the input with past data:

```
ZLEMA = EMA(close + (close - close[lag]), length)
```
- `lag = (length - 1) / 2`

### 🔹 Volatility Filter

```
Volatility = Highest(ATR(length), length * 3) × Volatility Multiplier
```

---

## 🔁 Loop-Based Scoring System

The strategy evaluates price action over a custom loop window:

```pinescript
for i = loop_start to loop_end
    if basis_price > basis_price[i]
        sum += 1
    else
        sum -= 1
```

Positive scores = uptrend bias, negative scores = downtrend.

---

## 🚦 Signal Conditions

### 📤 Long Signal
- Score > Threshold
- Close > ZLEMA + volatility buffer

### 📥 Short Signal
- Score < Threshold
- Close < ZLEMA - volatility buffer

Trend must change to trigger.

---

## 🌥️ Ichimoku Enhancements

Ichimoku Cloud logic is used for **exit filtering**:
- **Close Long** if:
  - Price fully below cloud
  - Tenkan-sen under Kijun-sen
  - Candle body under both TK lines
- **Close Short** if:
  - Green cloud ahead and price inside it

---

## 🎨 Visualization Features

- Bullish/Bearish candle coloring
- Zero Lag Basis trend-colored line
- Trend shift markers (`𝑳` for Long, `𝑺` for Short)
- Optional Ichimoku cloud overlays

---

## 🧪 Strategy Settings

- Custom loop range, thresholds, and volatility factor
- Backtest limiter (start date)
- Enable/disable long/short signals
- Cleanly grouped UI inputs

---

## 🔔 Alerts

- `"Zero Lag Signals Long"`
- `"Zero Lag Signals Short"`

---

## 📜 License

This strategy is licensed under the **Mozilla Public License 2.0**. See [LICENSE](https://mozilla.org/MPL/2.0/) for more info.

---

## 🧠 Credits

- Original core by **QuantAlgo**
- Enhanced and integrated with Ichimoku by **@0xBujang**

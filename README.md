# 📈 Anchored VWAP-Based Uptrend Breakout Strategy

## 1) Strategy Title  
**Anchored VWAP-Based Uptrend Breakout Strategy**

---

## 2) Strategy Description  

This strategy combines **trend detection**, **macro high-low analysis**, and an **anchored VWAP (Volume-Weighted Average Price)** mechanism to generate dynamic buy/sell signals with capital allocation logic. It attempts to capture breakout opportunities within uptrends while managing risks through stop-loss levels and volume-based scaling.

---

### Steps Followed  

1. **Trend Detection**  
   - The algorithm classifies recent price movements into:
     - **Uptrend (1)**
     - **Downtrend (0)**
     - **Neutral (-1)**  
   - Classification is based on sequential highs and lows over a rolling 4-period window.

2. **Macro Lows and Highs Identification**  
   - Detects **macro swing lows** and **macro swing highs** from trend labels.
   - Used to confirm whether the price structure supports continuation or reversal.

3. **Anchored VWAP Calculation**  
   - Prices are anchored whenever price falls below the highest low band.
   - VWAP is computed using anchored prices and volumes to identify strong **above-anchor breakouts**.

4. **Buy Logic**  
   - If price rises above anchored VWAP and shows momentum:
     - Allocate **10–30%** of available capital depending on average buy cost.
     - Place a **STOP order** with an 8% stop-loss and 8% take-profit (minimum).  
   - If no prior buys exist, **20% of capital** is deployed initially.  
   - For fresh opportunities, a **5% allocation** is made when price is above average buy cost or under massive upward momentum.

5. **Sell Logic**  
   - If macro low peaks drop by at least **2 steps**, all open trades are closed.
   - If slope of recent highs weakens significantly, partial or complete exits are triggered.
   - Sell signals also occur when price exceeds **8% above average buy price**.

---

### Trading Interpretations  

- **Bullish Scenarios (Buy Triggers):**  
  - Price crosses **above anchored VWAP**.  
  - **Macro swing lows** and slope conditions confirm continuation of an uptrend.  
  - **Massive upward momentum** pattern detected in recent trend labels.  

- **Bearish Scenarios (Sell Triggers):**  
  - Failure of upward slope in recent highs.  
  - Price retreats below highest low band.  
  - Drop in swing lows signals trend weakness.  

- **Risk Management:**  
  - Dynamic **stop-loss** placement based on 8% of price or second-last low.  
  - **Capital scaling** ensures larger allocations only when price supports favorable momentum vs. average buy cost.  

---

## 3) Libraries Used  

- **AlgoAPI**  
  - `AlgoAPIUtil`: Utility for constructing and sending trading orders.  
  - `AlgoAPI_Backtest`: Handles event-driven backtesting and order execution simulation.  

- **datetime**  
  - Used for timestamp handling and calculating slopes/durations between highs and lows.  

---

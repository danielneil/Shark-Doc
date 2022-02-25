<p align="center">
  <img src="https://github.com/danielneil/Shark/blob/main/shark/files/shark_ui_patches/logofullsize.png?raw=true">
</p>

## Backtesting the famous RSI(2) strategy using Shark against BitCoin

This article discusses backtesting the RSI2 strategy with Shark against Bitcoin.

### Introduction to RSI2

RSI(2) is a famous trading strategy developed by Larry Connors.

> It is a fairly simple mean-reversion trading strategy designed to buy or sell securities after a corrective period. Traders should look for buying opportunities when 2-period RSI moves below 10, which is considered deeply oversold. Conversely, traders can look for short-selling opportunities when 2-period RSI moves above 90. ([Stock Charts](https://school.stockcharts.com/doku.php?id=trading_strategies:rsi2))

The sample code below is loosely modeled on the Stock Charts article above, but to summarise, the strategy behaves as follows:

#### 1. Identify the Major Trend using a long-term average

Connors recommends the 200-day moving average. 

> The long-term trend is up when a security is above its 200-day SMA and down when a security is below its 200-day SMA. Traders should look for buying opportunities when above the 200-day SMA and short-selling opportunities when below the 200-day SMA.

Therefore:
* For long opportunities > 200-day SMA
* For short opportunities < 200-day SMA

### 

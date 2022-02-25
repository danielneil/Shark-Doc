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

> The long-term trend is up when a security is above its 200-day SMA and down when a security is below its 200-day SMA. Traders should look for BUYING opportunities when above the 200-day SMA and SHORT-selling opportunities when below the 200-day SMA.

Therefore:
* Identify long opportunities when price is > 200-day SMA
* Identify short opportunities when price is < 200-day SMA

#### 2. Choose an RSI level to identify buying or selling opportunities within the bigger trend

Connors recommends RSI levels between 0 and 10 for buying and between 90 and 100 for selling.

> He found that returns were higher when buying on an RSI dip below 5 than on one below 10. In other words, the lower RSI dipped, the higher the returns on subsequent long positions. For short positions, the returns were higher when selling short on an RSI surge above 95 than on a surge above 90. In other words, the more short-term overbought the security, the greater the subsequent returns on a short position.

Therefore:
* Identify buying opportunities when RSI levels between 0 and 10.
* Identify selling opportunities when RSI levels between 90 and 100.



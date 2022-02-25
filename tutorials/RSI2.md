<p align="center">
  <img src="https://github.com/danielneil/Shark/blob/main/shark/files/shark_ui_patches/logofullsize.png?raw=true">
</p>

## Backtesting the famous RSI(2) strategy using Shark against BitCoin

This article discusses backtesting the [RSI2 strategy](https://school.stockcharts.com/doku.php?id=trading_strategies:rsi2) with Shark against Bitcoin.

### Introduction to RSI2
----

RSI(2) is a famous trading strategy developed by Larry Connors.

> It is a fairly simple mean-reversion trading strategy designed to buy or sell securities after a corrective period. Traders should look for buying opportunities when 2-period RSI moves below 10, which is considered deeply oversold. Conversely, traders can look for short-selling opportunities when 2-period RSI moves above 90. ([Stock Charts](https://school.stockcharts.com/doku.php?id=trading_strategies:rsi2))

The sample code below is loosely modeled on the Stock Charts article above, but to summarise, the strategy behaves as follows:

#### 1. Identify the Major Trend using a long-term average

Connors recommends the 200-day [moving average](https://www.investopedia.com/terms/m/movingaverage.asp). 

> The long-term trend is up when a security is above its 200-day SMA and down when a security is below its 200-day SMA. Traders should look for BUYING opportunities when above the 200-day SMA and SHORT-selling opportunities when below the 200-day SMA.

Therefore:
* Identify long opportunities when price is > 200-day SMA
* Identify short opportunities when price is < 200-day SMA

#### 2. Choose an RSI level to identify buying or selling opportunities within the bigger trend

Connors recommends [RSI](https://www.investopedia.com/terms/r/rsi.asp) levels between 0 and 10 for buying and between 90 and 100 for selling.

> He found that returns were higher when buying on an RSI dip below 5 than on one below 10. In other words, the lower RSI dipped, the higher the returns on subsequent long positions. For short positions, the returns were higher when selling short on an RSI surge above 95 than on a surge above 90. In other words, the more short-term overbought the security, the greater the subsequent returns on a short position.

Therefore:
* Identify buying opportunities when RSI levels between 0 and 10.
* Identify selling opportunities when RSI levels between 90 and 100.

#### 3. Set the exit point

> Connors advocates exiting long positions on a move above the 5-day SMA and short positions on a move below the 5-day SMA.

Therefore:

* Exit long positions when price moves above the 5-day SMA.
* Exit short positions when price moves below the 5-day SMA. 

### Shark Configuration

This section details the Shark configuration required to implement the backtest as above.

#### 1. Clone the Shark GitHub repository 

See quick setup [https://github.com/danielneil/Shark/blob/main/README.md#quick-setup](instructions).

#### 2. Fork the Shark-Config github repository, to your own GitHub account.

[How to?](https://docs.github.com/en/get-started/quickstart/fork-a-repo)

#### 4. From your forked Shark-Config Repo

Completed wipe the file Shark-Config/config/files/trading-config.yml and copy and paste the following
```
---
- instrument: BTC-USD
  group: B
  plugin:
  - name: yahoo_finance_data
    desc: "Yahoo Finance [ BTC-USD Historical Data File ]"
    group: "Yahoo Finance [ Historical Data ]"
    period1: 1410912000
    period2: 1644537600
    interval: 1d
    includeAdjustedClose: true
  - name: backtest
    desc: "BACKTEST: [ RSI2 ]"
    group: "Backtesting"
    file: rsi2.py
    shares: 100
    capital: 10000000
    data_format: yahoo_finance
    entrySMA: 200
    exitSMA: 5
    rsiPeriod: 2 
    overSoldThreshold: 10
    overBoughtThreshold: 90
    data_format: yahoo_finance_data
```

#### 3. Update the build.sh script to reflect your forked Shark-Config GitHub repo URL.

With a text editor, open site.yml in the Shark git repo, and do the following:

```
   # Change the following
   shark_config_repo: "https://github.com/danielneil/Shark-Config.git"
   
   # To something like this (where your_username, is your github username) 
   shark_config_repo: "https://github.com/<your_username>/Shark-Config.git"
```








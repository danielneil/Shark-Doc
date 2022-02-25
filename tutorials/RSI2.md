<p align="center">
  <img src="https://github.com/danielneil/Shark/blob/main/shark/files/shark_ui_patches/logofullsize.png?raw=true">
</p>

## Backtesting Larry Connor's RSI2 strategy against BitCoin with Shark

This article discusses backtesting the [RSI2 strategy](https://school.stockcharts.com/doku.php?id=trading_strategies:rsi2) against Bitcoin with Shark.

If you're impatient and just want to know - RSI2 performed terribly against BitCoin.

### Quick Introduction to RSI2
---

RSI(2) is a famous trading strategy developed by Larry Connors.

> It is a fairly simple mean-reversion trading strategy designed to buy or sell securities after a corrective period. Traders should look for buying opportunities when 2-period RSI moves below 10, which is considered deeply oversold. Conversely, traders can look for short-selling opportunities when 2-period RSI moves above 90. ([Stock Charts](https://school.stockcharts.com/doku.php?id=trading_strategies:rsi2))

The [sample code](https://github.com/danielneil/Shark-Config-RSI2-Demo/blob/master/backtests/files/backtests/rsi2.py) below is loosely modeled on the Stock Charts article above, but to summarise, the strategy behaves as follows:

##### 1. Identify the Major Trend using a long-term average

Connors recommends the 200-day simple [moving average](https://www.investopedia.com/terms/m/movingaverage.asp) (SMA). 

> The long-term trend is up when a security is above its 200-day SMA and down when a security is below its 200-day SMA. Traders should look for BUYING opportunities when above the 200-day SMA and SHORT-selling opportunities when below the 200-day SMA.

Therefore:
* Identify long opportunities when price is > 200-day SMA
* Identify short opportunities when price is < 200-day SMA

##### 2. Choose an RSI level to identify buying or selling opportunities within the bigger trend

Connors recommends [RSI](https://www.investopedia.com/terms/r/rsi.asp) levels between 0 and 10 for buying and between 90 and 100 for selling.

> He found that returns were higher when buying on an RSI dip below 5 than on one below 10. In other words, the lower RSI dipped, the higher the returns on subsequent long positions. For short positions, the returns were higher when selling short on an RSI surge above 95 than on a surge above 90. In other words, the more short-term overbought the security, the greater the subsequent returns on a short position.

Therefore:
* Identify buying opportunities when RSI levels between 0 and 10.
* Identify selling opportunities when RSI levels between 90 and 100.

##### 3. Set the exit point

> Connors advocates exiting long positions on a move above the 5-day SMA and short positions on a move below the 5-day SMA.

Therefore:

* Exit long positions when price moves above the 5-day SMA.
* Exit short positions when price moves below the 5-day SMA. 

### Shark Configuration
---

This section details the Shark configuration required to implement the backtest as above.

##### 1. Clone the Shark GitHub repository 

```
git clone https://github.com/danielneil/Shark.git
```

See Quick Setup [https://github.com/danielneil/Shark/blob/main/README.md#quick-setup](instructions).

##### 2. Fork the Shark-Config github repository, to your own GitHub account.

* [How?](https://docs.github.com/en/get-started/quickstart/fork-a-repo)
* If you just want to see an example, here is one I prepared [earlier](https://github.com/danielneil/Shark-Config-RSI2-Demo).

##### 3. From your forked Shark-Config Repo

Wipe the demo config file Shark-Config/config/files/trading-config.yml and replace with the following
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

It demostrates the use of two Shark plugins, namely yahoo_finance_data and backtest.

##### 4. Update site.yml to reflect your forked Shark-Config GitHub repo URL.

With a text editor, open site.yml in the Shark git repo, and:

```
   # Change the following: 
   shark_config_repo: "https://github.com/danielneil/Shark-Config.git"
   
   # To something like this (where your_username, is your github username) 
   shark_config_repo: "https://github.com/<your_username>/Shark-Config.git"
```

Also, as I have forked it for you, you can spin up my version with:
```
   # Change the following: 
   shark_config_repo: "https://github.com/danielneil/Shark-Config.git"
   
   # To this:
   shark_config_repo: "https://github.com/danielneil/Shark-Config-RSI2-Demo.git"
```

##### 5. Build Shark as per the Quick Setup instructions, specifically.
```
yum install epel-release -y
yum install ansible -y
yum install git -y

cd Shark && ./build.sh 
```

Open a web browser and navigate to http://SHARK_SERVER_IP/shark - (with shark/shark as username/password )

##### 6. Let Shark do its thing
  
(It might take a few minutes for Shark to cache the historical data file from yahoo finance and then perform the backtest).
  
With your new RSI2 Configuration, Shark has done three things.
 
* Downloaded the historical data from yahoo finance
* Ran your RSI2 backtest code against the downloaded historical data
* Produced a report detailng its findings on the above
  
If you click "Coins", you should have an image that looks like this:
  
<p align="center">
  <img src="https://github.com/danielneil/Shark-Doc/blob/main/tutorials/shark_tutorial_images/shark-rsi2-main.png?raw=true">
</p>
  
You can see there are two plugins that correlate to the configuration you entered as above.
  
If you looked hard, you probably noticed the [Sharpe Ratio](https://www.investopedia.com/terms/s/sharperatio.asp) was 0.0 (which is terrible!), ideal Sharpe ratios are always postive numbers! 

##### 7. Analysing the results
 
As per the result from the backtest plugin that ran our RSI2 code, the Sharpe ratio was less than ideal.
  
If want to drill into the specifics of the report, from the side menu, navigate to:
 
1. Under Portfolio > Backtesting, click Reports
2. Select the coin (BTC-USD), and the results should be as follows.
  
For the impatient, here it what I found.

<p align="center">
  <img src="https://github.com/danielneil/Shark-Doc/blob/main/tutorials/shark_tutorial_images/shark-rsi2-backtest-report.png?raw=true">
</p>
  
### Why did RSI2 perform terribly?
---
  
Well, could be a few reasons:
  
* Perhaps RSI2 is indeed a terrible strategy for trading BitCoin.
* A limitation of Yahoo Finance data is that only the close price is listed, perhaps intraday tick data would perform better? 
* My code could be crap? Let me know if you find a bug.

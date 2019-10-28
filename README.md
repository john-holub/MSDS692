# Developing Algorithmic Trading Strategies
Project for MSDS692, Data Science Practicum I

John Holub

___
## Table of Contents
- Summary & Project Goals
- Exploratory Analysis
- Algorithmic Systems
- System Performance Results
- Challenges & Findings
- Acknowledgments and References

___
## Summary
In recent years cloud computing environments has made previous very cumbersome and expensive intraday financial time series data much more accessible than it has ever been. In addition to the data becoming more accessible, cloud computing has also made working with the data much easier as well with online environments, docker images and IDEs.

It is estimated over &quot;80% of daily trades in United State are machine-led&quot;<sup>1</sup> which is up from an estimated 15% in early 2000s<sup>1</sup>. This suggests a growth market for algorithmic trading and possibly extending its benefits to the non-professional. With this project I intend to explore the possibilities of algorithmic trading, not only in the short-term, but also for long-term investments and development of capital preservation methods applied to traditional portfolio allocations.

## Project Goals
1. Gain familiarity with large price/time series financial data and defining, developing, testing, optimizing and implementing (bring to Production Stage) algorithmic trading strategies.
2. Develop method(s) for rapid Exploratory Data Analysis (EDA) and Feasibility Analysis (FA) of potential algorithms.
3. Bring algorithm(s) to production and test performance in live real-time environment (paper trading).
4. Summarize, visualize and communicate results in useful and attractive format.

___
## Exploratory Analysis
It's generally accepted amongst traders that roughly 80% of individual stocks follow the general market. Therefore, it is very important that we test to see how systems perform when compared to the general market. For this 


```python
# Developing Algorithmic Trading Strategies Project
Data Science Practicum I
MSDS692, John Holub

EDA to determine up and down market changepoint dates using fbprophet and stocker. These dates will be used to evaluate system viability in up/down market conditions.
```

Install and update libaries


```python
pip install -U quandl numpy pandas fbprophet matplotlib pytrends pystan plotly yfinance
```


```python
# Command for plotting in the notebook
import matplotlib.pyplot as plt
import yfinance as yf 
%matplotlib inline
```


```python
from stocker import Stocker
```


```python
# Use this code for Quandl WIKI stocks (no ETFs)
tesla = Stocker(ticker='TSLA')
```

    TSLA Stocker Initialized. Data covers 2010-06-29 00:00:00 to 2018-03-27 00:00:00.
    


```python
# Use this code for yahoo stocks and ETFs, must supply dates
SPY = yf.download('SPY','2009-01-01','2019-01-01')
```

    [*********************100%***********************]  1 of 1 completed
    


```python
stock_history = tesla.stock
stock_history.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Open</th>
      <th>High</th>
      <th>Low</th>
      <th>Close</th>
      <th>Volume</th>
      <th>Ex-Dividend</th>
      <th>Split Ratio</th>
      <th>Adj. Open</th>
      <th>Adj. High</th>
      <th>Adj. Low</th>
      <th>Adj. Close</th>
      <th>Adj. Volume</th>
      <th>ds</th>
      <th>y</th>
      <th>Daily Change</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2010-06-29</td>
      <td>19.0000</td>
      <td>25.0000</td>
      <td>17.54</td>
      <td>23.89</td>
      <td>18766300.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>19.0000</td>
      <td>25.0000</td>
      <td>17.54</td>
      <td>23.89</td>
      <td>18766300.0</td>
      <td>2010-06-29</td>
      <td>23.89</td>
      <td>4.8900</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2010-06-30</td>
      <td>25.7900</td>
      <td>30.4192</td>
      <td>23.30</td>
      <td>23.83</td>
      <td>17187100.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>25.7900</td>
      <td>30.4192</td>
      <td>23.30</td>
      <td>23.83</td>
      <td>17187100.0</td>
      <td>2010-06-30</td>
      <td>23.83</td>
      <td>-1.9600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2010-07-01</td>
      <td>25.0000</td>
      <td>25.9200</td>
      <td>20.27</td>
      <td>21.96</td>
      <td>8218800.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>25.0000</td>
      <td>25.9200</td>
      <td>20.27</td>
      <td>21.96</td>
      <td>8218800.0</td>
      <td>2010-07-01</td>
      <td>21.96</td>
      <td>-3.0400</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2010-07-02</td>
      <td>23.0000</td>
      <td>23.1000</td>
      <td>18.71</td>
      <td>19.20</td>
      <td>5139800.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>23.0000</td>
      <td>23.1000</td>
      <td>18.71</td>
      <td>19.20</td>
      <td>5139800.0</td>
      <td>2010-07-02</td>
      <td>19.20</td>
      <td>-3.8000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2010-07-06</td>
      <td>20.0000</td>
      <td>20.0000</td>
      <td>15.83</td>
      <td>16.11</td>
      <td>6866900.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>20.0000</td>
      <td>20.0000</td>
      <td>15.83</td>
      <td>16.11</td>
      <td>6866900.0</td>
      <td>2010-07-06</td>
      <td>16.11</td>
      <td>-3.8900</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2010-07-07</td>
      <td>16.4000</td>
      <td>16.6300</td>
      <td>14.98</td>
      <td>15.80</td>
      <td>6921700.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>16.4000</td>
      <td>16.6300</td>
      <td>14.98</td>
      <td>15.80</td>
      <td>6921700.0</td>
      <td>2010-07-07</td>
      <td>15.80</td>
      <td>-0.6000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2010-07-08</td>
      <td>16.1400</td>
      <td>17.5200</td>
      <td>15.57</td>
      <td>17.46</td>
      <td>7711400.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>16.1400</td>
      <td>17.5200</td>
      <td>15.57</td>
      <td>17.46</td>
      <td>7711400.0</td>
      <td>2010-07-08</td>
      <td>17.46</td>
      <td>1.3200</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2010-07-09</td>
      <td>17.5800</td>
      <td>17.9000</td>
      <td>16.55</td>
      <td>17.40</td>
      <td>4050600.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>17.5800</td>
      <td>17.9000</td>
      <td>16.55</td>
      <td>17.40</td>
      <td>4050600.0</td>
      <td>2010-07-09</td>
      <td>17.40</td>
      <td>-0.1800</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2010-07-12</td>
      <td>17.9500</td>
      <td>18.0700</td>
      <td>17.00</td>
      <td>17.05</td>
      <td>2202500.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>17.9500</td>
      <td>18.0700</td>
      <td>17.00</td>
      <td>17.05</td>
      <td>2202500.0</td>
      <td>2010-07-12</td>
      <td>17.05</td>
      <td>-0.9000</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2010-07-13</td>
      <td>17.3938</td>
      <td>18.6400</td>
      <td>16.90</td>
      <td>18.14</td>
      <td>2680100.0</td>
      <td>0.0</td>
      <td>1.0</td>
      <td>17.3938</td>
      <td>18.6400</td>
      <td>16.90</td>
      <td>18.14</td>
      <td>2680100.0</td>
      <td>2010-07-13</td>
      <td>18.14</td>
      <td>0.7462</td>
    </tr>
  </tbody>
</table>
</div>



fbprophet determines significant changedates which can be used to test system performance in previous up/down markets


```python
tesla.changepoint_date_analysis()
```

    
    Changepoints sorted by slope rate of change (2nd derivative):
    
              Date  Adj. Close     delta
    217 2016-02-08      147.99  7.293481
    169 2015-11-27      231.61 -3.517562
    265 2016-04-18      253.88 -3.505999
    313 2016-06-24      193.15  2.392548
    144 2015-10-22      211.72  1.987002
    


![png](output_9_1.png)



```python

```





___
## Algorithmic Systems
This is a very simple system that shorts equal dollar amounts of 3x Miner ETFs, attempting to capture the ETF rebalance decay. I was pleased to get a rebalancing system coded functionally, however the results are rather poor due to large drawdowns.

CODE:
```python
# Developing Algorithmic Trading Strategies Project
# Data Science Practicum I
# MSDS692, John Holub

# Simple strategy to capture decay of 3x miner ETFs. Rebalances every 60 days.

class OptionsAlgorithm(QCAlgorithm):

    def Initialize(self):
        self.SetStartDate(2014, 1, 1)
        # self.SetEndDate(2018, 12, 31)
        self.SetCash(100000)
        self.SetBrokerageModel(BrokerageName.InteractiveBrokersBrokerage)
        
        self.equitylist = ["JNUG", "JDST", "DUST", "NUGT","DGAZ","UGAZ"]

        self.noe = len(self.equitylist)
        def zerolistmaker(n):
            listofzeros = [0] * n
            return listofzeros

        self.equity = zerolistmaker(self.noe)
        self.syl = zerolistmaker(self.noe)
        
        for x in range(self.noe):
            self.equity[x] = self.AddSecurity(SecurityType.Equity, self.equitylist[x], Resolution.Minute)
            self.syl[x] = self.equity[x].Symbol
        
        self.days_counter = 100000
        
        #Set Trading and closing Times, for 1 day intra
        self.Schedule.On(self.DateRules.EveryDay(),self.TimeRules.At(9, 35),Action(self.Rebalance))
    
    def Rebalance(self): 
        
        self.days_counter+=1
        
        if self.days_counter >= 60:
            for x in range(self.noe):
                self.SetHoldings(self.syl[x], -1/(self.noe))
                self.days_counter = 0
```
___
## System Results

#### 3X ETF SHORT PAIRS Strategy Performance
![alttext1](https://github.com/john-holub/MSDS692/blob/master/IMAGES/3xETF_perf1.png "Image 1")
System returns are good, at 14% CAGR (Compound annual growth rate), however drawndowns make the system totally unviable with 38% max draw-down and numerous other very large drawdowns, as can be seen on the monthly returns.

#### 3X ETF SHORT PAIRS 5 worst drawdowns
![alttext1](https://github.com/john-holub/MSDS692/blob/master/IMAGES/3xETF_perf3.png "Image 3")
Here are the 5 worst drawdowns, where we can see the system had 2 drawdowns of over -30% and several more greater than -20%.

#### 3X ETF SHORT PAIRS performance vs SP500 Benchmark
![alttext1](https://github.com/john-holub/MSDS692/blob/master/IMAGES/3xETF_perf2.png "Image 3")
Again the system has decent returns, but as demonstrated by this chart the drawdowns are much worse than the SP5-- benchmark.

___
## Challenges 
- Emerging technology; not very robust documentation, not much on web, community not very active, many features buggy/not active yet
- Cloud computing platform more restrictive than local or virtual machine
- Some small fees (datafeeds/subscriptions)
- Very time consuming to manually go through trades for quality assurance
- Exceedingly difficult to beat general market benchmark (SP500) and/or traditional allocations (e.g. “Bogle Portfolio”)

## Findings
- Algo trading rapidly become viable for retail investors and traders. 
- Executions and live deployment APIs work well through retail investment brokers.
- Countless number of possible strategies, that will appeal to retail investors and traders.
- Strategies can be coded without tremendous difficulty, but viable strategies that outperform the general market over a long period are exceedingly difficult to discover.

___
## References

1. Real Finance. (2019) Algo Trading Dominates 80% Of Stock Market | Seeking Alpha. Retrieved September 16, 2019, from https://seekingalpha.com/article/4230982-algo-trading-dominates-80-percent-stock-market

2. Quantcademy. (2019) Self-Study Plan for Becoming a Quantitative Trader - Part I | QuantStart. Retrieved October 04, 2019, from https://www.quantstart.com/articles/Self-Study-Plan-for-Becoming-a-Quantitative-Trader-Part-I

3. Koehrsen, Will. (2019) Stock Prediction in Python - Towards Data Science. Retrieved October 20, 2019, from https://towardsdatascience.com/stock-prediction-in-python-b66555171a2

4. QuantConnect - Wikipedia. (2019) Retrieved September 16, 2019, from https://en.wikipedia.org/wiki/QuantConnect

5. Reddit. (2019) Algorithmic Trading. Retrieved September 27, 2019, from https://old.reddit.com/r/algotrading/
___ 






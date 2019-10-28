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


![alttext1](https://github.com/john-holub/MSDS692/blob/master/IMAGES/3xETF_perf1.png "Image 1")
#### 3X ETF SHORT PAIRS Strategy Performance


![alttext1](https://github.com/john-holub/MSDS692/blob/master/IMAGES/3xETF_perf2.png "Image 2")
#### 3X ETF SHORT PAIRS Cumulative Returns vs SP500 benchmark

![alttext1](https://github.com/john-holub/MSDS692/blob/master/IMAGES/3xETF_perf3.png "Image 3")
#### 3X ETF SHORT PAIRS 5 worst drawdowns


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






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


![alttext1](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_1.PNG "Image 1")

Understanding the data from the DICOM files is imperative to being able to ensure one's coneptualization of bounding boxes on the arrays from those files. After all, I am not a radiologist and do not have medical training. Therefore, I need to visualize those boxes in order to augment my knowledge regarding the visual aspects of pneumonia:

![alttext2](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_2.PNG "Image 2")

Now that we have visualized the bounding boxes and the XRAYs, we should take a look at the demographics of our study participants.

#### Frequency Chart of Detailed Class (Colored by Binary Class)
![alttext3](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_3.PNG "Image 3")

#### Frequency Chart of Binary Class (Colored by Binary Class)
![alttext4](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_4.PNG "Image 4")


#### Frequency Chart of Sex (Colored by Binary Class)
![alttext5](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_5.PNG "Image 5")

Ensuring that we maintain reasonably consistent demographic spreads when determining training and test sets will be imperative. Exploratory analysis will assist in that effort.

Making sure we understanding the pneumonia spread in these images will help us to identify anomalies in our predictions.
#### Heatmap of Pneumonia Presence in the Sample Images
![alttext6](https://github.com/evangibson/Pneumonia_Detection/blob/master/images/_img_6.PNG "Image 6")

For a look at some more of the exploratory analysis, please see the *Pneumonia Exploratory Analysis.ipynb* file.

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






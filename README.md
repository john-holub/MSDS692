# MSDS692, Data Science Practicum I: 
**Developing Algorithmic Trading Strategies**

**TO DO** :
1. EDA on "types of days" at very least identify "changepoints"
2. Several Strategies
  A. high volume, high volatility universe
  B. rebalance PP
    i. shorting ultras portfolio rebalance
    ii. Options sales on Friday
  D. gmail reminder strategy from 2013




**Developing Algorithmic Trading Strategies with QuantConnect and Lean Algorithmic Trading Engine (LEAN)**

1. **High level description** :

In recent years cloud computing environments has made previous very cumbersome and expensive intraday financial time series data much more accessible than it has ever been. In addition to the data becoming more accessible, cloud computing has also made working with the data much easier as well with online environments, docker images and IDEs.

It is estimated over &quot;80% of daily trades in United State are machine-led&quot;1 which is up from an estimated 15% in early 2000s1. This suggests a growth market for algorithmic trading and possibly extending its benefits to the non-professional. With this project I intend to explore the possibilities of algorithmic trading, not only in the short-term, but also for long-term investments and development of capital preservation methods applied to traditional portfolio allocations.

**Project Goals** :

1. Gain familiarity with large price/time series financial data and defining, developing, testing, optimizing and implementing (bring to Production Stage) algorithmic trading strategies.
2. Develop method(s) for rapid Exploratory Data Analysis (EDA) and Feasibility Analysis (FA) of potential algorithms.
3. Bring algorithm(s) to production and test performance in live real-time environment (paper trading).
4. Summarize, visualize and communicate results in useful and attractive format.

1. **Potential types of data science tasks** :

1. Classification of differing trading environments (e.g. &quot;bull&quot; or bear&quot;).
2. Clustering of differing trading betas, potentially to protect portfolio value in adverse trading environments.
3. Data Engineering of time series data, (e.g. merging event dates, such as earnings, to time series) to include &quot;Data Wrangling&quot; of potential &quot;bad ticks&quot; which can skew system results.
4. Prediction using time series analysis to predict future price action.
5. Machine and Supervised Learning to optimize algorithm performance.
6. Data visualization of classification, clustering and algorithm results.

1. **Data description** :

QuantConnect has made data freely available for over &quot;400 TB tick resolution data … That library covers US equities, options, futures, fundamentals, CFD, and forex markets dating back to 1998. There&#39;s a total of 29,000+ stocks, 100+ currency pairs, 70+ CFD contracts, and more.&quot;2

As someone who has been struggling to update and maintain local SQL databases of financial data off and on for 15 years, this is an unbelievable resource. While the data is on the could environment, the sheer size of might make working with some time frames (i.e. years or decades) and resolutions (i.e. tick level) difficult.

1. **How data will you be analyzed** :

1. Clustering of differing trading betas, potentially to protect portfolio value in adverse trading environments.

1. Prediction using time series analysis to predict future price action.
2. Machine and Supervised Learning to optimize algorithm performance.

1. **Anticipated difficulties** :

I plan on using the online platform QuantConnect as much as possible to leverage integrated data access and libraries via its online IDE and docker image. However, while QuantConnect has dozens on popular Python libraries loaded automatically with its Docker image, I can foresee scenarios where I will not be able to import other libraries that are not available.  If this is the case I will likely have today download the open source LEAN Engine that QuantConnect runs on run on a local Virtual Machine (VM).

Another potential difficulty is the limited computing power of the free QuantConnect accounts, limited to 1 x 4GHz Core and 8GB RAM.3  I can increase this to 4 x 4GHz Cores and 12GB RAM for $20/month3 but if this is still not sufficient I will again have to resort to a local VM.

Another potential difficulty is the sheer amount of data, I imagine many strategies will only be able to be backtested on limited timeframes (i.e. only backtest year 2018) and subject underliers (i.e. only &quot;APPL&quot; stock or &quot;ES&quot; future, rather than basket of numerous underliers) with potentially less granular resolution (i.e. days, minutes rather than ticks).

1. **Project timeline suggested** :

- **Weeks 1-2.9** : Refine Project Proposal
- **Week 3-4** : Test limits/abilities of cloud environment/setup local environment if required. EDA, begin testing trading ideas working toward functioning algorithm (e.g. code works)
- **Week 5** : Working with functional algorithm(s), work towards profit viability
- **Week 6** : Backtesting and optimization of algorithm(s)
- **Week 7** : Live trade of algorithm(s), organize results, update blog, prepare presentation
- **Week 8** : Present results and make plans for future research

**References** :

1: Real Finance. (2019) Algo Trading Dominates 80% Of Stock Market | Seeking Alpha. Retrieved September 16, 2019, from [https://seekingalpha.com/article/4230982-algo-trading-dominates-80-percent-stock-market](https://seekingalpha.com/article/4230982-algo-trading-dominates-80-percent-stock-market)

2: Thapar, Nitin. (2019) The Unconventional Guide To The Best Websites For Quants. Retrieved September 16, 2019, from [https://blog.quantinsti.com/unconventional-guide-best-websites-quants/](https://blog.quantinsti.com/unconventional-guide-best-websites-quants/)

3: QuantConnect. (2019) Upgrade your Plan | Support QuantConnect - QuantConnect.com. Retrieved September 16, 2019, from [https://www.quantconnect.com/upgrade](https://www.quantconnect.com/upgrade)

4: QuantConnect - Wikipedia. (2019) Retrieved September 16, 2019, from [https://en.wikipedia.org/wiki/QuantConnect](https://en.wikipedia.org/wiki/QuantConnect)

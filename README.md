# Ethereum-Data-Analysis
This repository contains tools, scripts, and notebooks for analyzing Ethereum return data to uncover trends, visualize price activity, and derive actionable insights for researchers, developers, and Ethereum enthusiasts.

## Tech Stack
- **Languages:** Python (Pandas, NumPy)

- **Visualization:** Plotly, Matplotlib, Seaborn

- **Data Sources:** yfinance, fredapi,

- **Tools:** Jupyter Notebooks,

## Analysis


### Coverting Prices to Returns
We'll model and approach the time series ethereum price data to be stationary. Stationary assumes that the statistics of the process, such as the series Mean and Variance, do not change over time. This assumption allows to build a model that aims to forcast the future valueof ETH.

However, ETH's prices are not stationary. Not only does ETH's price change over time, but There are observable trends or seasonality. So, we'll be transforming the prices into returns, attempting to make the time series stationary.

Other benefits of using returns, rather than prices, is the normalization. Allowing for the comparison of various return series, which would prove rather difficult since the volatility of ETH's price is rather high.

**For this analysis I'll use two types of returns:**

- **Simple return:** The simple return is the weighted sum of the return. Defined as:

$$
R_t = (P_t - P_{t-1})/P_{t-1} = P_t/P_{t-1}-1 
$$

- **Log return:** The log return is the sum of the return over time. Defined as:

$$
r_t = log(P_t/P_{t-1}) = log(P_t) - log(P_{t-1})
$$

**$P_t$ is the price of ETH at time $t$.**


### Adjusting Returns for Inflation
Since our data spans from November 9, 2017 inflation is given consideration. Inflation is the general rise of the prices level of an economy over time. The pair were meassuring is `ETH-USD`, and  while ETH doesn't experience inflation like traditional assets, USD is being used to meassure the value of ETH.

**There is more than one way to approach the return adjustment for inflation:**

1. **Adjust ETH Return for USD Inflation:**
    - Adjust the historical ETH-USD return by the U.S. CPI to see the real (inflation-adjusted) return of ETH:
    
$$
R^r_t = \frac{1+R_t}{1+\pi_t}-1
$$

> **Where $R^r_t$ is the real return, $R_t$ is the time $t$ simple return, $\pi_t$ stands for the inflation rate.**


2. **On-Chain ETH Consumer Price Index (Synthetic Index):**
    - We could create our own synthetic Ethereum CPI by tracking the price of on-chain goods or services over time, such as:

        - Gas fees (in gwei)

        - ETH-based stablecoin peg maintenance

        - ETH-denominated NFT or DeFi prices

        - Average tx costs in ETH

**For the purpose of the analysis, I'll adjust ETH's return for USD inflation.**

### Calculating Realized Volatility
Realized volatility is a statistical measure of how much an asset’s price actually fluctuated over a given period.

$$
RV = \sqrt{\sum_{i=1}^{T} r^2_t}
$$

<br>


>#### Why Do We Calculate It?
>1. Measure of Risk
>Higher volatility = more uncertainty in price
>
>       **Investors and analysts use it to evaluate the riskiness of holding the asset**
>
>2. Compare Across Assets
>You can compare ETH’s realized volatility to BTC, gold, or stocks
>
>       **Helps decide where to allocate capital depending on risk appetite**
>
>3. Strategy Design
>Quant strategies, option pricing models (like Black-Scholes), and portfolio managers all need volatility estimates
>
>       **It’s critical in value-at-risk (VaR), Sharpe ratio, and stop-loss modeling**
>
>4. Market Behavior Insight
>Volatility clusters (periods of high volatility grouped together) can signal structural changes, market fear, or major catalysts
>
>       **For example: realized vol spikes after major crashes or macroeconomic announcements**
>
>5. Validate or Refute "Crypto = Risky" Narratives
>You can show, with data, how ETH volatility evolves — does it stabilize over time? Or still behave like a high-beta asset?


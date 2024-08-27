# Overview of Robo-advisor

This robo-advisor is designed to recommend the optimal portfolio for each type of risk-averse investor.

## Inputs —

Users are asked to provide their:

- Initial investment
- Investment horizon
- Monthly additional investment
- Required returns
- [Risk tolerance level](https://cafnr.missouri.edu/divisions/division-of-applied-social-sciences/research/investment-risk-tolerance-assessment/)

## Outputs —

Based on the information provided, the robo-advisor will recommend the distribution of investments across various asset types:

- Gold
- Bonds
- Shares
- ETFs

---

# How does it work?

- ***Data collection & preprocessing***
    
    The daily price data is retrieved from `yfinance` and processed to exclude non-trading days. The data includes the prices of gold, recommended bonds & ETFs, and all S&P500 stocks.
    
    *Note: Due to data availability, this robo-advisor focuses exclusively on US financial assets.*
    
- ***Finding optimal portfolio***
    - Calculate risks and returns for all the assets
    - Find the highest-yield stocks, together with gold and recommended bonds & ETFs
    - Generate samples of different asset distributions.
    - Find the optimal portfolio for each level of risk tolerance
        - *Risk averse:* The minimum-risk portfolio
        - *Risk neutral:* The maximum risk-return tradeoff portfolio
            
            $max(\frac{R_{portfolio} - R_f}{std_{portfolio}})$
            
        - *Risk lover:* The most aggressive portfolio

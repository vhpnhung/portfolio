# Introduction

## Data source

The dataset is retrieved from Kaggle → 

The original data provider is a real estate listing website - https://www.realtor.com/

Latest update: Mar 2024

[USA Real Estate Dataset](https://www.kaggle.com/datasets/ahmedshahriarsakib/usa-real-estate-dataset)

---

# EDA

## Discovering

- The dataset contains 1 csv file *(2,001,666 entries $\times$ 10 columns)*
    
    
    - `status` - Housing status, either ‘for sale’ or ‘ready to build’
    - `bed` - The number of bedrooms
    - `bath` - The number of bathrooms
    - `acre_lot` - Land size in acres
    - `house_size` - Living space in square feet
    - `city` - The city that the house is located in
    - `state` - State name
    - `zip_code` - Postal code of the area
    - `prev_sold_date` - The latest date that the house was sold
    - `price` - Housing price
    

## Cleaning & Joining

- ***Cleaning***
    - Convert data
        
        `prev_sold_date` is converted from `object` into `datetime`
        
    - Remove unnecessary column(s)
        
        `zip_code` is removed in this case
        
    - Remove null values
        
        
        - Because there are houses that had never sold previously, entries with null values in `prev_sold_date` is not eliminated.
        - Lands in ‘ready to build’ status didn’t have defined number of bedroom and bathroom, so entries with that status but without `bed` and `bath` information are accepted
        
        <aside>
        📊 1,050,751 entries remaining
        
        </aside>
        
    - Remove outliers
        
        
        Employ IQR on columns whose `dtype = ‘float64’`
        
        <aside>
        📊 720,524 entries remaining
        
        </aside>
        
    - Remove invalid values
        
        
        Delete entries with the year of `pre_sold_date` > 2023
        
        <aside>
        📊 720,524 entries remaining
        
        </aside>
        
    - Winsorize
        
        The 1% of the lowest value and the 1% of the highest values are replaced.
        
- ***Structuring***
    - Add a measure column `land_size`
        
        Replace `acre_lot` by column `land_size = acre_lot * 43560` *(convert unit from acre to square feet)*
        
    - Add a measure column `price_per_sqr_ft`
        
        `price_per_sqr_ft` = `price` / `land_size`  as a measure of ‘price per square feet land area’
        
- ***Joining***
    
    
    To explore the impact of geographic factors to housing market, latitude and longitude of U.S. states are merged.
    
    Data source: Kaggle                                     →    [US State and Territory Latitude and Longitude data](https://www.kaggle.com/datasets/tennerimaheshwar/us-state-and-territory-latitude-and-longitude-data)

  ## Identifying Trends & Insights

| ***Exploratory questions*** | ***Findings*** |
| --- | --- |
| How many houses are for sale, and are ready to build? | For sale: 699,579
Ready to build: 20,945 |
| Compare the prices between houses that are for sale, and those are ready to build | Average price of houses for sale is $325.5K, which is lower than that of houses to build ($509.7K) |
| Which states have the greatest (lowest) number of houses listed? | Pennsylvania (Colorado) |
| How many houses that had been sold before? *(resale house)* | There are 445,401 resale houses, accounting for 61.82% houses in the dataset |
| Which states have the greatest (lowest) proportion of new houses to total houses for sale? | While all houses in Puerto Rico, Virgin Islands and Wyoming are new (100%), the percentages for Delaware (26.63%) and Virginia (44.08%) are the lowest among 16 states observed. |
| How many bedrooms and bathrooms in general?
Which types are the most expensive (cheapest)? | 3-to-4-bedroom and 2-bathroom houses are most preferred

## Hypothesis Testing

> ***Q1. Did multi-floor houses have higher price than one-floor houses?***
> 
- Assumptions
    - Multi-floor houses are those where house size > land size
    - As sample size is large enough, central limit theory holds.
- **two-sample t-test *(test of difference in means)*** is used, significance level = 0.05
    - $H_0: \mu_{P_{multi}} = \mu_{P_{single}}$ *(there is no difference between prices of multi- and single-floor)*
    - p-value = 0.8 → Fail to reject the null hypothesis 
    → Average prices of multi- and single-floor are the same.

> ***Q2. Is there any relationship between house price and other field?***
> 
- **t-test** is used for correlation test, significance level = 0.01

# Overview

Airbnb was born in 2007 when two hosts welcomed three guests to their San Francisco home, and has since grown to over 5 million hosts who have welcomed over 1.5 billion guest arrivals in almost every country across the globe. Every day, hosts offer unique stays and experiences that make it possible for guests to connect with communities in a more authentic way.

This analysis aims to provide a vision where data and information empower communities to understand, decide and control the role of renting residential homes to tourists in Barcelona.

# Data source

[Barcelona Airbnb listings - Inside Airbnb](https://www.kaggle.com/datasets/zakariaeyoussefi/barcelona-airbnb-listings-inside-airbnb)


---

# Preprocessing

**Conducted by Python. Please visit the file named `preprocessing.ipynb`.**

- Drop null values
- Drop unnecessary columns
    
     *e.g., `zipcode`*
    
- Convert data types
    
    Convert data type of some columns, e.g., `host_is_superhost` from `object` to `boolean`, & `price` from `object` to `float`.
    

*Conducted in Power BI*

- Create measures in Power BI
    - Measure to calculate **Occupancy rate** - that is, the percentage of occupied rooms in a property at a given time *(1 year in this project)*
    - Measure to compute **Listings per host**

---

# Dashboard

**The Power BI report file is uploaded in this folder. Please visit the files named `report`.**

- There are more than **9,700 hosts** with 20,000 accommodations in Barcelona, in which *Superhosts* account for only **21.74%**.
- Most of accommodations are **serviced apartments.**

> *An Airbnb Superhost is a host who Airbnb recognizes for providing excellent hospitality and high-quality accommodations.*
> 
- Eixample, Ciutat Vella, and Sants-Montjuïc are the top three districts with the highest number of Airbnb listings in Barcelona.

- **None** of the top 10 districts by number of listings have high occupancy levels.

> *I calculate occupancy rate as:      $OccupanyRate = 1-\frac{Availability365}{365}$*
> 
- Additionally, **4 out of the 5** districts with the highest occupancy rates have relatively **low average prices** compared to the overall average price of accommodations in Barcelona.
- Visitors tend to rent entire accommodations and private rooms rather than shared rooms.

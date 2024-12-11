# Power-Outage-Data-Analysis

### By David Oh

## Introduction

This project will delve into data about data points on individual power outages. There is data on location, time, date, duration, cuase, expenses, and more. Understanding what kinds of factors contribute to how severe or long a power outage can be extremely useful to predict and even possibly prevent future outages.

Therefore, the question I will try to answer is: what factors contribute most to the severity/downtime of power outages? I will mainly be focusing on data in relation to location, time, date, duration, and cause. The dataset includes 1534 rows, which correspond to 1534 individual outages, and 57 columns. 

The relevant columns of the dataset for my analysis include: 'OBS', 'POSTAL.CODE', 'NERC.REGION', 'CLIMATE.REGION', 'CLIMATE.CATEGORY', 'OUTAGE.START.DATE', 'OUTAGE.START.TIME', 'OUTAGE.RESTORATION.DATE', 'OUTAGE.RESTORATION.TIME', 'CAUSE.CATEGORY', 'CAUSE.CATEGORY.DETAIL', 'TOTAL.SALES', 'HURRICANE.NAMES', 'OUTAGE.DURATION', 'DEMAND.LOSS.MW', 'CUSTOMERS.AFFECTED.' (more details on columns below). 


## Data Cleaning and Exploratory Data Analysis

To begin analysis we must first comb through the data, making it more viable for analysis:

### Data Cleaning
The steps I took to clean the data are as follows:

* Retrieve the relevant columns using pandas dataframes.
* Replace null values with specifically np.nan in python.
    * Many of the null values in the data set were entered as 'NA' and not np.nan
* Combine start/end date and start/end time values into date time objects for easier manipulation
|   OBS | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     | CLIMATE.CATEGORY   | OUTAGE.START.DATE   | OUTAGE.START.TIME   | OUTAGE.RESTORATION.DATE   | OUTAGE.RESTORATION.TIME   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   TOTAL.SALES |   HURRICANE.NAMES |   IND.PRICE |   TOTAL.CUSTOMERS |   OUTAGE.DURATION |   RES.SALES |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED | OUTAGE.START        | OUTAGE.RESTORATION   |
|------:|:--------------|:--------------|:-------------------|:-------------------|:--------------------|:--------------------|:--------------------------|:--------------------------|:-------------------|:------------------------|--------------:|------------------:|------------:|------------------:|------------------:|------------:|-----------------:|---------------------:|:--------------------|:---------------------|
|     1 | MN            | MRO           | East North Central | normal             | 2011-07-01 00:00:00 | 17:00:00            | 2011-07-03 00:00:00       | 20:00:00                  | severe weather     | nan                     |   6.56252e+06 |               nan |        6.81 |           2595696 |              3060 | 2.33292e+06 |              nan |                70000 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |
|     2 | MN            | MRO           | East North Central | normal             | 2014-05-11 00:00:00 | 18:38:00            | 2014-05-11 00:00:00       | 18:39:00                  | intentional attack | vandalism               |   5.28423e+06 |               nan |        6.49 |           2640737 |                 1 | 1.58699e+06 |              nan |                  nan | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |
|     3 | MN            | MRO           | East North Central | cold               | 2010-10-26 00:00:00 | 20:00:00            | 2010-10-28 00:00:00       | 22:00:00                  | severe weather     | heavy wind              |   5.22212e+06 |               nan |        6.07 |           2586905 |              3000 | 1.46729e+06 |              nan |                70000 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |
|     4 | MN            | MRO           | East North Central | normal             | 2012-06-19 00:00:00 | 04:30:00            | 2012-06-20 00:00:00       | 23:00:00                  | severe weather     | thunderstorm            |   5.78706e+06 |               nan |        6.71 |           2606813 |              2550 | 1.85152e+06 |              nan |                68200 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |
|     5 | MN            | MRO           | East North Central | warm               | 2015-07-18 00:00:00 | 02:00:00            | 2015-07-19 00:00:00       | 07:00:00                  | severe weather     | nan                     |   5.97034e+06 |               nan |        7.74 |           2673531 |              1740 | 2.02888e+06 |              250 |               250000 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |


### Univariate Analysis




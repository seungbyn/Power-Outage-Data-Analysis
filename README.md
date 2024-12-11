# Power-Outage-Data-Analysis

## By David Oh

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

### Univariate Analysis




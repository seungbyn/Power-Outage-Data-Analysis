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

The following histogram depicts the distribution of power outages by outage duration (in minutes). This allows us to visually see how most of the power outages are within the 0-20,000 minute range, while there are some outliers that are beyond this. 

<iframe
  src="assets/duration_hist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The following bar graph depicts the distributions of outage duration by climate region.
<iframe
  src="assets/region_bar_graph.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Bivariate Analysis
The followng dataframe shows the mean outage duration for each of the climate regions. There seems to a general trend of lower mean outage durations for geographic locations that are more inland in the United States

|CLIMATE            |   OUTAGE.DURATION |
|------------------:|------------------:|
|Central            |          2701.13  |
|East North Central |          5352.04  |
|Northeast          |          2991.66  |
|Northwest          |          1284.5   |
|South              |          2846.1   |
|Southeast          |          2217.69  |
|Southwest          |          1566.14  |
|West               |          1628.33  |
|West North Central |           696.562 |

Central	2701.130890
East North Central	5352.043796
Northeast	2991.656977
Northwest	1284.500000
South	2846.100917
Southeast	2217.686667
Southwest	1566.136364
West	1628.331707
West North Central	

### Interesting Aggregates
The following pivot table shows the total outage duration for each of the climate regions and climate categories that exist within the data. Although there does not seem to be a huge correlation, generally the areas that are geographically closer to the borders of the United States have higher total outage duration. 

|CLIMATE            |   cold |   normal |   warm |
|------------------:|---------:|-------:|-------:|
|Central            | 181991 |   273579 |  60346 |
|East North Central | 249614 |   432240 |  51376 |
|Northeast          | 442527 |   407039 | 179564 |
|Northwest          |  41110 |    35947 |  79652 |
|South              | 112712 |   409084 |  98654 |
|Southeast          |  76818 |   169851 |  85984 |
|Southwest          |  11981 |    13030 | 112809 |
|West               | 111051 |   106236 | 116521 |
|West North Central |   1000 |      199 |   9946 |

## Assessment of Missingness

### NMAR Analysis

Looking through the columns I believe that the 'DEMAND.LOSS' may be not missing at random. Some data values in this column are missing however, I suspect it may be due to the nature of the data collection itself. It may difficult to measure how much power was lost if there was outage that shuts down all measurement instruments. To better understand this it would be helpful to collect data on whether or not measurement instruments were also out of commission during each specific outage. 

### Missingness Dependency

While testing for data that may be missing at random, I examined the missing values within the "HURRICANE.NAMES' column. The results of the permutation test regarding this missingness dependency made it clear that the missing values in 'HURRICANE.NAMES' was dependent on the column 'CAUSE.CATEGORY.' The following plot shows the distribution of values of the "CAUSE.CATEGORY' column when 'HURRICANE.NAMES' was non-null vs null. 

<iframe
  src="assets/hurricane_true.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/hurricane_false.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## Hypothesis Testing

To explore my main question further I chose to run a hypothesis test to answer the question if the power outage duration was any different for the western regions United States versus the eastern regions of the United States. 

Null Hypothesis: The average power outage durations in the Western Regions of the United States is the same as the average power outage durations in the Eastern Regions of the United States

Alternate Hypothesis: The average power outage durations in the Western Regions of the United States is less than the average power outage duration in the Eastern Regions of the United States

Ultilizing these hypotheses and a p-value of 0.01 I ran the hypothesis test. To accomplish this I utilized a permutation test which examined the two sample sets that were split in relation to the 'CLIMATE.REGION' column. The two sets were split into the following.
* WEST: 'CLIMATE.REGION' was one of the following: ['West', 'Northwest', 'Southwest', 'West North Central']
* EAST: 'CLIMATE.REGION' was one of the following: ['Northeast', 'Southeast', 'Central', 'East North Central']

With these two sample populations I was able to find the mean outage duration of each population to find the observed statistic (west outage duration mean - east outage duration mean) which I then compared to the 500 testing statistics. I found that this test would lead me to reject the null hypothesis with a p-value of 0.0. This meant that there was a definite difference in the mean outage duration of the two populations. 

## Framing a Prediction Problem

### Problem Identification

The prediction probelm that I chose to pursue was a regression model. The response variable that I am trying to predict is outage duration, and I will evaluate the model's efficacy with R^2 as I feel that this will better show if my model is tracking patterns in the data. Accuracy was also an option to evaluate my model, however, given the relatively complex trends within the data it may be difficult to utilize pure accuracy to evaluate my model. 

In terms of what data points are viable to use at the "time of prediction," I ruled out 'DEMAND.LOSS' and 'OUTAGE.RESTORATION.TIME' as they are both only available data after the power outage has passed. I was considering to rule out 'CAUSE.CATEGORY' as it may be hard to evaluate the cause of the outage at the time of prediction, however, looking at the data it seems that the majority of outages are caused by weather or sabatoge. I feel that discerning between these two at the time of prediction may be possible or very likely. 

## Baseline Model

My first model utilized two columns to predict the duration of outages. These two columns were 'CAUSE.CATEGORY' and 'OUTAGE.START.' With the 'CAUSE.CATEGORY' column I simply utilized one hot encoding as it was a nominal data type, however with the 'OUTAGE.START' column there were more steps involved. This column was of datetime objects, therefore I had to convert it to a quantative value that made sense in context. To do this I first transforms the datetime objects into numbers which corresponded to the hour of the time (24 hour time). I then used a Binarizer with a threshold of 12 to distinguish if the start time was during the AM or PM time of day. 

This model did not perform that well evaluated using the R^2 score. There was a relatively low R^2 score that came with this model, which means that the variance of the predicted outage durations and the actual outage duration were not very similar. While, discouraging to see this, I took these findings to better tweak my model and increase its efficacy. 

## Final Model

For my final model I ultimately used two columns as features for the model. These columns included 'CLIMATE.REGION' and 'CAUSE.CATEGORY.' It may seem that two features is lacking to capture the complexity of the case, however, I found that with the more features I added the more my model seemed to struggle. Therefore, I choose to test different features to see which had the most correlation with outage duration and it turned out that 'CLIMATE.REGION' and 'CAUSE.CATEGORY' worked the best. 

By using cross validation and GridSearchCV I was able to find that one hot encoding 'CLIMATE.REGION' and using a dictionary to encode the values in 'CAUSE.CATEGORY' oridnally worked relatively well compared to my previous model. I was able to give more weight to certain values in 'CAUSE.CATEGORY' to better aid my model in its predicitons. 

Overall, the efficacy of my model increased almost tenfold after implementing these changes based on the R^2 score evaluation. However, my model is far from perfect and I am aiming to continue to work on the model further in pursuit of better hyperparameters and/or transformations. 

## Fairness Analysis

To analyze the fairness of my model I decided to use the two groups I used in my hypothesis test. I divided my test groups into east and west regions and tested my model on each population separately. I then found the absolute difference in R^2 score for each population to use as my observed statistic. 

I then used another permutation test to test if the two populations were different. This test gave me 500 test statistics, which I compared with my observed statistic to get a p-value. The p-value for my observed statistic turned out to be around 0.4, which is not enough to reject the null hypothesis. This ultimately means that my model is also fair in terms of the two groups, performing similarly for both populations. 





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

### Bivariate Analysis
The followng dataframe shows the mean outage duration for each of the climate regions. There seems to a general trend of lower mean outage durations for geographic locations that are more inland in the United States

PUT IMAGE HERE

### Interesting Aggregates
The following pivot table shows the total outage duration for each of the climate regions and climate categories that exist within the data. Although there does not seem to be a huge correlation, generally the areas that are geographically closer to the borders of the United States have higher total outage duration. 

ADD GRAPH HERE

## Assessment of Missingness

### NMAR Analysis

Looking through the columns I believe that the 'DEMAND.LOSS' may be not missing at random. Some data values in this column are missing however, I suspect it may be due to the nature of the data collection itself. It may difficult to measure how much power was lost if there was outage that shuts down all measurement instruments. To better understand this it would be helpful to collect data on whether or not measurement instruments were also out of commission during each specific outage. 

### Missingness Dependency

While testing for data that may be missing at random, I examined the missing values within the "HURRICANE.NAMES' column. The results of the permutation test regarding this missingness dependency made it clear that the missing values in 'HURRICANE.NAMES' was dependent on the column 'CAUSE.CATEGORY.' The following plot shows the distribution of values of the "CAUSE.CATEGORY' column when 'HURRICANE.NAMES' was non-null vs null. 

PLOT HERE


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

My prediction model will try to predict the outage duration given some information of the outage (location, time, customers served, price)

Clearly state your prediction problem and type (classification or regression). If you are building a classifier, make sure to state whether you are performing binary classification or multiclass classification. Report the response variable (i.e. the variable you are predicting) and why you chose it, the metric you are using to evaluate your model and why you chose it over other suitable metrics (e.g. accuracy vs. F1-score).

Note: Make sure to justify what information you would know at the “time of prediction” and to only train your model using those features. For instance, if we wanted to predict your final exam grade, we couldn’t use your Final Project grade, because the project is only due after the final exam! Feel free to ask questions if you’re not sure.

## Baseline Model

Describe your model and state the features in your model, including how many are quantitative, ordinal, and nominal, and how you performed any necessary encodings. Report the performance of your model and whether or not you believe your current model is “good” and why.

Tip: Make sure to hit all of the points above: many projects in the past have lost points for not doing so.

## Final Model

State the features you added and why they are good for the data and prediction task. Note that you can’t simply state “these features improved my accuracy”, since you’d need to choose these features and fit a model before noticing that – instead, talk about why you believe these features improved your model’s performance from the perspective of the data generating process.

Describe the modeling algorithm you chose, the hyperparameters that ended up performing the best, and the method you used to select hyperparameters and your overall model. Describe how your Final Model’s performance is an improvement over your Baseline Model’s performance.

Optional: Include a visualization that describes your model’s performance, e.g. a confusion matrix, if applicable.

## Fairness Analysis

Clearly state your choice of Group X and Group Y, your evaluation metric, your null and alternative hypotheses, your choice of test statistic and significance level, the resulting 
p
-value, and your conclusion.

Optional: Embed a visualization related to your permutation test in your website.





![Plot of x vs y](assets/missing_hist.pngplot.png)





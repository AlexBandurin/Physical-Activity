# Physical Activity Analysis: Project Overview

In this analysis, we will be exploring data from the Physical Activity and Transit Survey (PAT). It is a survey conducted by the NYC Department of Health and Mental Hygiene in 2010-2011 consisting of 2 major parts: a telephone survey of physical activity and health (N=3811) and a weeklong accelerometer device study (N=679) . Note: A sub-sample of participants of the phone survey participated in the accelerometer study.

[Data source](https://www.nyc.gov/site/doh/data/data-sets/physical-activity-and-transit-survey-public-use-data.page)
Python Version: Python 3.10.9
Packages: pandas, numpy, matplotlib, seaborn, sklearn

## This analysis consists of several parts:

- Select a subset of features, based on presense of NaNs, multicollinearity, and gaunged significance.
- Perform correlation analysis between them to gain insight about health, habits, and physical activity 
- Select a subset of the previous feature set, and perform cluster analysis using the K means and Gaussian Mixture Model algorithms to 
  better understand the patterns in the data.
  
## Correlation Analysis

### Data Preparation:

- Convert datasets form SAS format to CSV and load into dataframes
- Select a 34 features from the 281 total features in the original datasets
- Merge the 2 surveys into one dataframe
- Rename columns/features for clarity. 

### Correlation matrix

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/heatmap.jpeg"  width="60%" height="60%">

## Clustering Analysis

### Data Preparation:

- From the features explored up until this point, select 17 to perform cluster analysis with. These are:
   <font size="2">
  - Health (reported health status)
  - Age
  - MVPA (All minutes per week of all physical activity)
  - Diet (diet)
  - Exer_routine (Regular exercise routine)
  - Gym_member (had gym membership in the last year)
  - Screentime (Categories of hours per weekday of television or computer use during weekdays)
  - phys7 (During the last 7 days, did you do anysports, fitness, or recreational activities?)
  - Tobacco (Tobacco use)
  - BMI (Body Mass Index (BMI), categorical)
  - Cholesterol (High cholesterol)
  - Diabetes (Presense of diabetes)
  - Hypertension (Hypertension)
  - Sleep (Number of days in the last 30 days the participant did not have enough rest or sleep)
  - Mental (Number of days in the last 30 days the participant didn't have good mental health)
  - Counts_avg (*"The accelerometer was set to record activity in 10 second increments – this number represents an average of all counts on all valid           days")
  - moderate_avg (Average number of Moderate minutes on all valid days, measured by accelerometer)
  </font> 
 - Handle missing values. Since we are running a clustering algorithm, there can be no NaNs within the dataset. This was done using imputation with mean      and mode values.

### K Means

For **K-Means** algorithm, Elbow was method used to determine optimal number of clusters to use:

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/elbow.jpeg"  width="60%" height="60%">

Thus, 2 clusters were used, and the data was separated in the following manner as shown in the bar plot:

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/bar.jpeg"  width="60%" height="60%">

For **GMM** algorithm, Akaike information criterion (AIC) and Bayesian information criterion (BIC) was used to determine number of clusters, K:

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/GMM.jpeg"  width="60%" height="60%">

The algorithm was ran with 2 and 3 clusters, in the following manner:

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/bar2.jpeg"  width="60%" height="60%">

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/bar3.jpeg"  width="60%" height="60%">




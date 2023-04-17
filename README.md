# Physical Activity Analysis: Project Overview

In this analysis, we will be exploring data from the Physical Activity and Transit Survey (PAT). It is a survey conducted by the NYC Department of Health and Mental Hygiene in 2010-2011 consisting of 2 major parts: a telephone survey of physical activity and health (N=3811) and a weeklong accelerometer device study (N=679). Note: A sub-sample of participants of the phone survey participated in the accelerometer study.

[Data source](https://www.nyc.gov/site/doh/data/data-sets/physical-activity-and-transit-survey-public-use-data.page)

Python Version: 3.10.9
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

### K-Means

Elbow was method used to determine optimal number of clusters to use:

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/elbow.jpeg"  width="60%" height="60%">

Thus, 2 clusters were used, and the data was separated in the following manner as shown in the bar plot:

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/bar.jpeg"  width="60%" height="60%">

It seems like the algorithm divided people into those that are "Healthy" (cluster 2) and "Unhealthy" (cluster 1).

We could see that cluster 1 contains individuals with an average "Health" variable of 1.9, which is equivalent to "very good", while cluster 2 is at 2.9, which is just "good". Surprisingly, the average ages are very similar, with cluster 1 being a little older (as to be expected). 

Notable characteristics of Cluster 2 (Healthy):
- Slightly Better Diet 
- Much less screentime (about 2 hours, compared to Cluster 1's 3.5 hours average)
- Slightly lower BMI
- Participants with diabetes, hypertension, and high cholesterol: (43,9), (112,30), and (76,32) for clusters 1 and 2, respectively. So there are drastic differences in chronic conditions.
- Slightly better mental health.
- Better Sleep (2.5 days less bad sleep days during the last 30 days)

Now, as for physical activity, we see some very clear differences:

- An average of about 15,000 more average accelerometer counts (or over 60% more) in cluster 2.
- Over twice (!) (120% more) the average number of minutes of moderate physical activity intensity (as opposed to light and vigorous) on all valid days, measured by accelerometer for cluster 2.
- Over twice the number of people with an exerice routine in cluster 2

### Gaussian Mixture Model (GMM)

Akaike information criterion (AIC) and Bayesian information criterion (BIC) was used to determine number of clusters, K:

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/GMM.jpeg"  width="60%" height="60%">

To help us determine the right number of clusters to use, we will use 2 estimators of prediction error: Akaike information criterion (AIC) and Bayesian information criterion (BIC). These estimate the relative amount of information lost by a given model. The error will naturally go down with more clusters used, but, as we did with the K means algorithm, we will use the cluster that occurs after the 'steepest' decline in error on the graph. In this case, that number seems to be 4 or 3. 

Let us start with 3 clusters, then 4.


<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/bar2.jpeg"  width="60%" height="60%">

Cluster 1 stands out as the least healthy. It has the least reported health, worst physical health metrics, least sleep, and worst self-identified mental health. This cluster makes up 5% of the group.

Cluster 3 is healthiest, overall. It really stands out by its accelerometer indicators. Participants here have been the most active during the test week. These is the majority of people surveyed.

Cluster 2 is average. It is in between the 2 other clusters in all the health metrics. What stands out is that the age here is the highest, so it seems like the people that fall into this classification are moslty elderly, which makes sense.

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/bar3.jpeg"  width="60%" height="60%">

Cluster 4 is healthiest, overall. It has the highest reported "health", most exercise (most gym memberships, highest indicators of physical activity), the least screentime, slightly lower BMI.

Cluster 3 stands out as the least healthy in terms of mental health. Participants here got the least sleep, and are self-identified least mentally healthy. However, their exercise attributes are on average, are only second worst.

Cluster 1 is about second healthy, but it is also the oldest, and like with 3 clusters, it seems like this is the reason for the difference in health indicators.

It is difficult to pit a characteristic to cluster 2, so it is seems best to keep 3 clusters.

# Conclusion:

We conclude that K means is a better-suited clustering algorithm for our purposes as it is the most comprehensive for identifying distinctions between healthy and unhealthy individuals. Based on our analysis, it is clear that the most distuniushing characteristics correlated<font size="5"><sup>*</sup></font> with a healthy lifestyle are (in the order of decreasing correlation):

- Regular physical exercise (frequent moderate physical activity)
- Less screentime (computer or television during weekdays)
- More nights of good sleep
- A good diet
- Lower Body Mass Index
- Chronic Conditions

### Most of these factors are within an indivudual's control, which suggests that better health could be attained with better habits.

<font size="5"><sup>*</sup></font> It is very important to keep in mind that correlation does not mean causation. So, just because participants in the "healthy" cluster exhibited the aforementioned behaviours does not mean that their health was directly *caused* by them. 

##  Feature Key: 

**Age:**
     
| Label|Meaning (age in years)|
| --- | --- |
|1|18-24|
|2|25-44|
|3|45-64|
|4|65+  |

**Health:**

| Label|Meaning|
| --- | --- |
|1|Excellent|
|2|Very good|
|3|Good|
|2|Fair|
|3|Poor|

The following variables use the same labeling (Excellent-Poor): 
-  **Diet:**

**Exer_routine:**

|Label|Meaning|
| --- | --- |
|1|Yes|
|2|No|

The following variables use the same labeling (Yes/No): 
- **"Gym_member**
- **Cholesterol**
- **Diabetes**
- **Hypertension**

**Screentime:**

| Label|Meaning|
| --- | --- |
|1|Never|
|2|½ hour or less|
|3|1-1 ½ hours|
|4|2-2 ½ hours|
|5|3-3 ½ hours|
|6|4-4 ½ hours|
|7|5-5 ½ hours|
|8|6-6 ½ hours|
|9|7-7 ½ hours|
|10|8-9 ½ hours|
|11|10-12 hours|

**Tobacco**

| Label|Meaning|
| --- | --- |
|1|Most days (or all days)|
|2|Some days|
|3|Never|

**BMI**

| Label|Meaning|
| --- | --- |
|1|Underweight|
|2|Normal weight|
|3|Overweight|
|4|Obese|

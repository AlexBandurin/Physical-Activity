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

### Create a correlation matrix

<img src="https://github.com/AlexBandurin/Physical-Activity/blob/master/heatmap.jpeg"  width="60%" height="60%">

## Clustering Analysis




# Bellabeat Fitness Data Analysis Case Study

![Bellabeat](https://github.com/bhagyashri49641/Bellabeat_data_analysis/blob/main/bellabeat.png?raw=true)

This analysis is an optional Capstone project from the [Google Data Analytics Professional Certificate](https://www.coursera.org/professional-certificates/google-data-analytics) on Coursera. 
##### Author: Bhagyashri mane

##### Date: February 26, 2025

##### [Tableau Dashboard](insert link)

##### [Tableau Story Presentation to Skateholders](insert link)


## Background:
Bellabeat is a high-tech manufacturer of beautifully designed health-focused smart products for women  since 2013. Inspiring and empowering women with knowledge about their own health and habits, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for females.
The Bellabeat keeps track of health data related to user's activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions.

The co-founder and Chief Creative Officer, Urška Sršen is confident that an analysis of non-Bellebeat consumer data (ie. FitBit fitness tracker usage data) would reveal more growth opportunities.

The company has 5 focus products: Bellabeat app, leaf, time, spring and bellabeat membership. Our team has been asked to focus on a Bellabeat product and analyze smart device usage data to gain insight into how people already use their smart devices. The insights we discover will then help guide the marketing strategy for the company. 

#

_I followed below six steps of the data analysis process:_

### ❓ [Ask](#1-ask)
### 💻 [Prepare](#2-prepare)
### 🛠 [Process](#3-process)
### 📊 [Analyze](#4-analyze)
### 📋 [Share](#5-share)
### 🧗‍♀️ [Act](#6-act)

## 1. Ask
💡 **BUSINESS TASK: Analyze FitBit Fitness Tracker App data to gain insights into how consumers are using the FitBit app and discover trends and insights for Bellabeat marketing team.**

Primary stakeholders: Urška Sršen and Sando Mur, executive team members.

Secondary stakeholders: Bellabeat marketing analytics team.

### Business Objectives:
- What are the trends identified?
- How could these trends apply to Bellabeat customers?
- How could these trends help influence Bellabeat marketing strategy?

## 2. Prepare 

### Tools:
Python for Data Cleaning, Data Transformation, Data Visualisation and Data Analysis

### Data Set:
The data set is publicly available on [Kaggle](https://www.kaggle.com/arashnic/fitbit).

The dataset has 18 CSV. The data also follow a ROCCC approach:

- Reliability: The data is from 30 FitBit users who consented to the submission of personal tracker data and generated by from a distributed survey via Amazon Mechanical Turk. 
- Original: The data is from 30 FitBit users who consented to the submission of personal tracker data via Amazon  Mechanical Turk.
- Comprehensive: Data minute-level output for physical activity, heart rate, and sleep monitoring. While the data tracks many factors in the user activity and sleep, but the sample size is small and most data is recorded during certain days of the week. 
- Current: Data is from March 2016 to May 2016. Data is not current so the users habit may be different now. 
- Cited: Unknown. 

⛔ The dataset has limitations:

- Only 30 user data is available. The central limit theorem general rule of n≥30 applies and we can use the t test for statstic reference. However, a larger sample size is preferred for the analysis.
- Upon further investigation with ```n_distinct()``` to check for unique user Id, the set has 33 user data from daily activity, 24 from sleep and only 8 from weight. There are 3 extra users and some users did not record their data for tracking daily activity and sleep. 
- For the 8 user data for weight, 5 users manually entered their weight and 3 recorded via a connected wifi device (eg: wifi scale).
- Most data is recorded from Tuesday to Thursday, which may not be comprehensive enough to form an accurate analysis. 







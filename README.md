# CASE STUDY: Bellabeat Data Analysis Case Study

![Bellabeat](https://github.com/bhagyashri49641/Bellabeat_data_analysis/blob/main/bellabeat.png?raw=true)

This analysis is a Capstone project from the [Google Data Analytics Professional Certificate](https://www.coursera.org/professional-certificates/google-data-analytics) on Coursera. 
##### Author: Bhagyashri mane

##### Date: February 26, 2025


#
_The 6 steps of Data Analysis are used to present this analysis:_


### STEP 1. Ask
### 1.1 Background:
Bellabeat is a high-tech manufacturer of beautifully-designed health-focused smart products for women since 2013. Inspiring and empowering women with knowledge about their own health and habits, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for females.

The Bellabeat keeps track of health data related to user's activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions.

The company has 5 focus products: Bellabeat app, leaf, time, spring and bellabeat membership. Our team has been asked to focus on a Bellabeat product and analyze smart device usage data to gain insight into how people already use their smart devices. The insights we discover will then help guide the marketing strategy for the company. 

### 1.2 Business task: 
Analyze FitBit Fitness Tracker App data to gain insights into how consumers are using the FitBit app and discover trends and insights for Bellabeat marketing team.

### 1.3 Business Objectives:
- What are the trends identified?
- How could these trends apply to Bellabeat customers?
- How could these trends help influence Bellabeat marketing strategy?

### 1.4 Deliverables:
- A clear summary of the business task
- A description of all data sources used
- Documentation of any cleaning or manipulation of data
- A summary of analysis
- Supporting visualizations and key findings
- High-level content recommendations based on the analysis
  
### 1.5 Key Stakeholders:
- Urška Sršen: Bellabeat’s cofounder and Chief Creative Officer (Primary stakeholder).
- Sando Mur: Mathematician, Bellabeat’s cofounder and key member of the Bellabeat executive team (Primary stakeholder).
- Bellabeat marketing analytics team: A team of data analysts guiding Bellabeat's marketing strategy(Secondary stakeholders).



## STEP 2. PREPARE 

### 2.1 Information on Data Source:
The data set is publicly available on [Kaggle: FitBit Fitness Tracker Data](https://www.kaggle.com/arashnic/fitbit).
Generated by respondents from a distributed survey via Amazon Mechanical Turk between 12 April 2016 to 12 May 2016.
The dataset has 18 CSV.
30 FitBit users who consented to the submission of personal tracker data.
Data collected includes : information about daily activity, steps,distance, heart rate and sleep monitoring that can be used to explore user's habits.


### 2.2 Limitations of Data Set:
- Data collected from year 2016. Users' daily activity, fitness and sleeping habits, diet and food consumption may have changed since then, hence data may not be timely or relevant.
- Sample size of 30 female FitBit users is not representative of the entire female population.
- As data is collected in a survey, hence unable to ascertain the integrity or accuracy of data.
- Upon further investigation with ```n_distinct()``` to check for unique user Id, the set has 33 user data from daily activity, 24 from sleep and only 8 from weight. There are 3 extra users and some users did not record their data for tracking daily activity and sleep. 
- For the 8 user data for weight, 5 users manually entered their weight and 3 recorded via a connected wifi device (eg: wifi scale).
- Most data is recorded from Tuesday to Thursday, which may not be comprehensive enough to form an accurate analysis.


### 2.3 Is Data ROCCC?
A good data source is ROCCC which stands for Reliable, Original, Comprehensive, Current, and Cited.

- Reliable - LOW - Not reliable as it only has 30 respondents >>The data is from 30 FitBit users who consented to the submission of personal tracker data and generated by from a distributed survey via Amazon Mechanical Turk. 
- Original - LOW - Third party provider (Amazon Mechanical Turk) >> The data is from 30 FitBit users who consented to the submission of personal tracker data via Amazon  Mechanical Turk.
- Comprehensive - MED - Parameters match most of Bellabeat's products' parameters >> Data minute-level output for physical activity, heart rate, and sleep monitoring. While the data tracks many factors in the user activity and sleep, but the sample size is small and most data is recorded during certain days of the week. 
- Current - LOW - Data is 8 years old and is not relevant >>Data is from March 2016 to May 2016. Data is not current so the users habit may be different now. 
- Cited - LOW - Data collected from third party, hence unknown
Overall, the dataset is considered bad quality data and it is not recommended to produce business recommendations based on this data.


### 2.4 Data Selection:
The following file is selected and copied for analysis.
    • dailyActivity_merged.csv
    
### 2.5 Tools:
- R for Data Cleaning, Data Transformation and Data Analysis
- Tableau for Data Visualisation

refer RAnalysis file for PROCESS and ANALYZE step
## STEP 3: PROCESS
- In this step we check for Data Integrity ,accuracy, dupicates, incomplete, nulls.
- Data Validation: includes checking datatypes , data ranges and other constraints.
- Data manipulation to make it more organised
- refer RAnalysis file for PROCESS and ANALYZE step

## STEP 4: ANALYZE
- make sense of the given data
-refer RAnalysis file for PROCESS and ANALYZE step
  
## STEP 5: SHARE
In this step, we are creating visualizations and communicating our findings based on our analysis.
##### [Tableau Dashboard](https://public.tableau.com)

##### [Tableau Story Presentation to Skateholders](https://public.tableau.com)

-Shared my case study report on: kaggle and Github

## STEP 6: ACT






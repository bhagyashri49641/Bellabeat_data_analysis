# CASE STUDY: Bellabeat Data Analysis Case Study

![Bellabeat](https://github.com/bhagyashri49641/Bellabeat_data_analysis/blob/main/bellabeat.png?raw=true)

This analysis is a Capstone project from the [Google Data Analytics Professional Certificate](https://www.coursera.org/professional-certificates/google-data-analytics) on Coursera. 
##### Author: Bhagyashri mane
##### Date: February 26, 2025


## The 6 steps of Data Analysis are used to present this analysis
### ❓ [Ask](#1-ask)
### 💻 [Prepare](#2-prepare)
### 🛠 [Process](#3-process)
### 📊 [Analyze](#4-analyze)
### 📋 [Share](#5-share)
### 🧗‍♀️ [Act](#6-act)

## 1. Ask
### 1.1 Background:
Bellabeat is a high-tech manufacturer of beautifully designed health-focused smart products for women since 2013. Inspiring and empowering women with knowledge about their own health and habits, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for females.

The Bellabeat keeps track of health data related to user's activity, sleep, stress, menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions.

The company has 5 focus products: Bellabeat app, leaf, time, spring, and bellabeat membership. Our team has been asked to focus on a Bellabeat product and analyze smart device usage data to gain insight into how people already use their smart devices. The insights we discover will then help guide the company's marketing strategy. 

### 1.2 Business task: 
Analyze FitBit Fitness Tracker App data to gain insights into how consumers are using the FitBit app and discover trends and insights for Bellabeat marketing team.

### 1.3 Business Objectives:
- What are the trends identified?
- How could these trends apply to Bellabeat customers?
- How could these trends help influence Bellabeat's marketing strategy?

### 1.4 Deliverables:
- A clear summary of the business task
- A description of all data sources used
- Documentation of any cleaning or manipulation of data
- A summary of analysis
- Supporting visualizations and key findings
- High-level content recommendations based on the analysis
  
### 1.5 Key Stakeholders:
- Urška Sršen: Bellabeat’s co-founder and Chief Creative Officer (Primary stakeholder).
- Sando Mur: Mathematician, Bellabeat’s cofounder and a key member of the Bellabeat executive team (Primary stakeholder).
- Bellabeat marketing analytics team: A team of data analysts guiding Bellabeat's marketing strategy(Secondary stakeholders).



## 2. Prepare
[Back to Top](#author-bhagyashri-mane)

### 2.1 Information about Data Source:
The data set is publicly available on [Kaggle: FitBit Fitness Tracker Data](https://www.kaggle.com/arashnic/fitbit).
Generated by respondents from a distributed survey via Amazon Mechanical Turk between 12 April 2016 to 12 May 2016.
The dataset has 18 CSV.
30 FitBit users who consented to the submission of personal tracker data.
Data collected includes: information about daily activity, steps, distance, heartrate and sleep monitoring that can be used to explore user's habits.


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
- dailyActivity_merged.csv
- sleepDay.csv
- weightLogInfo.csv
- hourly(steps,calories,intensities)_merged csv
    
### 2.5 Tools:
- R for Data Cleaning, Data Transformation and Data Analysis
- Tableau for Data Visualization

## 3. Process
[Back to Top](#author-bhagyashri-mane)

- In this step, we check for Data Integrity, accuracy, duplicates, incomplete, and nulls.
- Data Validation: includes checking data types, data ranges, and other constraints.
- Data manipulation to make it more organized
- merge data if needed
- refer FitbitAnalysis.Rmd file for process steps using R.

### 3.1 Check For NA
```{r}
sum(is.na(daily_activity))
sum(is.na(sleep_day))
sum(is.na(weight))
sum(is.na(hourly_steps))
sum(is.na(hourly_intensities))
sum(is.na(hourly_calories))
# sum(is.na(heartrate))
## We will leave the NA. The NA belongs to "Fat" data of different dates.
```
### 3.2 Check for duplicates and remove duplicates
```{r}
cat("Number of duplicate rows in daily_activity before removal:", nrow(daily_activity[duplicated(daily_activity),]), "\n")
daily_activity <- daily_activity[!duplicated(daily_activity),]
cat("Number of duplicate rows in daily_activity after removal:", nrow(daily_activity[duplicated(daily_activity),]), "\n") 
# Confirm duplicates removed
sum(duplicated(daily_activity))
```
#### Repeat the above code chunk for all csv that we need

### 3.3 Convert character columns to date
[Back to Process](#3-process)

```{r}
daily_activity$ActivityDate <- as.Date(daily_activity$ActivityDate, format = "%m/%d/%Y")
sleep_day$SleepDay <- as.Date(sleep_day$SleepDay, format = "%m/%d/%Y")
weight$Date <- as.Date(weight$Date, format = "%m/%d/%Y")
```
#### Use the below date format to extract hours from hourly data
```{r} 
hourly_steps$ActivityHour <- as.POSIXct(hourly_steps$ActivityHour, format = "%m/%d/%Y %I:%M:%S %p") # Convert ActivityHour to POSIXct (24-hour format )
hourly_steps$Date <- as.Date(format(hourly_steps$ActivityHour, format = "%m/%d/%Y")) # Extract Date
hourly_steps$Hour <- format(hourly_steps$ActivityHour, format = "%H")  # Character # Extract the hour
hourly_steps$Hour <- as.numeric(hourly_steps$Hour)            # Convert to numeric (0-23)
write_csv(hourly_steps, "hourly_steps.csv")                 # Check result
```
### 3.4 Add a new column for the weekdays
[Back to Process](#3-process)
```{r}
daily_activity <- daily_activity %>% mutate( weekday = weekdays(as.Date(ActivityDate, "%m/%d/%Y")))
```
### 3.5 Clean column names
[Back to Process](#3-process)
```{r}
daily_activity <- daily_activity %>% clean_names()
sleep_day <- sleep_day %>% clean_names()
weight <- weight %>% clean_names()

hourly_steps <- hourly_steps %>% clean_names()
hourly_intensities <- hourly_intensities %>% clean_names()
hourly_calories <- hourly_calories %>% clean_names()

## View updated column names
colnames(daily_activity)
colnames(sleep_day)
colnames(weight)
colnames(hourly_steps)
colnames(hourly_intensities)
colnames(hourly_calories)

```
### 3.6 merge daily_activity, sleep and weight data
[Back to Process](#3-process)

```{r}
merged1 <- merge(daily_activity,sleep_day,
                  by.x = c("id", "activity_date"), 
                  by.y = c("id", "sleep_day"),
                  all=TRUE)
merged_data <- merge(merged1, weight, 
                      by.x = c("id", "activity_date"), 
                      by.y = c("id", "date"),
                      all=TRUE)

#save csv for future use
write_csv(merged_data, "merged_data.csv")

# Check head, NA, duplicates, distinct id in merged data.
head(merged_data)
glimpse(merged_data)
sum(is.na(merged_data))
sum(duplicated(merged_data))
n_distinct(merged_data$id)

# similarly merge hourly steps, intensity and calories data (for code check FitbitAnalysis.Rmd file)
```
### 3.7 Examine the dataset and check if all 30 users are unique.
[Back to Process](#3-process)

#### Check to see if all users are unique.We supposed to have 30 users or 30 IDs. So We have 3 extra from daily activity, 6 less from the sleep day table, and 22 less from the weight table. 
```
n_distinct(daily_activity$id)
n_distinct(sleep_day$id)
n_distinct(weight$id)
```
#### Since weight table only has 8 users enter their information. Let's take a look at how they enter the information. 5 users are manually reporting the weight and 3 uers are reporting it with a connected device - wifi connected scale. 
```
weight %>% 
  filter(is_manual_report == "True") %>% 
  group_by(id) %>% 
  summarise("Manual Weight Report"=n()) %>%
  distinct()

weight %>% 
  filter(is_manual_report == "False") %>% 
  group_by(id) %>% 
  summarise("Manual Weight Report"=n()) %>%
  distinct()
```
## 4. Analyze
[Back to Top](#author-bhagyashri-mane)

- make sense of the given data
- refer FitbitAnalysis.Rmd file for analyzing steps using R.

### 4.1 Summary
Check min, max, mean, median and any outliers. Avg weight is 135 pounds with BMI of 24 and burn 2050 calories. Avg steps is 10200, max is almost triple that 36000 steps. Users spend on avg 12 hours a day in sedentary minutes, 4 hours lightly active, only half hour in fairly+very active! Users also gets about 7 hour of sleep. 
```
merged_data %>%
  dplyr::select(
         total_steps,
         total_distance,
         very_active_minutes,
         fairly_active_minutes,
         lightly_active_minutes,
         sedentary_minutes,
         calories,
         total_minutes_asleep,
         total_time_in_bed,
         weight_kg,
         bmi
         ) %>%
  na.omit() %>%
  summary()

hourly_merge %>%
  dplyr::select(
                hour,
                step_total,
                calories,
                total_intensity,
                )%>%
  na.omit() %>%
  summary()
```
![summary](link of screenshot)

### 4.2 Active Minutes:
[Back to Analyze](#4-analyze)
Percentage of active minutes in the four categories: very active, fairly active, lightly active and sedentary. From the pie chart, we can see that most users spent 81.3% of their daily activity in sedentary minutes and only 1.74% in very active minutes. 
```
percentage <- data.frame(
  level=c("Sedentary", "Lightly", "Fairly", "Very Active"),
  minutes=c(sedentary_percentage,lightly_percentage,fairly_percentage,active_percentage)
  )


plot_ly(percentage, labels = ~level, values = ~minutes, type = 'pie',textposition = 'outside',textinfo = 'label+percent',
        marker = list(colors = c("#FF4500", "#1E90FF", "#32CD32", "#FFD700"))) %>%
          layout(title = 'Activity Minutes Percentage',
          xaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE),
          yaxis = list(showgrid = FALSE, zeroline = FALSE, showticklabels = FALSE)
          )
```
![newplot](link to pie chart)


The American Heart Association and World Health Organization recommend at least 150 minutes of moderate-intensity activity or 75 minutes of vigorous activity, or a combination of both, each week. That means it needs an daily goal of 21.4 minutes of FairlyActiveMinutes or 10.7 minutes of VeryActiveMinutes.

In our dataset, **30 users** met fairly active minutes or very active minutes.
```
active_users <- merged_data %>%
  filter(fairly_active_minutes >= 21.4 | very_active_minutes>=10.7) %>% 
  group_by(id) %>% 
  count(id) 
glimpse(active_users)
```

### 4.3 Noticeable Day:
[Back to Analyze](#4-analyze)

The bar graph shows that there is a jump on Saturday: user spent LESS time in sedentary minutes and take MORE steps. Users are out and about on Saturday. 

![image](sedentary minutes vs weekday)
![image](total steps vs weekday)



### 4.4 Hourly Steps:
[Back to Analyze](#4-analyze)

Let's look at how active the users are per hourly in total steps. From 5PM to 7PM the users take the most steps. 
```{r}
avg_daily_steps <-  hourly_merge %>%
                    filter(step_total > 0) %>% 
                    group_by(hour) %>%
                    summarise(avg_steps = mean(step_total, na.rm = TRUE), .groups = "drop")
glimpse(avg_daily_steps)


plot6 <-  ggplot(data=avg_daily_steps, aes(x=hour, y=avg_steps, fill=avg_steps ))+
  geom_bar(stat="identity")+
  geom_text(aes(label = round(avg_steps)), vjust = -0.5, size = 3)+
  scale_fill_gradientn(colors = c("red", "orange", "yellow", "green"))+
  scale_x_continuous(breaks = 0:23) +  # Ensure all hours (0 to 23) are displayed
  labs(title="Hourly Steps", x="Hour of the Day", y="Average Steps") +
  theme_minimal()
ggsave("Average_Hourly_Steps.png", plot = plot6, width = 10, height = 5, dpi = 200)

```
![image](Avg steps vs hour of the day)


How active the users are weekly in total steps. Tuesday and Saturdays the users take the most steps. 
```
```{r}
# Weekly analysis of Steps 
# calculate the avg of all over steps for each weekday here group only by weekday
avg_weekday_steps <- merged_data %>%
                      group_by(weekday) %>%
                      summarise(avg_weekly_steps = mean(total_steps, na.rm = TRUE), .groups = "drop")
glimpse(avg_weekday_steps)

Average_Weekday_Steps <-  ggplot(data = avg_weekday_steps, aes(x=weekday, y=avg_weekly_steps, fill=weekday))+ 
                          geom_bar(stat="identity")+
                          geom_text(aes(label = round(avg_weekly_steps, 1)), vjust = -0.5, size = 3) +
                          labs(title="Average Weekday Steps", y="Average Steps")+
                          theme_minimal()
ggsave("Average_Weekday_Steps.png", plot = Average_Weekday_Steps, width = 8, height = 6, dpi = 200)
```
![image](avg steps per week)




### 4.5 Interesting Finds:
[Back to Analyze](#4-analyze)

The more active that you're, the more steps you take, and the more calories you will burn. This is an obvious fact, but we can still look into the data to find any interesting. Here we see that some users who are sedentary, take minimal steps, but still able to burn over 1500 to 2500 calories compare to users who are more active, take more steps, but still burn similar calories.

```
plot9 <-
  ggplot(data=merged_data, aes(x=total_steps, y = calories, color=sedentary_minutes))+ 
  geom_point()+ 
  stat_smooth(method=lm)+
  scale_color_gradient(low="steelblue", high="orange")+
  labs(title="The Relationship Between Calories and Total Steps", x="Total Steps", y="Calories Burned")+
  theme_minimal()

ggsave("calories_vs_total_steps.png", plot = plot9, width = 8, height = 6, dpi = 300) #plot9

```
![image](calories vs steps)

Comparing the four active levels to the total steps, we see most data is concentrated on users who take about 5000 to 15000 steps a day. These users spent an average between 8 to 13 hours in sedentary, 5 hours in lightly active, and 1 to 2 hour for fairly and very active. 

![image](active_minutes_vs_steps)

According to [this healthline.com article](https://www.healthline.com/nutrition/how-many-calories-per-day#average-calorie-needs), moderately active woman between the ages of 26–50 needs to eat about 2,000 calories per day and moderately active man between the ages of 26–45 needs 2,600 calories per day to maintain his weight. Comparing the four active levels to the calories, we see most data is concentrated on users who burn 2000 to 3000 calories a day. These users also spent an average between 8 to 13 hours in sedentary, 5 hours in lightly active, and 1 to 2 hour for fairly and very active. Additionally, we see that the sedentary line is leveling off toward the end while fairly + very active line is curing back up. This indicate that the users who burn more calories spend less time in sedentary, more time in fairly + active. 

![image](active_minutes_vs_calories)

### 4.6 Sleep:
[Back to Analyze](#4-analyze)

According to article: [Fitbit Sleep Study](https://blog.fitbit.com/sleep-study/#:~:text=The%20average%20Fitbit%20user%20is,is%20spent%20restless%20or%20awake.&text=People%20who%20sleep%205%20hours,the%20beginning%20of%20the%20night.), 55 minutes are spent awake in bed before going to sleep. We have 13 users in our dataset spend 55 minutes awake before alseep. 

```
awake_in_bed <- mutate(sleep_day, AwakeTime = total_time_in_bed - total_minutes_asleep)
awake_in_bed <- awake_in_bed %>% 
  filter(AwakeTime >= 55) %>% 
  group_by(id) %>% 
  arrange(AwakeTime, desc=TRUE) 
```

How about calories vs asleep? Do people sleep more burn less calories? Plotting the two variables we can see that there is not much a correlation. 
```
ggplot(data=merged_data, aes(x=total_minutes_asleep, y = calories, color=total_minutes_asleep))+ 
  geom_point()+ 
  xlab("Total Minutes Alseep")+
  geom_smooth(method = 'loess', formula = 'y ~ x', color = '#005FCC') +
  scale_color_gradient(low="steelblue", high="orange")+
  labs(x = "total minutes asleep", y = "calories", title="Calories vs Total Minutes Asleep")
```
![image](Calories vs Total Minutes Asleep)

we will check is there any effect of sedentary minutes and time asleep
```
plot13 <- ggplot(data = merged_data, aes(x = sedentary_minutes, y = total_minutes_asleep, color=total_minutes_asleep)) +
  geom_point() +
  scale_color_gradient(low="steelblue", high="orange")+
  geom_smooth(method = 'loess', formula = 'y ~ x', color = '#005FCC') +
  labs(title = "Total Minutes Asleep vs Sedentary minutes", x = 'sedentary minutes', y = 'minutes asleep') +
  theme_classic()
ggsave("total_minutes_asleep_vs_Sedentary_minutes.png", plot = plot13, width = 10, height = 6, dpi = 300) #plot13
```
![image](total_minutes_asleep_vs_Sedentary_minutes)

  
## 5. Share
[Back to Top](#author-bhagyashri-mane)

- Fitbit data analysis Dashboard: [Tableau Dashboard](https://public.tableau.com)

- Shared my case study report on: [Github](https://github.com/bhagyashri49641/Bellabeat_data_analysis)


## 6. Act
[Back to Top](#author-bhagyashri-mane)
 
Conclusion based on our analysis:
- Sedentary make up a significant portion, 81% of users daily active minutes. Users spend on avg 12 hours a day in sedentary minutes, 4 hours lightly active, and only half-hour in fairly+very active! 
- We see the most change on Saturday: users take more steps, burn more calories, and spend less time sedentary. Sunday is the most "lazy" day for users. 
- 54% of the users who recorded their sleep data spent 55 minutes awake in bed before falling asleep.
- Users take the most steps from 5 PM to 7 PM
Users who are sedentary take minimal steps and burn 1500 to 2500 calories compared to users who are more active, take more steps, but still burn similar calories.

Marketing recommendations to expand globally:

##### 🔢  Obtain more data for an accurate analysis, encouraging users to use a wifi-connected scale instead of manual weight entries. 

##### 🚲  Educational healthy style campaign encourages users to have short active exercises during the week, longer during the weekends, especially on Sunday where we see the lowest steps and most sedentary minutes.

##### 🎁  Educational healthy style campaign can pair with a point-award incentive system. Users completing the whole week's exercise will receive Bellabeat points on products/memberships.

##### 🏃‍♂️ The product, such as Leaf wellness tracker, can beat or vibrate after a prolonged period of sedentary minutes, signaling the user it's time to get active! Similarly, it can also remind the user it's time to sleep after sensing a prolonged awake time in bed.



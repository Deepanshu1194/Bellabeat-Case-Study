# Bellabeat-Case-Study
Bellabeat- a high-tech manufacturer of health-focused products for women, working on the fitbit dataset which was collected from Kaggle.com and will try to find trends and key insights to help the stakeholders to make data driven decisions.
# 1. Ask

Guiding questions
 
* What is the problem you are trying to solve: The objective of the analysis is to identify t rends in non-Bellabeat smart device usage which can be applied to a Bellabeat product.

* How can your insights drive business decisions: It is expected that the insights would reveal more opportunities for growth, thus, provding high-level recommendations that will inform Bellabeat marketing strategy.

Key tasks

**Identify the business:**

  + Trends in smart device usage
  + How these trends apply to bellabeat customers
  + How these trends will influence Bellabeat marketing strategy
  
**Consider key stakeholders:**

  + Primary stakeholders: Bellabeat cofounders and other members of the executive team
  + Secondary stakeholders: Bellabeat Marketing Analytics team

**Deliverable:**

  + Clear statement of the business task: To better understand how consumers use non-Bellabeat smart devices by analyzing smart device usage data. Subsequently, apply the insights to Bellabeat customers and identify ways in which these insights can strategically influence the Bellabeat marketing strategy.

# 2. Prepare

Guiding questions

* Where is your data stored: Sršen recommended a public data that explores the daily habits of smart device users. This data was obtained from thirty eligible Fitbit users who consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. It also includes information about daily activity, steps, and heart rate that can be used to explore users’ habits. This data can be accessed on Kaggle FitBit Fitness Tracker Data (CC0: Public Domain), and is made av- ailable through Mobius.

* How is the data organized? Is it in long or wide format: The data consist of 18 .csv files of which 15 are in long (each row is one time point per subject, i.e., each subject has data in multiple rows) format while 3 are in wide (each data subject has a single row with multiple columns to hold values of various attributes of the subject) format. The data sets consists of quantitative, qualitatative, discrete, continuous and ordinal observations in a structured format with numeric, string, date-time and boolean data types. Further information about the data can be obtained from fitabase data dictionary.

* Are there issues with bias or credibility in this data? Does your data ROCCC: There are challenges with bias and credibility in the data sets, and this challenges will be discussed below:

  + Reliable: The data is not reliable as the sample size does not reflect the population of active fitbit users in 2016. In 2016, the average number of active fitbit users was 23,200,000 link and only 30 individuals participated in the survey. While the sample size of 30 holds true according to the central limit theorem, at 90% confidence level and with a 5% margin of error, assuming a 50% response distribution, a minimum sample size of 271 would have been required to accurately reflect the population of Fitbit users in 2016. Also, there is a potential sampling bias in the data as the demography of Fitbit users was not made available. Bellabit smart devices cater exclusively to women; therefore, insights generated from Fitbit data may not be appl* icable to Bellabit customers.

  + Original: Though the data was made available by a third party, Mobius, it is original as the source of the data can be verified link.

  + Comprehensive: The data is not comprehensive as it does not contain all the critical information needed to answer the question posed in the business task, e.g., demographic information is missing.

  + Current: The data is not current as it is from 2016 and might not reflect how users currently use fitbit devices.

  + Citation: Furberg, R., Brinton, J., Keating, M., & Ortiz, A. (2016). Crowd-sourced Fitbit datasets 03.12.2016 - 05.12.2016 Zenodo.- https://doi.org/10.5281/zenodo.53894

* How are you addressing licensing, privacy, security, and accessibility: It is a public data set with licence - https://creativecommons.org/publicdomain/zero/1.0/, and personally identifiable information has been anonymised.

* How did you verify the data’s integrity: Data integrity was verified by manually checking the 18 .csv files for accuracy, completeness, consistency, and trustworthiness.

* How does it help you answer your question: The data contains very useful information such as estimated energy expenditure (calories), sleep logs, food logs, activity logs etc., which would help answer the questions posed in the business task.

* Are there any problems with the data: Yes, the problems with the data hs been discussed previously.

Key tasks:

  + Download data and store it appropriately -- completed
  + Identify how it’s organized -- completed
  + Sort and filter the data -- completed

# 3. Process

Guiding questions

* What tools are you choosing and why: R notebook was chosen for the analysis because it is excellent for reproducing analysis, creating engaging visualizations, and deriving accurate insights from large amounts of data.

* Have you ensured your data’s integrity: The integrity of the data was continuously ensured throughout the analysis. This was done by ensuring that the data sets were valid, accurate, consistent, complete and aligned with the business objective.

* What steps have you taken to ensure that your data is clean: the data sets were cleaned using functions from data manipulation and cleaning packages such as "tidyverse", "skimr", "here", and "janitor". The data sets were inspected for duplicates and blank rows, null values were filtered from the data sets. The data types were formatted to align with business task, columns were inspected for mispelled words, mistyped numbers, extra spaces and characters as well as other cleaning actions.

* How can you verify that your data is clean and ready to analyze: The data cleaning activities were cross-examined against a data cleaning verification checklist. Checklist items such as sources of errors, null data, mispelled words, mistyped numbers, extra spaces and characters, duplicates, mismatched data types, and truncated data were reviewed and used to verify the cleaning activities.

* Have you documented your cleaning process so you can review and share those results: The data cleaning actions were documented.

Key tasks:

  + Check the data for errors -- completed
  + Choose your tools -- completed
  + Transform the data so you can work with it effectively -- completed
  + Document the cleaning process -- completed

Deliverable

* Documentation of any cleaning or manipulation of data

3.1 Select and Import Data on manual exploration of the data sets, it was noticed that the records and attributes in dailyCalories_merged.csv, dailyIntensities_merged.csv and dailySteps_merged.csv have all been merged into dailyActivity_merged.csv; thus, there will be no need to import these data sets.

To address the questions posed in the business task, the datasets dailyActivity_merged.csv, hourlySteps_merged.csv, heartrate_seconds_merged.csv, sleepDay_merged.csv, and weightLogInfo_merged.csv, hourlyIntensities_merged.csv will be employed for analysis. These datasets have pertinent information that can be leveraged to reveal trends in Fitbit device usage; therefore, they will be imported.

### Install and Load packages 

```{r load packages}
library(tidyverse)
library(skimr)
library(readr)
library(janitor)
library(lubridate)
```

### Import dataset to R
```{r load dataset}
daily_activity <- read_csv("/cloud/project/Dataset/dailyActivity_merged.csv")
hourly_steps <- read_csv("/cloud/project/Dataset/hourlySteps_merged.csv")
heartrate_seconds <- read_csv("/cloud/project/Dataset/heartrate_seconds_merged.csv")
sleep_day <- read_csv("/cloud/project/Dataset/sleepDay_merged.csv")
weight_log_info <- read_csv("/cloud/project/Dataset/weightLogInfo_merged.csv")
hourly_intensities <- read_csv("/cloud/project/Dataset/hourlyIntensities_merged.csv")
```
### Preview summary of dataset

```{r daily activity}
head(daily_activity)
str(daily_activity)
```

```{r hourly steps}
head(hourly_steps)
str(hourly_steps)
```

```{r heartrate seconds}
head(heartrate_seconds)
str(heartrate_seconds)
```

```{r sleep day}
head(sleep_day)
str(sleep_day)
```

```{r weight log info}
head(weight_log_info)
str(weight_log_info)
```

```{r hourly intensities}
head(hourly_intensities)
str(hourly_intensities)
```
### Data Cleaning

```{r Change Activity Date format from char to date type format}
daily_activity <- daily_activity %>% 
  mutate(ActivityDate = mdy(ActivityDate),
         Days = weekdays(ActivityDate))
glimpse(daily_activity)
```

```{r Check the discrepancy between the values of TotalDistance and TrackerDistance}
not_equal <- 0
for(i in 1: nrow(daily_activity)){
  if(daily_activity$TotalDistance[i] != daily_activity$TrackerDistance[i]){
    not_equal <- not_equal + 1
  }
}
cat("Total count of different entries:" ,not_equal, "\n" )
```
The "TotalDistance" attribute is the total kilometers tracked for each user while the "TrackerDistance" is the total kilmometers tracked by the fitbit device. It is expected that both entries will be the same, however, the attributes differed for 15 records. We will drop the "TotalDistance" atribute and work with TrackerDistance"in the analysis since it ewas genereted by the fitbit device.

```{r Drop the column names which is not required} 
daily_activity_new <- daily_activity %>% 
  select(-c(TotalDistance, LoggedActivitiesDistance)) %>% 
  clean_names()
```

```{r change_time_column}
hourly_steps_new <- hourly_steps %>%
  mutate(
    ActivityHour = mdy_hms(ActivityHour),
    Day = weekdays(ActivityHour))%>%
  clean_names()
glimpse(hourly_steps_new)
```

```{r Change Time column from character data type to date time format}
heartrate_seconds_new <- heartrate_seconds %>%
  mutate(
    Time = mdy_hms(Time),
    Day = weekdays(Time))%>%
  rename(heart_rate = Value)%>%
  clean_names()

glimpse(heartrate_seconds_new)
```

```{r check for Duplicates}
cat("Number of duplicates: ", sum(duplicated(sleep_day)), "\n")

sleep_day <- sleep_day %>%
  distinct()

cat("After dropping duplicates, number of duplicates: ", sum(duplicated(sleep_day)), "\n")
```

```{r Transform Sleep_day column from character data type to date time type}
sleep_day_new <- sleep_day %>%
  mutate(
    SleepDay = mdy_hms(SleepDay),
    Day = weekdays(SleepDay))%>%
  clean_names()

 glimpse(sleep_day_new)
```

```{r check for null values}
 cat("Number of nulls: ", sum(is.na(weight_log_info)), "\n")
 
 cat("Total number of rows: ", nrow(weight_log_info))
```
The dataset encompassing health metrics like weight and BMI is valuable, however we have concerns regarding its completeness. The IsManualReport column suggests that the weight data was voluntarily submitted, hinting at potentially irregular tracking by participants. A closer look at the ID and Date columns also indicates that weight tracking may not be reliable. To determine the extent of data completeness, we will compare the number of weight measurements per participant against the dataset's overall duration. This comparison will demonstrate the dataset's reliability.
 
```{r Determine the range of dates covered in the data}
 total_period <- range(as.Date(weight_log_info$Date, format="%m/%d/%Y"))
 days_in_period <- as.integer(total_period[2] - total_period[1]) + 1
```

```{r Group the data by participant and count the number of measurements entered}
 measurements_per_participant <- weight_log_info %>%
   group_by(Id) %>%
   summarise(Number_of_Measurements = n(), .groups = 'drop') %>%
   mutate(Days_in_period = days_in_period) %>%
   arrange(desc(Number_of_Measurements))
measurements_per_participant
```
As suspected, only a small subset of participants (8) recorded their weights throughout the month, with merely 3 doing so with enough regularity to estimate a weekly average. While this dataset may still hold value, its limitations due to sparse data will need to be kept in mind.

```{r Transform Date column from character data type to date time format, drop Fat and LogId columns}
 weight_log_info_new <- weight_log_info %>%
   mutate(
     Date = mdy_hms(Date),
     Day = weekdays(Date))%>%
   select(-c(Fat, LogId))%>%
   clean_names()
 
 glimpse(weight_log_info_new)
 
 cat("\n\n Any nulls left in the data: ", any(is.na(weight_log_info_new)))
```

```{r Transform Date column from character data type to date time format then clean up column names}
 hourly_intensities_new <- hourly_intensities %>%
   mutate(
     ActivityHour = mdy_hms(ActivityHour), 
     Day = weekdays(ActivityHour),
     hour = hour(ActivityHour))%>%
   clean_names()
 
 glimpse(hourly_intensities_new)
```
# 4. Analyze
Now after data cleaning process, now we have better understanding of the data we are working with. Our primary goal is to better understand how Bellabeat's customers are using the devices. There are few questions which will help us to make data driven decision.

Business task: To better understand how consumers use non-Bellabeat smart devices by analyzing smart device usage data. Subsequently, apply the insights to Bellabit customers and identify ways in which these insights can strategically influence the Bellabeat marketing strategy.

To answer these questions, we need to understand:

1. The number of days(range) in which respondents activities were tracked.
2. The frequency of fitbit smart device usage by the respondents.
3. How active are users on average?
4. Respondents utilizing all tracker features.
5. Respondents getting the required amount of sleep.

```{r The number of days(range) in which respondents activities were tracked}
 
number_of_days <- daily_activity_new %>%
select(activity_date) %>%
summarize(total_days = as.numeric(diff(range(activity_date))))
 
cat("Total number of tracked days: ", number_of_days$total_days)

time_period <- range(daily_activity_new$activity_date)
start <- format(time_period[1], "%d/%m/%Y")
end <- format(time_period[2], "%d/%m/%Y")
sprintf("Period of tracked activity: %s to %s", start, end)
```
To understand how frequent the respondents used fitbit tracker, the users will be categorized into:

Frequent users: respondents who used the smart devices more than 20 days in the survey period
Moderate users: respondents who used the devices between 15 and 20 days in this period
Occasional users: respondents who used the device for less than 15 days.

```{r The frequency of fitbit smart device usage by the respondents}

frequency_of_use <- daily_activity_new %>%
  group_by(id) %>%
  summarize(user_category = factor(case_when(
    n() >= 20 ~ "frequent_users",
    15 <= n() & n() < 20 ~ "moderate_users",
    n() < 15 ~ "occassional_users"
  ), levels = c("frequent_users", "moderate_users", "occassional_users"))) %>%
  mutate(user_category = user_category)

head(frequency_of_use)

utilization_trend <- frequency_of_use %>%
  group_by(user_category) %>%
  summarize(users = n())%>%
  mutate(percent = round(users/sum(users)*100, 2))

utilization_trend
```

How active are users on average?
Diving deeper into the data, We're interested in exploring the range and average number of daily steps taken by each user, along with the standard deviation. This analysis will provide insight into the users' activity levels.

```{r Analyzing steps per day}

#converting the ActivityDate column to Date format
daily_activity_new$ActivityDate <- as.Date(daily_activity$ActivityDate, format = "%m/%d/%Y")

#Summarize the daily average steps
daily_average_steps <- daily_activity_new %>%
  filter(total_steps > 0) %>%
  group_by(activity_date) %>%
  summarize(avg_steps = mean(total_steps),
            std_dev = sd(total_steps)
  )

#Find the max, min, overall average, and standard deviation of steps
max_average_steps <- round(max(daily_average_steps$avg_steps),0)
min_average_steps <- round(min(daily_average_steps$avg_steps),0)
mean_average_steps <- round(mean(daily_average_steps$avg_steps),0)
sd_average_steps <- round(sd(daily_average_steps$avg_steps),0)

#Display the results
print(paste("Max average steps: ", max_average_steps))
print(paste("Min average steps: ", min_average_steps))
print(paste("Mean average steps: ", mean_average_steps))
print(paste("Standard deviation of average steps: ", sd_average_steps))
```
Respondents utilizing all tracker features
To determine the number of users using all the tracker features (dailyActivity, heartrate_seconds, sleepDay, and weightLogInfo), the four tables will be merged.

```{r Respondents utilizing all tracker features}
daily_activity_update <- daily_activity_new %>%
  mutate(activity_date = as.POSIXct(activity_date))

heartrate_seconds_update <- heartrate_seconds1 %>%
  mutate(time = floor_date(time, unit = "days")) 

weight_log_info_update <- weight_log_info_new %>% 
  mutate(date = floor_date(date, unit = "days"))

merge_all <- daily_activity_update %>%
  inner_join(sleep_day_new, by = c("id", "activity_date" = "sleep_day")) %>%
  inner_join(weight_log_info_update, c("id", "day", "activity_date" = "date")) %>%
  inner_join(heartrate_seconds_update, by = c("id", "day", "activity_date" = "time"))

cat("\n Number of respondents utilizing all tracker features: ", n_unique(merge_all$id))
```
Respondents getting the required amount of sleep
The number of respondents getting the recommended amount of sleep 
```{r Respondents getting the required amount of sleep
merge1 <- inner_join(daily_activity_new, sleep_day_new, 
                     by = c("id" = "id", "activity_date" = "sleep_day", "days" = "day"))

head(merge1)
cat("\n\n Number of respondents using the sleep tracker: ", n_unique(merge1$id))
```
# 5. Share

**Guiding questions**

Despite limitations in the data such as the lack of demographical information and the limited numbers of respondents who participated in the survey, the analysis revealed valuable insights into how consumers were using fitbit smart device.

The stories from the data are as follows:

* Respondents activities were tracked for 30 days between 12/04/2016 and 12/05/2016
* 30 respondents were frequent users of Daily Activity tracker in fitbit smart device, i.e., they used the app 20 days or more in the survey period. 2 respondents are moderate users (used Daily Activity tracker between 15 and 20 days) while just one respondent was an occasional user ( used Daily Activity tracker for less than 15 days).
* Only 24 respondents utilized the sleep tracker while only 3 respondents utilized all smart device features.

**Deliverable** 
Supporting visualizations and key findings

Respondent Category Vs. Frequency of Use in Percentages
```{r Install the plotrix package}
install.packages("plotrix")
library(plotrix)


```{r Respondent Category Vs. Frequency of Use in Percentages}
pie3D(utilization_trend$percent,
      theta = 1.1,
      radius = 1.5,
      explode = 0.5,
      col = c("royalblue4", "skyblue3", "snow"),
      labels  = paste0(utilization_trend$percent, "%"),
      start = 0.5,
      main = "Daily Activity:Respondent Category Vs. Percentage Frequency of Use",
      mar = c(4,6,4,6))

```

```{r legend_plot, echo=FALSE}
legend("bottomright", 
       legend = utilization_trend$user_category,
       fill = c("royalblue4", "skyblue3", "snow"),
       title = "User Category",
       cex = 0.8)
```

```{r subtitle_2, echo=FALSE}
title(main = "",
      sub = "Trend in how frequent the respondents utilized daily activity tracker",
      line = -25)
```
Created scatterplot to show relationship between Total Daily Steps and Calories
```{r relationship between Total Daily Steps and Calories}
ggplot(data=daily_activity_new, aes(x=total_steps, y = calories, color=calories)) +
  geom_jitter() +
  geom_smooth(method="gam", formula = y ~s(x), color="red") +
  labs(title="Total Daily Steps and Calories Burned", subtitle="Data from 2016",caption="CC0: Public Domain, dataset made available through Mobius")

```
As expected, there was a trend where higher total steps correlates to more calories burned.


The analysis reveals that, on average, Bellabeat's customers walk about 9.7k steps daily, with individual averages ranging from 4.3k to 8.2k steps. The standard deviation indicates a relatively consistent step count among users daily. To gain a clearer understanding of these findings, we can visualize the average daily steps with a graph.

```{r Adding daily max and min values to daily_average_steps}
daily_average_steps <- daily_activity_new %>%
  filter(total_steps > 0) %>%
  group_by(ActivityDate) %>%
  summarize(
    avg_steps = mean(total_steps),
    max_steps = max(total_steps),
    min_steps = min(total_steps)
  )
```

```{r plot the results using ggplot2}
ggplot(data = daily_average_steps, aes(x = ActivityDate, y = avg_steps)) +
  geom_point() +
  geom_line (alpha = 0.3) +
  geom_smooth(method = "loess", se = FALSE, color = "blue") +
  labs(title = "Average Steps Per Day", x = "Day", y = "Average Steps")
```

```{r Percentage of Respondents getting the required amount of daily sleep}
pie3D(sleep_amt$percent,
      theta = 1,
      radius = 0.8,
      explode = 0.1,
      col = c("royalblue4", "skyblue3"),
      labels  = paste0(sleep_amt$percent, "%"),
      start = 1.7,
      main = "Recommended amount of sleep Vs. Percentage of Respondents",
      mar = c(4,6,4,6))
```

```{r legend_plot_1}
legend("bottomright", 
       legend = sleep_amt$sleep,
       fill = c("royalblue4", "skyblue3"),
       title = "Sleep",
       cex = 1)
```

```{r subtitle}
title(main = "",
      sub = "The percentage of Respondents getting or not getting the recommended sleep amount",
      line = -25)
```

# 6. Act

Significant limitations and constraints within the Fitbit smart device usage datasets may compromise the reliability of insights derived from the analysis for data-driven decision-making. Therefore, it is imperative to address these challenges before extending reliable insights to inform the Bellabeat smart device marketing strategy.

In this analysis, we explored data collected from Bellabeat users, covering a period from mid-April to mid-May.

Nonetheless, based on the trends identified in the datasets, I would recommend the following course of action to the Bellabeat executive team:

* Average daily steps: Only 7 out of 33 respondents achieved the recommended average daily amount of steps by the CDC; users should be prompted to take more steps daily for optimal health outcomes.

* There appears to be a correlation between the use of Bellabeat products and activity levels, though it's important to note that external factors like weather improvements could also influence these trends.

* Weekly amount of physical activity: Almost half of the respondents did not achieve the weekly recommended amount of physical activity. The marketing team can promote the need to track this feature as one of the benefits of owning a Bellabeat smart device.

* Tracker features: Only 3 respondents utilized all tracker features (dailyActivity, sleep, weight log, and heart rate). The benefits of each feature should be spotlighted in marketing campaigns.

# Call Centre Trends Analysis Dashboard

## Demo
1. [Power BI File](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task1_Call_Centre_Trend/Task1_Call_Centre_Trends.pbix)
2. [Screenshots](https://github.com/ksharma1908/pwc-virutal-internship/tree/main/Task1_Call_Centre_Trend/Screenshots) | [Screenshot 1](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task1_Call_Centre_Trend/Screenshots/screenshot_1.JPG) | [Screenshot 2](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task1_Call_Centre_Trend/Screenshots/screenshot_2.JPG) | [Screenshot 3](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task1_Call_Centre_Trend/Screenshots/screenshot_3.JPG)
3. [Data File](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task1_Call_Centre_Trend/01_Call_Center_Dataset.xlsx)

## Table of Contents
1. [Project Description](#project-description)
2. [Problem Statement](#problem-statement)
3. [Datasource](#datasource)
4. [Data Preparation](#data-preparation)
5. [Data Modeling](#data-modeling)
6. [Data Analysis (DAX)](#data-analysis-dax)
7. [Data Visualization (Dashboard)](#data-visualization-dashboard)
8. [Insights](#insights)
9. [Recommendations](#recommendations)
10. [Learnings](#learnings)

## Project Description
This Power BI project focuses on analyzing a comprehensive call center dataset to gain insights into call center performance, customer satisfaction, and emerging trends. The dataset includes features such as Call ID, Agent, Date, Time, Topic, Answered (Y/N), Resolved, Speed of Answer, Avg Talk Duration, and Satisfaction Rating.

Using Power BI's extensive range of visualizations and analytical capabilities, dynamic reports and dashboards were created to explore the dataset and uncover key trends. The analysis covers:

- **Call Volume and Distribution:** Analyzing the number of calls over time, identifying peak hours, and examining the distribution of calls across topics.
- **Call Center Performance:** Evaluating metrics such as speed of answer, average talk duration, and resolution rates.
- **Customer Satisfaction Analysis:** Examining satisfaction ratings to identify factors influencing customer satisfaction.
- **Trend Identification:** Spotting emerging trends or recurring issues based on call topics.

## Problem Statement
The goal of this project is to create a dashboard in Power BI that reflects all relevant Key Performance Indicators (KPIs) and metrics from the dataset to assist the call center manager in making data-driven decisions.

**Possible KPIs include:**
- Overall customer satisfaction
- Overall calls answered/abandoned
- Calls by time
- Average speed of answer
- Agent’s performance quadrant: average handle time vs. calls answered

## Datasource
- **Dataset:** Call Centre Trends
- **File:** `01 Call-Center-Dataset.xlsx`

## Data Preparation
The Call Centre Trends dataset contains 10 columns and 5000 rows of observations. The data preparation was performed in Power Query Editor within Microsoft Power BI Desktop.

### Data Cleaning Steps:
1. **Value Replacement:**
    - The "Answered (Y/N)" column was clarified by replacing "N" with "No" and "Y" with "Yes."

2. **Error Removal:**
    - Errors were identified and removed to ensure data accuracy and reliability.

3. **Data Type Validation:**
    - Validated each column to ensure correct data types were assigned.

4. **Datetime Transformation:**
    - The "AvgTalkDuration" column was transformed to focus specifically on time by removing date information.

## Data Modeling
After data cleaning and transformation, the dataset was modeled in Power BI. Key measures were created to drive insights and visualizations.

## Data Analysis (DAX)
The following DAX measures were used to analyze the data:

- **Total Calls:** `COUNT(Call_centre_data[Answered (Y/N)])`
- **Total Calls Answered:** `COUNTROWS(FILTER(Call_centre_data, Call_centre_data[Answered (Y/N)] = "Yes"))`
- **Total Calls Unanswered:** `COUNTROWS(FILTER(Call_centre_data, Call_centre_data[Answered (Y/N)] = "No"))`
- **Total Resolved Calls:** `COUNTROWS(FILTER(Call_centre_data, Call_centre_data[Resolved] = "Yes"))`
- **Total Unresolved Calls:** `COUNTROWS(FILTER(Call_centre_data, Call_centre_data[Resolved] = "No"))`
- **Average Satisfaction Rate:** `AVERAGE(Call_centre_data[Satisfaction rating])`
- **Average Speed of Answering (Seconds):** `AVERAGE(Call_centre_data[Speed of answer in seconds])`

## Data Visualization (Dashboard)
A Power BI dashboard was created to visualize the key insights from the Call Centre Trends data. The dashboard includes:

- **Call Volume Trends:** Analysis of call volume over time, highlighting peak hours and days.
- **Agent Performance:** Quadrant analysis showing agent performance based on average handle time and calls answered.
- **Customer Satisfaction:** Visualization of customer satisfaction ratings.
- **Issue Resolution:** Insights into resolved and unresolved calls.

## Insights
Key insights derived from the dashboard include:

1. **Satisfaction Rate:** The average customer satisfaction rating is 3.4 out of 5, indicating moderate satisfaction.
2. **Call Handling:** The majority of calls are answered, demonstrating effective call management.
3. **Agent Speed:** Diane is the quickest at answering calls, with a satisfactory rating of 3.4, indicating efficiency.
4. **Popular Topics:** Most calls are related to Streaming and Technical Support, suggesting areas needing more attention.
5. **Agent Performance:** Martha has the highest customer satisfaction, while Jim handles the most calls and resolves many issues.
6. **Issue Resolution:** Admin Support resolves the most calls, while Technical Support sees more unresolved issues.
7. **Resolution Trends:** January had the highest resolution rate, with a dip in February, followed by a rise in March.

## Recommendations
Based on the insights, the following recommendations were made:

1. **Train Agents Better:** Provide training to improve call handling and customer satisfaction.
2. **Direct Calls Smarter:** Utilize technology to route calls to the appropriate agents quickly.
3. **Get More Tech Help:** Hire or train more tech support staff to address the high volume of technical issues.
4. **Reward Good Work:** Incentivize agents who perform well in terms of speed, resolution, and satisfaction.
5. **Give Feedback Regularly:** Hold regular feedback sessions with agents to discuss performance and areas for improvement.
6. **Watch Call Trends:** Continuously monitor call types to proactively address common issues.
7. **Ask Customers for Feedback:** Regularly gather customer feedback post-call to identify areas of improvement.

## Learnings
Through this project, several new techniques and features in Power BI were learned and applied:

1. **Dynamic Date Message:**
    - Created a dynamic message that changes based on the selected date range.
   ```DAX
   selected dates = 
   VAR startdate = MIN('call center data'[Date])
   VAR enddate = MAX('call center data'[Date])
   RETURN 
    "Showing data from " & FORMAT(startdate, "MMMM dd, yyyy") & 
    " to " & FORMAT(enddate, "MMMM dd, yyyy")

2. **Month Calculation:**
    - Used the FORMAT function to extract and display the month from the date.
   ```DAX
   Month = FORMAT('call center data'[Date],"mmmm")

3. **Icons Implementation:**
    - Incorporated custom icons from FlatIcon to enhance the dashboard's visual appeal.

# Diversity & Inclusion Analysis Dashboard

## [Demo Live](https://project.novypro.com/pSXbkU)
1. [Power BI File](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task3_Diversity_and_Inclusion/Task3_Diversity_and_Inclusion.pbix)
2. [Screenshots](https://github.com/ksharma1908/pwc-virutal-internship/tree/main/Task3_Diversity_and_Inclusion/Screenshots) | [Screenshot 1](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task3_Diversity_and_Inclusion/Screenshots/screenshot_1.JPG) | [Screenshot 2](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task3_Diversity_and_Inclusion/Screenshots/screenshot_2.JPG)
3. [Data File](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task3_Diversity_and_Inclusion/Task3_Diversity_and_Inclusion.xlsx)

## Table of Contents
1. [What is Diversity & Inclusion?](#what-is-diversity-and-inclusion)
2. [Data Source](#data-source)
3. [Skills Demonstrated](#skills-demonstrated)
4. [Data Modeling](#data-modeling)
5. [Data Visualization](#data-visualization)
6. [Insights](#insights)
7. [Recommendations](#recommendations)
8. [What I Learned](#what-i-learned)

## What is Diversity & Inclusion?
Diversity and inclusion (D&I) refer to the policies and practices that promote the representation and participation of different groups of individuals, including those of different genders, races, ethnicities, abilities, sexual orientations, and other characteristics. A strong D&I strategy is essential for fostering innovation and improving employee satisfaction and productivity.

---

## Data Source
The dataset used in this project consists of 5,000 rows and 15 columns, providing demographic information, hiring practices, employee satisfaction scores, and retention rates. It was sourced from [Organization Name].

---

## Skills Demonstrated
- **Data Cleaning**
- **Data Inspection**
- **Data Transformation**
- **Data Visualization**
- **Statistical Analysis**

### Data Cleaning Process:
The following transformations were performed using Power Query:

1. Changed data types for `EmployeeID`, `Gender`, and `Ethnicity` columns.
    - Example: `Table.TransformColumnTypes(#"Promoted Headers",{{"EmployeeID", type text}, {"Gender", type text}, {"Ethnicity", type text}})`
2. Replaced values for ethnic groups to ensure consistency:
    - `Caucasian` → `White`
    - `African American` → `Black`
    - `Hispanic` → `Latinx`
3. Renamed columns:
    - `EmployeeID` → `Employee ID`
    - `JobTitle` → `Job Title`

### Conditional Columns Added:
1. **DiversityStatus:** `= IF('DiversityDataset'[Gender] = "Female", "Diverse", "Non-Diverse")`
2. **InclusionStatus:** `= IF('DiversityDataset'[EmployeeSatisfaction] > 3, "Included", "Not Included")`

---

## Data Modeling
Once the data was cleaned, the dataset was modeled in Power BI Desktop.

### Measures (DAX):
The following DAX measures were created for visualization:

- `Total Employees = COUNT(DiversityDataset[Employee ID])`
- `Diverse Employees = CALCULATE(COUNTA('DiversityDataset'[Employee ID]), 'DiversityDataset'[DiversityStatus] = "Diverse")`
- `Included Employees = CALCULATE(COUNTA('DiversityDataset'[Employee ID]), 'DiversityDataset'[InclusionStatus] = "Included")`
- `Diversity Percentage = DIVIDE([Diverse Employees], [Total Employees])`
- `Employee Satisfaction Avg = AVERAGE(DiversityDataset[EmployeeSatisfaction])`
- `Retention Rate = DIVIDE(CALCULATE(COUNT('DiversityDataset'[Employee ID]), 'DiversityDataset'[Retention] = "Yes"), [Total Employees])`

---

## Data Visualization
The following dashboards were created:

### Diversity Overview
This visualization shows the diversity statistics across various demographic categories, including gender, ethnicity, and job titles.

### Employee Satisfaction
This dashboard displays average employee satisfaction scores segmented by gender and ethnicity.

### Retention Analysis
Churn rates were visualized based on inclusion metrics and retention rates across different demographic groups.

---

## Insights:
From the analysis, we observed the following:

1. Employees in diverse groups report higher satisfaction scores compared to non-diverse groups.
2. The overall retention rate is 82%, with a notable difference between diverse and non-diverse groups.
3. Certain job titles have significantly lower diversity representation, indicating areas for improvement.
4. Employee satisfaction is positively correlated with inclusion initiatives.

---

## Recommendations:
1. **Enhance Recruitment Practices:** Implement strategies to attract a more diverse applicant pool for underrepresented job titles.
2. **Support Inclusion Programs:** Develop programs that foster inclusion and support for diverse groups within the organization.
3. **Monitor Employee Feedback:** Regularly survey employees to gather feedback on D&I initiatives and satisfaction levels.
4. **Set Diversity Goals:** Establish measurable diversity goals and track progress toward achieving them.

---

## What I Learned
1. **Creating Hierarchies:** I learned how to create hierarchies in Power BI to better organize and analyze data.
2. **Using Filters and Slicers:** I implemented filters and slicers to enhance interactivity within the dashboard.
3. **Understanding DAX Functions:** Improved my understanding of various DAX functions and their application in data analysis.

---

## Additional DAX Formulas:

1. **Diversity Rate**  
   `Diversity Rate = DIVIDE([Diverse Employees], [Total Employees])`

2. **Retention Rate Calculation**  
   `Retention Rate = CALCULATE(COUNTROWS('DiversityDataset'), FILTER('DiversityDataset','DiversityDataset'[Retention]= "Yes"))`

3. **Diverse Female Employees**  
   `Diverse Females = CALCULATE(COUNTROWS('DiversityDataset'), FILTER('DiversityDataset','DiversityDataset'[DiversityStatus]= "Diverse"), FILTER('DiversityDataset','DiversityDataset'[Gender] = "Female"))`

4. **Diverse Male Employees**  
   `Diverse Males = CALCULATE(COUNTROWS('DiversityDataset'), FILTER('DiversityDataset','DiversityDataset'[DiversityStatus]= "Diverse"), FILTER('DiversityDataset','DiversityDataset'[Gender] = "Male"))`

5. **Average Satisfaction by Gender**  
   `Avg Satisfaction Female = AVERAGEIF('DiversityDataset','DiversityDataset'[Gender]= "Female",'DiversityDataset'[EmployeeSatisfaction])`

6. **Average Satisfaction by Ethnicity**  
   `Avg Satisfaction Latinx = AVERAGEIF('DiversityDataset','DiversityDataset'[Ethnicity]= "Latinx",'DiversityDataset'[EmployeeSatisfaction])`

7. **Count of Diverse Employees**  
   `Count of Diverse Employees = CALCULATE(COUNTROWS('DiversityDataset'), FILTER('DiversityDataset','DiversityDataset'[DiversityStatus]= "Diverse"))`

8. **Count of Non-Diverse Employees**  
   `Count of Non-Diverse Employees = CALCULATE(COUNTROWS('DiversityDataset'), FILTER('DiversityDataset','DiversityDataset'[DiversityStatus]= "Non-Diverse"))`

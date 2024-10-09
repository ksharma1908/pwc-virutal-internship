# Customer Churn Analysis Dashboard

## Demo
1. [Power BI File](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task2_Customer_Churn_Retention/Task2_Customer_Churn_Retentions.pbix)
2. [Screenshots](https://github.com/ksharma1908/pwc-virutal-internship/tree/main/Task2_Customer_Churn_Retention/Screenshots) | [Screenshot 1](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task2_Customer_Churn_Retention/Screenshots/Screenshot_1.JPG) | [Screenshot 2](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task2_Customer_Churn_Retention/Screenshots/Screenshot_2.JPG) | [Screenshot 3](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task2_Customer_Churn_Retention/Screenshots/Screenshot_3.JPG) | [Screenshot 4](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task2_Customer_Churn_Retention/Screenshots/Screenshot_4.JPG) | [Screenshot 5](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task2_Customer_Churn_Retention/Screenshots/Screenshot_5.JPG)
3. [Data File](https://github.com/ksharma1908/pwc-virutal-internship/blob/main/Task2_Customer_Churn_Retention/02_Churn_Dataset.xlsx)

## Table of Contents
1. [What is Customer Churn?](#what-is-Customer-Churn)
2. [Data Source](#data-source)
3. [Skills Demonstrated](#skills-demonstrated)
4. [Data Modeling](#data-modeling)
5. [Data Visualization](#data-visualization)
6. [Insights](#insights)
7. [Recommendations](#recommendations)
8. [What I Learned](#what-i-learned)

## What is Customer Churn?
Customer churn occurs when customers stop purchasing from or subscribing to a service due to dissatisfaction, competitive offerings, or changing preferences. Minimizing churn is crucial for business success.

---

## Data Source
The dataset used in this project consists of 7,043 rows and 23 columns, providing customer demographics, account information, and service subscription details. It was sourced from Forage.

---

## Skills Demonstrated
- **Data Cleaning**
- **Data Inspection**
- **Data Transformation**
- **Data Standardization**
- **Data Visualization**

### Data Cleaning Process:
The following transformations were performed using Power Query:

1. Changed data types for `customerID`, `gender`, and `SeniorCitizen` columns.
   - Example: `Table.TransformColumnTypes(#"Promoted Headers",{{"customerID", type text}, {"gender", type text}, {"SeniorCitizen", Int64.Type}})`
2. Replaced values for payment methods:
   - `Mailed check` → `Mailed Check`
   - `Electronic check` → `Electronic Check`
   - `Bank transfer (automatic)` → `Bank Transfer`
   - `Credit card (automatic)` → `Credit Card`
3. Renamed columns:
   - `customerID` → `CustomerID`
   - `gender` → `Gender`
   - `tenure` → `Tenure`

### Conditional Columns Added:
1. **CitizenshipStatus:** `= IF('ChurnDataset'[SeniorCitizen] = 0, "Young Citizen", "Senior Citizen")`
2. **ChurnStatus:** `= IF('ChurnDataset'[Churn] = "Yes", "Churned", "Retained")`

---

## Data Modeling
Once the data was cleaned, the dataset was modeled in Power BI Desktop.

### Measures (DAX):
The following DAX measures were created for visualization:

- `Total Customers = COUNT(ChurnDataset[CustomerID])`
- `Churned Customers = CALCULATE(COUNTA('ChurnDataset'[CustomerID]), 'ChurnDataset'[Churn] IN { "Yes" })`
- `Retained Customers = CALCULATE(COUNTA('ChurnDataset'[CustomerID]), 'ChurnDataset'[Churn] IN { "No" })`
- `Percent of Churned Customers = (ChurnDataset[Churned Customers] / [Total Customers])`
- `Churn Rate % = ChurnDataset[Churned Customers] / COUNT(ChurnDataset[CustomerID])`
- `Monthly Revenue Loss = CALCULATE(SUM(ChurnDataset[MonthlyCharges]), ChurnDataset[Churn] = "Yes")`
- `CitizenshipStatus = IF('ChurnDataset'[SeniorCitizen] = 0, "Young Citizen", "Senior Citizen")`
- `PaymentMode = IF(OR('ChurnDataset'[PaymentMethod] = "Electronic Check", 'ChurnDataset'[PaymentMethod] = "Mailed Check"), "Manual", "Automatic")`

---

## Data Visualization
The following dashboards were created:

### Customer Demographics
This visualization shows churn rates based on customer demographics, including gender, age, partners, and dependents.

### Account Details
Churn rates were visualized based on account details such as tenure, contract type, payment method, paperless billing, monthly charges, and number of tickets.

### Customer Subscriptions
This visualization presented churn rates based on the services each customer had subscribed to, including phone, multiple lines, internet, online security, tech support, and more.

---

## Insights:
From the analysis, we observed the following:

1. Customers on a two-year contract are more likely to stay, while those on month-to-month contracts are at a higher risk of churn.
2. The churn rate is 27%, with yearly charges of $16.06M and monthly charges of $456.12K.
3. A significant number of churned customers did not sign up for online security and tech support services.
4. 42% of the churned customers were using Fiber Optic as their internet service.

---

## Recommendations:
1. **Increase Long-Term Contracts:** Encourage customers to subscribe to one-year and two-year contracts to reduce churn.
2. **Incentivize Retention:** Offer discounts to customers on month-to-month contracts.
3. **Service Education:** Educate customers on the benefits of signing up for Online Security and Tech Support services.
4. **Boost Automatic Payments:** Increase sales of automatic payments and contracts by 5% annually.

---

## What I Learned
1. **Making Bookmarks:** I learned how to create bookmarks to manage and navigate between visuals efficiently.
2. **Using Toggle for Visualizations:** I implemented toggles with bookmarks to show and hide data dynamically based on user selection.
3. **Using Page Navigator:** Set up a page navigator that enables users to switch between different report pages with a single click.

---

## Additional DAX Formulas:

1. **Churn Rate**  
   `churn rate = DIVIDE('ChurnDataset'[churned], [Number of customers])`

2. **Churned Customers**  
   `churned = CALCULATE(COUNTROWS('ChurnDataset'), FILTER('ChurnDataset','ChurnDataset'[Churn]= "Yes"))`

3. **Churned Females**  
   `churned_females = CALCULATE(COUNTROWS('ChurnDataset'), FILTER('ChurnDataset','ChurnDataset'[Churn]= "Yes"), FILTER('ChurnDataset','ChurnDataset'[gender] = "Female"))`

4. **Churned Males**  
   `churned_Males = CALCULATE(COUNTROWS('ChurnDataset'), FILTER('ChurnDataset','ChurnDataset'[Churn]= "Yes"), FILTER('ChurnDataset','ChurnDataset'[gender] = "Male"))`

5. **Count of Female**  
   `Count of Female = CALCULATE(COUNTROWS('ChurnDataset'), FILTER('ChurnDataset','ChurnDataset'[gender]= "Female"))`

6. **Count of Male**  
   `Count of Male = CALCULATE(COUNTROWS('ChurnDataset'), FILTER('ChurnDataset','ChurnDataset'[gender]= "Male"))`

7. **Device Protection**  
   `Device_Protection = DIVIDE(CALCULATE(COUNT('ChurnDataset'[DeviceProtection]),'ChurnDataset'[DeviceProtection] = "Yes"),COUNT('ChurnDataset'[DeviceProtection]))`

8. **DSL Service**  
   `dsl service = CALCULATE(COUNTROWS('ChurnDataset'),'ChurnDataset'[InternetService] = "DSL")`

9. **Fiber Service**  
   `Fiber service = CALCULATE(COUNTROWS('ChurnDataset'),'ChurnDataset'[InternetService] = "Fiber optic")`

10. **Multiple Lines**  
    `Multiple_lines = DIVIDE(CALCULATE(COUNT('ChurnDataset'[MultipleLines]),'ChurnDataset'[MultipleLines] = "Yes"),COUNT('ChurnDataset'[MultipleLines]))`

11. **No Service**  
    `NO service = CALCULATE(COUNTROWS('ChurnDataset'),'ChurnDataset'[InternetService] = "No")`
# Customer Segmentation and Retention Analysis for Subscription Services
---
### Project Outline
---
[Project Overview](#project-overview)

[Project Workflow](#project-workflow)

[Data Source](#data-source)

[Datasets and column definitions](datasets-and-column-definitions)

[Key Insights from the Data](#key-insights-from-the-data)

[Tools Used](#tools-used)

[Data Cleaning and Preparation (Excel)](#data-cleaning-and-preparation)

[Key steps](#key-steps)

[Formula Used](#formula-used)

[Exploratory Data Analysis](#exploratory-data-analysis)

[Data Analysis (SQL)](#data-analysis-(sql))

[Data Visualization (Power BI)](#data-visualization-(power-bi))

[Key Findings](#key-findings)

[Pictorial Visuals of Analysis](#pictorial-visuals-of-analysis)

### Project Overview
---
This project aims to analyzes customer data in identifying key segments and behavioral trends within a subscription service. The objective is to explore customer behavior patterns, track different subscription types, and detect critical trends in cancellations and renewals. The deliverable is a Power BI dashboard that visualizes these insights, providing a comprehensive view of customer retention and segment-based performance.

### Project Workflow 
---
The project was completed in three phases: data cleaning and exploration in Excel, query-based analysis using SQL, and final visualization in Power BI. 

### Data Source 
---

The primary source of data used here was Customer Data.xlsx 

### Datasets and column definitions 
---

The Customer data used in this project consists of multiple columns that capture key information about sales transactions. Below is an explanation of each column in the dataset: 

• **CustomerId**: A unique identifier assigned to each customer in the dataset, such as 201, 202 etc.

• **Customer Name**: The full name of the customer associated with the subscription, such as John, Jane, Alex etc.

• **Region**: The geographical location or area where the customer resides or where the subscription is active, such as North, South, East and West.

• **Subscription Type**: The category or level of subscription chosen by the customer (e.g., Basic, Premium and Standard). 

• **Subscription Start**: The date when the customer's subscription began. 

• **Subscription End**: The date when the customer's subscription is set to end or renew.

• **Canceled**: Indicates whether the subscription was canceled, typically as a "Yes" or "No" value.

• **Revenue**: The total revenue generated from the customer’s subscription.

### Key Insights from the Data 

---
Here are some of the key insights derived from the customer subscription data:

1. **Top-Performing Regions**: Identify which regions generate the highest revenue and have the most active subscriptions, helping target marketing and retention efforts more effectively.

2. **Popular Subscription Types**: Analyze the distribution of subscription types (e.g., Basic, Premium) to understand customer preferences and identify high-value segments.

3.**Revenue Trends**: Track monthly revenue trends, highlighting periods with increased revenue or higher cancellations for possible seasonal patterns.

4. **Subscription Lifecycle Analysis**: Determine the average subscription duration across types, offering insight into how long customers typically remain subscribed before canceling or renewing.

5. **Behavioral Patterns in Cancellations**: Investigate patterns in cancellations, such as whether they occur more often with specific subscription types, in certain regions, or after a certain duration.

6. **Revenue per Customer Segment**: Segment customers by subscription type or region to determine which segments are the most profitable, guiding targeted strategies to increase revenue from high-value customers.


### Tools Used 
---
1.  **Microsoft Excel** [Download Here](https://www.microsoft.com/en-us/microsoft-365/excel)

• For initial data cleaning, 

• For analysis, 

• For exploration and 

• For Data visualization. 

2. **Microsoft SQL Server** [Download Here](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
   
   - Other SQL database you can use include MySQL: [Download MySQL](https://dev.mysql.com/downloads/),
   - PostgreSQL: [Download PostgreSQL](https://www.postgresql.org/download/)

• For data extraction 

• For advanced querying from the sales database. 

3.  **Power BI** [Downloaad Here](https://powerbi.microsoft.com/en-us/downloads/)

• For data visualization 

• For dashboard creation. 

4  **Github**  [Download Here](https://github.com/)
- for portfolio Building
  
- From this page, you can sign up, create repositories, and explore open-source projects.


### 1. Data Cleaning and Preparation (Excel) 
---

The sales data was first explored and cleaned in Excel. The following actions were done: 

• Data loading and Inspection. 

• Handling missing variables, removing duplicates and formatting columns. 

• Data validation to ensure consistency  

• Basic exploratory analysis, such as Subscription Duration, Most popular subscription type, total revenue etc using pivot tables. 

**Key Steps**: 

• Filtered sales data for the analysis period. 

• Created summary/pivot tables for subscription type categories, regions, and sales channels. 

• Calculated key metrics such as average subscription duration and total revenue by subscription type. 


### Formula Used 
---

• **Subscription Duration** 
```Excel
=DATEDIF([Subscription Start], [Subscription End], "M")  // for months
```
or 
```Excel
==F2 - E2
```
F2 - Subscription End, E2 - Subscription Start


### Exploratory Data Analysis 
---
The structured approach to perform Exploratory Data Analysis (EDA) on the customer subscription data in Excel include 
1. **Descriptive Statistics** -Revenue Totals and Averages, Count and Frequency etc
2. **Trend Analysis** - Revenue Over Time
3.**Segmentation Analysis** -Use Pivot Tables to group by Subscription Type and calculate metrics like total revenue, average revenue per type. This helps understand which subscription types are most valuable.

EDA was used to explore and to answer some questions about the Data such as; 

• what is the total and average revenue per customer and per subscription type? 

• which subscription types are most popular? 

• which subscription types generate the most revenue?


### 2. Data Analysis (SQL) 
---

After the initial data preparation, SQL was used to run more advanced queries on the dataset , allowing deeper insights. 

**_Key SQL Queries**_: 

• **To find the top 3 regions by subscription cancellations**
```SQL
SELECT  Top (3) Region, COUNT(CustomerID) AS Cancellations
FROM [dbo].[Customer Data]  WHERE Canceled = 'TRUE'
GROUP BY Region
ORDER BY Cancellations DESC;
```

• **To calculate total revenue by subscription type**
```SQL
SELECT [SubscriptionType], SUM(CAST(REPLACE(LTRIM(RTRIM([Revenue])), ',', '') AS DECIMAL(10, 2))) AS TotalRevenue
FROM [dbo].[Customer Data]
GROUP BY [SubscriptionType]
ORDER BY TotalRevenue DESC
``` 

• **To retrieve the total number of customers from each region**
```SQL
SELECT [Region], COUNT([CustomerID]) AS TotalCustomers
FROM [dbo].[Customer Data]
GROUP BY [Region];
```

• **To find the most popular subscription type by the number of customers**
```SQL
SELECT [SubscriptionType], COUNT([CustomerID]) AS MostPopularSubscriptionType
FROM [dbo].[Customer Data]
GROUP BY [SubscriptionType]
ORDER BY MostPopularSubscriptionType DESC
```

• **To calculate the average subscription duration for all customers**
```SQL
SELECT AVG(DATEDIFF(day, [SubscriptionStart], [SubscriptionEnd])) 
AS AverageSubscriptionDurationDays
FROM [dbo].[Customer Data];
```

### 3. Data Visualization (Power BI) 
---

DAX Measures for key insights were created: 

• **Total Subscriptions**:
```DAX
TotalSubscriptions = COUNTROWS('SubscriptionTable')
```

• **Canceled Subscriptions**:
```DAX
CanceledSubscriptions = CALCULATE(COUNTROWS('SubscriptionTable'), 'SubscriptionTable'[Status] = "Canceled")
```

• **Active Subscriptions**:
```DAX
ActiveSubscriptions = CALCULATE(COUNTROWS('SubscriptionTable'), 'SubscriptionTable'[Status] = "FALSE")
```
• Average Subscription Duration:
```DAX
AvgSubscriptionDuration = AVERAGE('SubscriptionTable'[SubscriptionDurationInMonths])
```
---
The final stage was to visualize the insights using Power BI. The interactive dashboard includes: 

• **Subscription Trends**: Use a Line Chart to show trends over time:
X-axis: Time (e.g., months, quarters, years).
Y-axis: Total Subscriptions, New Subscriptions, Cancellations, or Total Revenue.

• **Revenue Breakdown**: Use a Stacked Column Chart to display total revenue by Subscription Type or Region.

• Cancellation Analysis: Use a Stacked Bar Chart or Clustered Bar Chart to display:
a. Cancellations by Subscription Type.
b. Cancellations by Region or Customer name


### Key Findings 
---
1. **Most Popular Subscription Type**
   
- _Finding_:The Basic subscription is the most popular, with a total value of ₦37,500, while Premium and Standard subscriptions are equally popular, each generating ₦18,750.
- _Inference_: The higher adoption rate of the Basic subscription suggests that customers may prefer lower-cost options, possibly due to budget constraints or a perception that Basic provides sufficient value. This insight might indicate an opportunity to create upsell strategies for Basic subscribers who may be interested in additional features of higher-tier plans.
 
2. **Revenue Distribution by Subscription Type**

- _Finding_: Basic subscriptions contribute the most to overall revenue, while Premium and Standard subscriptions contribute less, despite offering more features.
- _Inference_: The revenue contribution from Basic subscriptions could mean a high volume of customers at this level, but it may also imply that Premium and Standard are not as attractive or that pricing does not justify their perceived value. Reviewing Premium and Standard subscription features or pricing could improve uptake and increase total revenue.

3. **Regional Performance and Customer Distribution**

- _Finding_: Certain regions have a higher concentration of customers, while others show fewer subscribers or higher cancellation rates. from our data the region with the highest concentration of customer was the South followed by West then East and North.
- _Inference_: Regions with high customer concentrations are potential areas for targeted marketing and customer engagement. In regions with high cancellation rates, exploring reasons behind cancellations could uncover service gaps, pricing concerns, or competition, helping shape strategies to improve customer experience and retention.

4. **Seasonal Trends in Subscriptions**

- _Finding_: The highest sales occurred in June, with a steady increase observed in the first quarter of the year.
- _Inference_: Seasonal trends in new subscriptions suggest that marketing efforts may be especially effective during certain times of the year. 

5. **Customer Retention by Subscription type**

- _Finding_: Retention rates are highest among Basic subscription users, with Premium and Standard subscriptions showing comparatively lower retention.
- _Inference_: Basic subscribers may feel that they receive good value for the cost, leading to higher satisfaction and loyalty. In contrast, the lower retention rates in Premium and Standard subscriptions might indicate that customers in these tiers do not see enough added value to justify the higher cost. This suggests a potential need to reassess the benefits or pricing of the Premium and Standard plans to increase their attractiveness and retain customers longer.
  
### Pictorial Visuals of Analysis
---
- **EXCEL**
---
- **MOST POPULAR SUBSCRIPTION TYPE**
![MostPopularSubscriptionType](https://github.com/user-attachments/assets/ae9683c9-3a10-4693-990a-381179a7c746)

- **CUSTOMER RETENTION RATE**
![CustomerRetentionRate](https://github.com/user-attachments/assets/b356bbe0-79bb-4b14-b9d8-f83c483a6c8c)

-**SUBSCRIPTION TYPE BY REGION**
![SubscriptionTypebyRegion](https://github.com/user-attachments/assets/49e7475e-ce86-45d2-9cf7-e26305d98096)

- **TOP REVENUE BY SUBSCRIPTION**
![TopRevenuebySubscription](https://github.com/user-attachments/assets/e6a1732d-b85d-4175-a9fe-033648aa7c54)

- **REVENUE TRENDS OVER TIME**
![RevenueTrendsovertime](https://github.com/user-attachments/assets/72bb2e95-8425-45ab-af35-08d3cb9a809f)

Inference
---
1. **Monthly Revenue Performance**:
June, February, and April recorded the highest revenue, each exceeding 15 million, indicating peak months with potentially increased customer engagement or higher sales.
October, September, and December showed the lowest revenue, all below 7.5 million, suggesting these months had reduced activity or sales volume.
2. **Revenue Distribution**:
Revenue is unevenly distributed throughout the year, with high peaks and low troughs. The substantial difference between peak and low months might indicate a seasonal trend or fluctuations in customer demand.
Months like June and February contribute significantly to the annual total, showing an upward trend in revenue during these periods.
3. **Strategic Implications**:
The business could focus on analyzing the factors contributing to high revenue in June, February, and April to replicate these successes in other months. Promotional events, marketing campaigns, or product launches during these periods could be reinforcing customer activity.
For the lower-revenue months, especially October, September, and December, it may be beneficial to introduce special offers, holiday discounts, or targeted campaigns to boost revenue and reduce seasonal variability.
Additionally, understanding customer behaviors and preferences during high-performing months could provide insights for strategic planning in less profitable months.
4. ** Conclusion**:
The company should capitalize on peak revenue months with enhanced sales and marketing strategies while devising interventions for low-revenue months to improve consistency. This approach would allow for better revenue stability and maximize yearly performance.

- **AVERAGE REVENUE BY CUSTOMER BY REGION**
![AvgRevenuebyCustomerbyRegion](https://github.com/user-attachments/assets/362356aa-4182-4aef-be72-f48b0ffda03a)

Inference 
---
1. **Regional Performance**:
South Region shows the highest average revenue per customer at 2,004, indicating that customers here may be purchasing higher-value subscriptions or spending more on services compared to other regions.
East and North Regions have the lowest average revenue per customer (1,994 and 1,993, respectively), suggesting a lower engagement or preference for basic services.
2. **Revenue Distribution**:
Revenue is unevenly distributed across regions, with the South contributing the most on a per-customer basis, while East and North regions are relatively lower.
The West Region has a moderate performance with an average revenue per customer of 1,999, slightly below the South but above the East and North.
3. **Strategic Implications**:
The South Region could be a focus area for premium services or up-selling opportunities due to higher spending by its customers.
The East and North Regions may require targeted marketing efforts or promotional strategies to increase customer engagement and revenue. Introducing offers, discounts, or incentives in these regions could potentially drive up average revenue per customer.
For the West Region, maintaining existing customer satisfaction while exploring cross-selling opportunities could help sustain or slightly increase revenue.
4. **Conclusion**:
The data suggests prioritizing the South Region for high-revenue growth strategies and considering specific customer acquisition or engagement strategies in the East and North. Focusing on these tailored approaches could help the company enhance regional revenue distribution and overall performance.

- **CUSTOMER DATA DASHBOARD**
![CUSTOMER DATA DASHBOARD](https://github.com/user-attachments/assets/b5dee6d6-f6cb-445a-beac-26fe46d7e723)

- **SQL**
---
- **TOTAL REVENUE BY SUBSCRIPTION TYPE**
![TotalRevenuebySubscriptionType](https://github.com/user-attachments/assets/8e75634d-2a48-4a17-9fef-7ae4e17dcb7b)

Inference
---
1. **Revenue Distribution by Subscription Type**:
The Basic subscription generates the highest revenue at $74,756,784.00, which aligns with its popularity among customers.
The Premium subscription generates $37,580,782.00, contributing about half of the revenue from Basic but still significant.
The Standard subscription generates $37,482,120.00, almost identical to Premium in terms of revenue. This shows that Premium and Standard are similarly valuable in revenue terms, despite possible differences in customer count or price points.
2. **Implications for Regional Performance**:
Although this result doesn’t directly show regional performance, the next steps could involve analyzing how each region contributes to these subscription types. Understanding where Basic, Premium, and Standard subscriptions are most popular across regions would offer actionable insights.
Regions with higher cancellations (referenced in the query but not shown in the results) could indicate areas where retention efforts are needed, especially for lower-revenue subscriptions.
3. **Strategic Implications**:
Focus on Upselling: Since Basic has the highest revenue but might be the lowest-priced option, there’s potential for upselling Basic subscribers to Premium or Standard to maximize revenue per user.
Retention Programs: High revenue from Basic subscriptions suggests a large customer base, which may have higher churn. Strategies aimed at retaining Basic subscribers could stabilize and possibly grow this revenue stream.
Product Enhancement for Premium and Standard: Given that Premium and Standard generate similar revenue, understanding the unique benefits each tier offers could allow the company to refine these tiers to increase their attractiveness and distinctiveness.
4. **Conclusion**:
The data highlights the importance of the Basic subscription as a core revenue driver. While Premium and Standard contribute similar revenue amounts, additional segmentation or feature enhancement might create opportunities for growth.
Overall, optimizing the Basic tier to reduce churn while making Premium and Standard tiers more appealing through added benefits or targeted marketing could provide balanced growth across all subscription types.


- **TOP 3 REGION BY SUBSCRIPTION CANCELLATION**
![Top3RegionbySubscriptioncancellation](https://github.com/user-attachments/assets/9c04354e-84c9-4a49-b748-41d5a31def93)

- **TOTAL REVENUE BY SUBSCRIPTION TYPE**
![TotalRevenuebySubscriptionType](https://github.com/user-attachments/assets/5e1e7fd0-ca7b-4888-9301-2c68a1ba8557)

- **AVERAGE SUBSCRIPTION FOR ALL CUSTOMERS**
![AverageSubscriptionforAll](https://github.com/user-attachments/assets/c332b7b2-8656-47a7-988c-a3049cec4066)

- **MOST POPULAR SUBSCRIPTION TYPE**
![MostPopularSuscriptionType](https://github.com/user-attachments/assets/9392739b-5946-449e-9277-d8acf2037869)

Inference
---
1. **Subscription Popularity**:
The Basic subscription is the most popular, with 37,500 customers, significantly higher than the other types.
Both the Premium and Standard subscriptions have an equal number of customers, 18,750 each, indicating a balanced interest between these two tiers but less than half the customer base of the Basic subscription.
2. **Revenue Implications**:
Since the Basic subscription has the highest number of customers, it is likely a major contributor to the total revenue. However, if Basic is a lower-priced option, the overall revenue per customer may be lower compared to Premium or Standard tiers.
Premium and Standard subscriptions, while less popular, might contribute higher per-customer revenue. Therefore, encouraging upgrades from Basic to these tiers could increase total revenue without requiring as many new customers.
3. **Strategic Implications**:
Retention and Upselling: The organization could explore targeted marketing strategies to encourage Basic customers to upgrade to Premium or Standard, possibly through value-added features or promotional discounts.
Customer Insights: Understanding why customers prefer the Basic subscription could reveal insights into customer needs and preferences. This data could be used to enhance features in higher-tier subscriptions to make them more appealing.
Customer Segmentation: Since Basic has such a high customer count, segmenting this group further could allow for customized campaigns aimed at increasing loyalty and reducing churn, especially if the Basic tier experiences higher turnover.
4. **Conclusion**:
The Basic subscription’s popularity indicates it appeals to a broad customer base, possibly due to affordability or basic service needs. However, to drive revenue growth, the organization should consider strategies to enhance the appeal of Premium and Standard options. By promoting upgrades and focusing on customer retention within the Basic tier, the company can achieve a more balanced revenue distribution and improve long-term profitability.

- **POWER BI**
---
KEY METRICS DISPLAY
---
![KEY PERFORMANCE INDICATORS](https://github.com/user-attachments/assets/0e28318a-56f7-4207-9ea7-bc9542d8eaee)
SHOWING THE FOLLOWING INDICATORS
- **ACTIVE SUBSCRIPTION**
- **CANCELED SUBSCRIPTION**
- **TOTAL SUBSCRIPTION**
- **AVERAGE SUBSCRIPTION DURATION (DAYS)**
- **TOTAL REVENUE**
- **CANCELLATION RATE**

SUBSCRIPTION TRENDS
---
**ACTIVE SUBSCRIPTION BY REGION (RIGHT)**     AND      **CANCELED SUBSCRIPTION BY SUBSCRIPTION TYPE (LEFT)**
![ACTIVE SUBSCRIPTION BY REGION ](https://github.com/user-attachments/assets/1e20ff78-bb1c-4b73-bb5a-70df495e0722)

**ACTIVE SUBSCRIPTION BY SUBSCRIPTION TYPE (LEFT)**     AND **CANCELED SUBSCRIPTION BY REGION  (RIGHT)**
![ACTIVE SUBSCIPTION BY SUBSCRIPTION TYPE](https://github.com/user-attachments/assets/58d71c08-9661-46fa-8ced-80286d666567)

**COUNT OF SUBSCRIPTION BY REGION**
![COUNT OF SUBSCRIPTION BY REGION](https://github.com/user-attachments/assets/a29bafa3-70e4-4ffa-abcb-19e4aaa4c20a)

REVENUE BREAKDOWN ANALYSIS
---
**TOTAL REVENUE BY SUBSCRIPTION TYPE**    AND   **TOTAL REVENUE BY REGION**
![TOTAL REVENUE BY REGION](https://github.com/user-attachments/assets/cb1fc540-c69d-4ef5-91a2-f79915df2ad5)

**CUSTOMER DATA DASHBOARD WITH INTERACTIVE SLICER (REGION)**
![CUSTOMER DATA DASHBOARD POWERBI](https://github.com/user-attachments/assets/c464c2cd-8d4a-4d2d-8bcf-6c4f57fa2c0e)


### **RECOMMENDATION**

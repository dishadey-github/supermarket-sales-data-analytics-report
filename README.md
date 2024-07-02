# Supermarket Sales Data Data Analytics Report

## Supermarket Sales Report Review
![Supermarket Sales Data Analytics Dashboard](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/e9d3a7f9-c2e0-4224-a0f2-76ad3e2a5153)


#### Overview
This repository contains the Supermarket Sales Data Analytics Dashboard, which provides an insightful visualization of supermarket sales data. The dashboard is designed to offer a comprehensive view of sales, profit, and returned orders, with comparisons to the previous year. It enables users to filter data by customer name, country/region, segment, and date range.

#### Data Source
Sample-Superstore.xlsx: Contains the raw data used to generate the dashboard. 
This Excel file contains Orders table and Returns table. This includes details on sales, profit, returned orders, and additional metrics.

#### Date Table:
Contains date-related information to support time-based filtering and calculations. (Date, Start of Month)

#### Key Measure Table:
It contains various calculated measures used in the dashboard. The key measure table has been created to fulfill the KPIs.
Key Measure table consists of the following -
##### 1. Main Metrics
   - Sales (Contains sales data for each transaction)
   - Profit (Contains profit data for each transaction)
   - % Returned Orders (Contains data on the percentage of returned orders)
##### 2. Previous Year (PY) - Comparative Metrics
   - Sales PY (Contains sales data from the previous year)
   - Profit PY (Contains profit data from the previous year)
   - % Returned Orders PY (Contains data on the percentage of returned orders from the previous year)
##### 3. % Change Metrics (vs PY)
   - vs PY - Sales (% of change of sales in the current year with respect to the previous year)
   - vs PY - Profit (% of change of profit in the current year with respect to the previous year)
   - vs PY - % Returned Orders (% of change of returned orders in the current year with respect to the previous year)

##### Activities to perform in the Power Query
1. Open Power Query Editor:
Click on Transform Data to open the Power Query Editor. In view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.

2. Inspect and Clean Data:
Verify that both datasets (Orders and Returns) are loaded correctly.
Check for any inconsistencies or missing values and handle them accordingly (e.g., removing null values, correcting data types).

##### Activities to perform in the Table View
##### 1. Create the Date Table
```
Date Table = 
ADDCOLUMNS(
    CALENDAR(MIN(Orders[Order Date]), MAX(Orders[Order Date])),
    "Start of month", EOMONTH([Date], -1) + 1
)
```
##### 2. Create Measure Table
##### Main Metrics
Sales
```
Sales = SUM(Orders[Sales])
```
Profit
```
Profit = SUM(Orders[Profit])
```
% Returned Orders
```
% Returned Orders = 
VAR total_orders = DISTINCTCOUNT(Orders[Order ID])
VAR returned_orders = DISTINCTCOUNT(Returns[Order ID])
VAR percentage = 
DIVIDE(
    returned_orders,
    total_orders
)
RETURN
percentage
```
##### Previous Year (PY) - Comparative Metrics
Sales PY
```
Sales PY = 
CALCULATE(
    [Sales],
    SAMEPERIODLASTYEAR('Date Table'[Date])
)
```
Profit PY
```
Profit PY = 
CALCULATE(
    [Profit],
    SAMEPERIODLASTYEAR('Date Table'[Date])
)
```
% Returned Orders PY
```
% returned orders PY = 
CALCULATE(
    [% returned orders],
    SAMEPERIODLASTYEAR('Date Table'[Date])
)
```
##### % Change Metrics (vs PY)
vs PY - Sales
```
vs PY - Sales = 
DIVIDE(
    [Sales] - [Sales PY],
    [Sales PY]
)
```
vs PY - Profit
```
vs PY - Profit = 
DIVIDE(
    [Profit] - [Profit PY],
    [Profit PY]
)
```
vs PY - % Returned Orders
```
vs PY - % returned orders = 
[% returned orders] - [% returned orders PY]
```

#### Numerical values :
##### Main Metrics
##### Sales: Total sales revenue.
Current Year (CY): $2.33M\
Previous Year (PY): $1.58M\
Change vs PY: 47.16% increase
##### Profit: Total profit earned.
CY: $292.30K\
PY: $196.37K\
Change vs PY: 48.85% increase
##### % Returned Orders: Percentage of orders that were returned.
CY: 5.79%\
PY: 8.74%\
Change vs PY: 2.95% decrease

##### Comparative Metrics
Sales vs PY (% change): Change in sales compared to the previous year.
47.16% increase\
Profit vs PY (% change): Change in profit compared to the previous year.
48.85% increase\
% Returned Orders vs PY (% change): Change in the percentage of returned orders compared to the previous year.
2.95% decrease


##### Dashboard Sections
##### Profit by Product
This section displays the profit earned from different product categories, including Furniture, Office Supplies, and Technology. It provides a breakdown of profit by specific products within these categories.

![image](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/622ce451-2aea-44f7-b82b-fdf9f9762a8c)

1. Furniture
Bookcases: ~$20K\
Chairs: ~$25K\
Furnishings: ~$15K\
Tables: -$17.75K (loss)\
Office Supplies\
Binders: ~$30K\
Envelopes: ~$5K\
Fasteners: ~$2K\
Labels: ~$3K\
Paper: ~$10K\
Storage: ~$5K\
Supplies: ~$2K
2. Technology
Accessories: ~$19.17K\
Copiers: ~$56.09K\
Machines: ~$25K\
Phones: ~$30K

![image](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/5a35dbe4-71c3-4997-8cdc-e2195ba4ff77)

#### Sales vs Previous Year Sales
This line chart shows the trend of sales over time, with a comparison to the previous year's sales. It helps identify patterns and seasonal trends.

#### Notable Trends:
Significant increase in sales during Q3 of 2023 compared to previous years.
Consistent growth in sales from 2020 to 2023.

![image](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/f281a956-37d0-459d-8bad-02de38e69410)

#### Profit by State
A geographical representation of profit across different states. This map helps visualize regional performance.

#### Top Performing States:
California: Highest profit\
Texas: Second highest profit

![image](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/0e1f7deb-468d-41ac-8b8f-be28c233d866)

#### Sales by Segment
A pie chart that breaks down sales by different market segments, such as Consumer, Corporate, and Home Office.

#### Sales Distribution:
- Consumer: 50.32%
- Corporate: 30.77%
- Home Office: 18.92%
  
Filtering the Dashboard\
The dashboard allows for dynamic filtering based on the following parameters:

Customer Name: Filter data specific to a particular customer\
Country/Region: Filter data for a specific country or region\
Segment: Filter data based on the market segment\
Date Range: Select a specific date range to view the data for that period


### Superstore Sales Report (with filter 1)

![Filter 1](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/727115f4-1dbd-4738-b168-58ea89ab01f0)

![filters](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/b8e54365-cb68-45b3-b765-5d408fb5721e)

This analysis examines the filtered dashboard data for the following
 - Customer Name : Adam Bellavance
 - Country/Regoin : United States
 - Segment : Home Office
 - Date : 09-06-2023 to 30-12-2023

![KPI](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/91979104-557e-4e4c-92fd-8c9e5c72eb7c)

#### KPIs Overview
Sales:
Current Year (CY): $2.86K\
Previous Year (PY): $4.47K\
Change vs PY: -36.05%

Profit:
CY: $449.03\
PY: $1.46K\
Change vs PY: -69.28%

% Returned Orders:
CY: 9,866.67%\
PY: 14800.00%\
Change vs PY: -4933.33%

#### Detailed Analysis
#### Sales
Current Year: Sales for the specified period are $2.86K\
Previous Year: Sales were $4.47K\
Change vs PY: A significant decrease of 36.05% compared to the previous year

#### Business Analytics Perspective:
This notable decline suggests a potential loss of market share or a reduction in customer purchases. It may be essential to investigate the factors contributing to this decrease. Are there specific products underperforming, or have there been changes in customer preferences? This drop might also highlight the need for marketing efforts or sales promotions to boost revenue.

#### Profit
Current Year: The profit recorded is $449.03\
Previous Year: The profit was $1.46K\
Change vs PY: A substantial decrease of 69.28%

#### Business Analytics Perspective:
The dramatic drop in profit raises concerns about cost management and pricing strategies. It may indicate increased operational costs or a shift towards lower-margin products. Understanding the cost structure and identifying areas where expenses can be optimized would be crucial. Additionally, evaluating the pricing strategy might help improve profitability.

#### % Returned Orders
Current Year: The percentage of returned orders is 9,866.67%\
Previous Year: The percentage was 14,800.00%\
Change vs PY: A decrease of 4,933.33%.

#### Business Analytics Perspective:
Despite the large numbers, the decrease in the percentage of returned orders is a positive indicator. It suggests improvements in product quality or customer satisfaction. Continued monitoring is needed to ensure this trend persists, and further analysis could pinpoint which product categories have the highest return rates and why.

![profit by product](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/6167d228-4e78-48c8-86fc-4d7c65a5f921)

#### Profit by Product
Chairs: Loss of $73.05\
Tables: Profit of $366.63\
Paper: Profit of $146.79\
Accessories: Slight profit, no specific value provided

#### Business Analytics Perspective:
Tables and Paper: These categories show a healthy profit and may be strong performers. Increasing focus on these products could drive overall profitability.
Chairs: The loss in this category indicates a problem that needs addressing. It could be due to high return rates, low sales, or high costs.
Accessories: Slight profit indicates potential for growth, suggesting a review of marketing and sales strategies for these products.

![CY Sales vs PY Sales](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/5121adf1-a801-4342-9c23-b627b131e832)

#### Sales vs Previous Year Sales
The line chart shows a rising trend in sales from August to November 2023.

#### Business Analytics Perspective:
This positive trend, despite the overall decrease compared to the previous year, is encouraging. It suggests a recovery phase or a successful recent strategy. Continuously tracking this trend can help in making informed decisions for future strategies.

![profit by state](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/e586524c-4023-4e23-989b-4c04bdfb8f3b)

#### Profit by State
Highlighted States: New York and Ohio show significant profit.

#### Business Analytics Perspective:
Focusing on these states for further market penetration and understanding the factors contributing to high performance can be beneficial. Replicating successful strategies in other regions might improve overall profitability.

![sales by segment](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/2524de77-f4ea-4a69-b4fc-b62030dd9cf6)

#### Sales by Segment
Home Office: 100%

#### Business Analytics Perspective:
The dashboard reflects data exclusively for the Home Office segment. This focused analysis helps understand the specific needs and behavior of home office customers. Tailoring marketing campaigns and product offerings to this segment can improve engagement and sales.

#### Conclusion:
This detailed analysis highlights several key areas for business improvement:
Sales and Profit Decline: Requires investigation into underlying causes, possibly revamping marketing strategies or improving product offerings.
Return Rate Improvement: Indicates progress but needs continuous monitoring and action to maintain this trend.
Product Profitability: Leveraging profitable products while addressing underperformers can enhance overall business performance.
Geographical Insights: Successful strategies in profitable states can be replicated elsewhere to drive growth.
Segment Focus: Tailoring strategies to the Home Office segment can lead to better customer satisfaction and increased sales.
By understanding and acting on these insights, the business can work towards reversing negative trends and capitalizing on positive ones for overall growth and profitability.


#### Filtering Example 2

![Filter 2](https://github.com/dishadey-github/supermarket-sales-data-analytics-report/assets/60807918/49843d27-cbc2-4f6f-bee8-3a82ebcfc42e)

This analysis shows reflecting upon the following filters\
- Customer Name : Aaron Hawkins
- Country/Region : United States
- Segment : Corporate
- Date Range : 14-01-2020 to 13-12-2023
the dashboard updates to reflect data specific to these criteria. This allows for targeted analysis and better decision-making.

#### Example Values:
Sales: $1.73K\
Profit: $362.88\
% Returned Orders: 4,933.33%

#### Profit by Product:
Envelopes: $62.64\
Phones: $121.44\
Chairs: ~$10

#### Sales vs Previous Year Sales:
Sharp increase in sales during mid-2022.

#### Profit by State:
New York: Highest profit for Aaron Hawkins

#### Sales by Segment:
Corporate: 100%

#### Business Analyst Perspective
As a business analyst, this dashboard provides critical insights into various aspects of supermarket performance:

#### Sales Growth
Numerical Insight: A 47.16% increase in sales over the previous year indicates strong growth, possibly due to successful marketing campaigns or increased customer retention.
Action: Investigate the strategies that contributed to this growth to replicate success in other regions or segments.

#### Profit Margins
Numerical Insight: A 48.85% increase in profit demonstrates improved cost management or higher-margin product sales.
Action: Identify the highest profit-generating products and focus on promoting these items. Analyze cost structures to understand where efficiencies have been gained.

#### Return Rates
Numerical Insight: A 2.95% decrease in returned orders percentage suggests improved customer satisfaction or better quality control.
Action: Continue monitoring return rates to maintain or further reduce them. Identify products with the highest return rates and investigate underlying issues.
#### Segment Analysis

Numerical Insight: With 50.32% of sales coming from the Consumer segment, this segment is the most significant contributor to revenue.
Action: Tailor marketing strategies to cater to consumer needs. Explore opportunities to grow the Corporate and Home Office segments.

By using this dashboard, analysts can provide actionable insights to drive business growth, optimize product offerings, and enhance customer satisfaction.

#### Conclusion
The Supermarket Sales Data Analytics Dashboard is a powerful tool for visualizing and analyzing supermarket performance data. By leveraging the provided data files and utilizing the filtering capabilities, users can gain a deeper understanding of their sales, profit, and returned orders, and make data-driven decisions to improve overall business performance.

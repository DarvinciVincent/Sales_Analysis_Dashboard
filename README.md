# Sales Analysis Dashboard

## Table of Contents:

- [Problem Statement](https://github.com/DarvinciVincent/Sales_Analysis_Dashboard/blob/main/README.md#problem-statement-)
- [Datasource](https://github.com/DarvinciVincent/Sales_Analysis_Dashboard/blob/main/README.md#datasource-)
- [Data Analysis (DAX)](https://github.com/DarvinciVincent/Sales_Analysis_Dashboard/blob/main/README.md#data-analysis-dax)
- [Insights & Recommendation](https://github.com/DarvinciVincent/Sales_Analysis_Dashboard/blob/main/README.md#insights)

## Problem Statement:

The main idea of this project is to:<br>
• Explore sales trends over time.<br>
• Identify the best-selling products.<br>
• Calculate revenue metrics such as total sales and profit margins.<br>
• Create visualizations to present findings effectively.

## Datasource:

Dataset used for this task was presented by [MeriSKILL](https://www.meriskill.com/) and Sales dataset:

Dataset: [Sales Dataset](https://github.com/DarvinciVincent/Sales_Analysis_Dashboard/blob/main/Sales%20Data.csv)

## Data Analysis (DAX):

Table and measures used in all visualizations are:

- D_CALENDAR date_table_base = <br>
VAR dates = <br>
CALENDAR (MIN('Sales Data'[Order Date]), max('Sales Data'[Order Date]))<br>
VAR date_table_base =<br>
ADDCOLUMNS (<br>
dates,<br>
"Date_raw", FORMAT( [Date], "YYYYMMDD"),<br>
"Year", YEAR ( [Date] ),<br>
"Half", FORMAT ( [Date], "YYYY") & " " & IF( MONTH( [Date] ) >= 7,"H2","H1"),<br>
"Half year", FORMAT ( [Date], "YYYY") & IF( MONTH( [Date]) >= 7, "H2", "H1"), <br>
"Quarter", FORMAT ( [Date], "YYYY Q" & QUARTER( [Date] )),<br>
"Quarter year", FORMAT ( [Date], "YYYY") & " Q" & QUARTER( [Date] ), <br>
"Year Month", FORMAT ( [Date], "YYYYMM", "en-GB" ),<br>
"Month no", FORMAT ( [Date], "MM" ),<br>
"Month", FORMAT ( [Date], "MMMM", "en-GB" ),<br>
"Month short", FORMAT ( [Date], "MMM", "en-GB" ),<br>
"Month short Year", FORMAT ( [Date], "MMM YYYY", "en-GB" ),<br>
"Month very short Year", FORMAT ( [Date], "MMM YY", "en-GB"), <br>
"Week no", WEEKNUM ([Date],2),<br>
"Start of week", FORMAT(( [Date] +1 ) - WEEKDAY ( [Date], 2), "DD-MMM-YY", "en-GB"),<br>
"Start week #", YEAR(( [Date] +1) - WEEKDAY ( [Date], 2)) & FORMAT (WEEKNUM( ( [Date] +1 ) - WEEKDAY ( [Date], 2)), "00"),<br>
"Year WeekNumber", FORMAT ( [Date], "YYYY" ) & " W "  & WEEKNUM([Date],2),<br>
"Day", FORMAT( [Date], "DD", "en-GB"),<br>
"Weekday short", FORMAT( [Date], "DDD", "en-GB"),<br>
"Weekday", FORMAT( [Date], "DDDD", "en-GB") <br>
)<br>
RETURN<br>
date_table_base'

- SalesPerOrder = 'sum('Sales Data'[Sales]) / COUNT('Sales Data'[Order ID])'

- Total Sales = 'CALCULATE(sum('Sales Data'[Sales]))'

- Time Category = 
'SWITCH(<br>
    TRUE(),<br>
    TIME(5, 0, 0) <= [Time] && [Time] < TIME(12, 0, 0), "Morning",<br>
    TIME(12, 0, 0) <= [Time] && [Time] < TIME(17, 0, 0), "Afternoon",<br>
    TIME(17, 0, 0) <= [Time] && [Time] < TIME(21, 0, 0), "Evening",<br>
    TRUE(), "Night"<br>
)'

## Insights and Recommendation:
**📌 Customer Support and Operational Efficiency:**<br>
Given the peak purchase hours in both the afternoon and evening, it's essential to have sufficient staff available during these times for excellent customer support and efficient
order processing. Excellent CS during these hours can lead to repeat business. Consider running marketing campaigns and promotions specifically during these afternoon and
evening hours to further boost sales.

**📌 Regional Sales Analysis:**<br>
As San Francisco emerges as the leading sales city, we advise investing in a deep understanding of the factors contributing to this success. These valuable insights can then be
applied to other regions to replicate the achievements. For cities with lower sales, like Austin, conducting comprehensive market research and revisiting marketing and sales
strategies may help uncover growth opportunities. Customizing strategies to suit each region's unique characteristics and preferences is paramount.

**📌 Product Prioritization:**<br>
Recognizing that MacBook Pro Laptop, iPhone, and ThinkPad Laptop are top-performing products, we encourage the continued prioritization and promotion of these items, 
especially during the forecasted high-sales months of February, March, and April. Exploring bundling options with complementary accessories or services can maximize salespotential. For less popular products such as LG dryer and LG washing machine, it's advisable to assess their viability in the product lineup. It might be more beneficial to reallocate resources to meet the demand for higher-performing products. 

**📌 Inventory and Seasonal Sales:**<br>
Given the historical sales data and the forecasted improvement in sales for the next 15 days, we recommend proactive inventory management. Increase inventory levels for your best-selling
products during these months to meet the anticipated demand. Implement targeted marketing campaigns to promote these products, and consider offering promotions and bundles to
maximize sales. Additionally, plan well in advance for December, the peak sales month, by stocking up on popular holiday-season products. For January, when sales tend to dip, consider
adjusting your inventory strategy by reducing stock levels for products with lower demand during this time while ensuring an adequate supply of products that might still be popular post-holiday. In anticipation of the August summer holiday season, maintain a well-stocked inventory of seasonal products. However, in September, when sales tend to dip, consider offering
promotions or bundling products to stimulate sales.

---


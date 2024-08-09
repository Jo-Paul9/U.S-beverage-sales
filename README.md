# Drinks Manufacturing Sales

### Dashboard Link : https://app.powerbi.com/links/kcITYDcAwk?ctid=1a9a22ab-8b57-46a6-b007-1b47221547f1&pbi_source=linkShare&bookmarkGuid=8ed5a34e-bda2-41cb-971d-ae7b958e7d6e

## Overview

This dataset represents the sales performance of various Coca-Cola beverages across different states and regions in the United States for the year 2022. Coca-Cola, headquartered in Atlanta, Georgia, is the world’s largest beverage manufacturer and distributor, as well as one of the most iconic brands in marketing history. The focus of this report is exclusively on Coca-Cola's sales within the U.S. market during the specified period, analyzing regional variations and overall trends in beverage production and distribution.

The Drinks Manufacturing Dataset provides a comprehensive overview of beverage sales across various regions and states. This dataset encompasses sales data from multiple beverage brands, including Coca-Cola, Diet Coke, Dasani Water, Fanta, Powerade, and Sprite. The data includes essential metrics such as sales amount, units sold, price per unit, and associated costs, enabling a detailed analysis of sales performance, profitability, and regional trends.


### Problem Statement

This report provides an in-depth analysis of beverage sales across various states in the United States for Coca-Cola and its associated brands. The analysis focuses on key performance indicators (KPIs) such as revenue, profit margins, and sales growth, offering actionable insights into regional sales trends and profitability.

### Objective

The objective is to enable Coca-Cola to effectively monitor and analyze its sales performance across various retailers, regions, and states over the specified period. This includes tracking total sales, profits, and identifying the regions or states that generate the highest sales and profit margins.

The dataset initially lacked a 'Cost per Unit' (CPU) column. To accurately compute the total cost and profit, I conducted research using reliable online sources to determine the CPU for each beverage brand in 2022. The cost per unit identified through this research are as follows: 

* Coca-Cola & Diet Coke at $0.26 
* Dasani Water at $1.63 
* Fanta at $0.19 
* Powerade at $0.50 
* Sprite at $0.30. 

These values were then used for calculating the total cost and profits.




### Hypotheses Questions:

1. Identify which regions and states generate the highest sales in terms of total revenue and profits using the provided dataset.

2. Determine the month that yields the highest revenue and profits during the specified period.

3. Highlight the top-selling product across various regions and states throughout the period.

4. Analyze monthly sales and calculate the month-over-month sales growth for the given period.

5. Identify the retailer with the highest sales and profit generation on a monthly basis.

6. Determine the top and least performing states and regions based on revenue and profit from sales. 


for creating new column (Cost_per_unit) the following DAX expression was written;
       
        Cost per Unit = 
        SWITCH(
                TRUE(),
                [Beverage Brand] = "Coca-Cola", 0.26,
                [Beverage Brand] = "Diet Coke", 0.26,
                [Beverage Brand] = "Dasani Water", 1.63,
                [Beverage Brand] = "Fanta", 0.19,
                [Beverage Brand] = "Powerade", 0.50,
                [Beverage Brand] = "Sprite", 0.30,
                BLANK()  // Default case if no match
        )



        
-  New measure was created to find total count of retailers.

Following DAX expression was written for the count of retailers,
        
        Retailers = DISTINCTCOUNT('drinks_sales'[Retailer])[ID])
        
        
 -  New measure was created to total cost of drinks,
 
 Following DAX expression was written to find total cost,
 
         Total Cost = SUMX(
                drinks_sales,
                [Cost per Unit] * [Units Sold]
        )
 


 -  New measure was created to calculate total revenue of drinks across U.S.
 
 Following DAX expression was written to find total revenue,
 
         Total Rev = SUM(drinks_sales[SalesAmount])
    

 -  New measure was created to calculate total quantity sold,
        
        Total Qty = SUM(drinks_sales[Units Sold])

-   New measure was created to calculate total brand,

        Total Brand = DISTINCTCOUNT(drinks_sales[Beverage Brand])

-   New measure was created to calculate the profit,

        Profit = SUMX(
                drinks_sales,
                [SalesAmount] - ([Cost per Unit] * [Units Sold])
         )

-   New measure was created to calculate the profit %

        Profit % = DIVIDE(
                [Profit],
                SUM(drinks_sales[SalesAmount]),
                0
         )

-   New measure was created to calculate the profit margin,

        Profit Margin = DIVIDE([Profit],SUM('drinks_sales'[SalesAmount]),0)

-   New measure was created to calculate the current & previous month and quater to dates,

        Current MTD = TOTALMTD([Total Rev],DATESMTD(date_table[Date]))

        Current QTD = TOTALQTD([Total Rev],DATESQTD('date_table'[Date]))

        Previous MTD = CALCULATE([Total Rev],PREVIOUSMONTH(DATESMTD('date_table'[Date])))

        Previous QTD = CALCULATE([Total Rev],PREVIOUSQUARTER(DATESQTD('date_table'[Date])))


-   New measure was created to calculate the month over month, and month over month growth %,

        MoM = [Current MTD] - [Previous MTD]

        MoM % = DIVIDE([MoM],[Previous MTD],0)

-   New measure was created to calculate the quarter over quarter, and quarter over quarter growth %

        QoQ = [Current QTD] - [Previous QTD]

        QoQ % = DIVIDE([QoQ],[Previous QTD],0)


 -  The report was then published to Power BI Service.
 
![publish messsage](https://github.com/user-attachments/assets/8dab7c06-7d8b-47a4-b1a1-61ae41780ebc)

# Snapshot of Dashboard (Power BI Service)

![dashboard_snapshot](https://github.com/user-attachments/assets/7cb8463a-2785-4964-aae9-2cd46da9ed31)

 
 # Report Snapshot (Power BI DESKTOP)

 
![U S  beverage sales dashboard](https://github.com/user-attachments/assets/2c83d491-a78f-425d-83cf-de90a929a452)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### Key Performance Indicators (KPIs):

* Average Revenue: $2.19K
* Total Revenue: $8.2M
* Total Cost: $8.7M
* Total Quantity Sold: 16M
* Number of Retailers: 4
* Month-over-Month (MoM) Sales Growth: 30.7%
* Total Profit: $481.5K
* Number of Brands: 6
* Profit Margin: -0.06
* Profit/Loss Percentage: -5.9%
* Quarter-over-Quarter (QoQ) Sales Growth: -7.0%



### Sales Report Analysis:

The sales report provides a comprehensive view of total sales and revenue for key indicators. Users can toggle between Revenue and Profit metrics to explore different aspects of the data.

### Revenue by State:

A map visual showcases total revenue by state, with bubble sizes representing sales volume. Larger bubbles indicate higher sales in dollars, helping identify which states contribute most to overall revenue.

### Revenue by Region:

A Donut Chart visualizes total revenue by region, with the West region leading in sales at $2.4M, representing 28.85% of total sales. The Northeast follows with $1.8M (21.81%), the Southeast with $1.6M (19.57%), the South with $1.3M (15.75%), and the Midwest with $1.2M (14.02%).

### Top and Least Sales by State:

A Clustered Bar Chart identifies the top 5 and bottom 5 states by sales. New York leads with $582,675, followed closely by California at $582,400. Nebraska is the lowest, with $54,380, followed by Minnesota at $67,910.

### Revenue by Month:

An Area Chart displays revenue trends over time, with December recording the highest sales at $984,700, while March shows the lowest at $459,805.

Profit Analysis:
The profit analysis highlights the significant contributions of Q4 and Q3 to overall profitability.

### Profit by Quarter:

Q4 and Q3 were particularly strong, with notable profits in November and December. December, in particular, achieved the highest profit of $152,110, with a profit margin of 15.4%.

### Profit by State:

Washington state reported the highest profit/loss at $71,720 (28.7% profit margin), while Alabama experienced the lowest at $47,072.5, with a loss margin of -27.6%.

### Customer (Retailer) Analysis:

The analysis of revenue by retailer and brand provides insights into which entities are driving sales.

### Revenue by Retailer:

A Clustered Bar Chart reveals that Sodapop generated the highest sales at $4,389,580, while DreamCo recorded the lowest at $404,412.5.

### Revenue by Brand:

Coca-Cola emerged as the top-performing brand with $1,919,227.5 in revenue, followed by Dasani Water at $1,639,062.5. Fanta recorded the lowest revenue at $967,887.5.

### Recommendations:
Based on the analysis, several strategic recommendations are proposed:

### Regional Focus:

-  Prioritize increasing supply and sales efforts in Washington state, which showed the highest profit margins.

-  Enhance marketing and sales campaigns in the West region, where sales were highest, to maximize profitability.

### Seasonal Strategy:

-  Boost production and marketing efforts during Q4, particularly around festive seasons, as this period consistently showed higher sales and profits.

### Cost Management:

-  Consider reducing production costs for Dasani Water to improve profitability, allowing a focus on more profitable products like Coca-Cola.

### Retailer Strategy:

-  Expand marketing efforts for FizzySip, the retailer with the highest profits, to other regions. This could significantly increase overall sales and profitability.

### Pricing Strategy:

-  Encourage retailers to align their pricing strategies with those who have shown better profit margins, considering factors like marketing campaigns and regional pricing variations.

By following these recommendations, Coca-Cola can enhance its sales performance, increase profitability, and strategically expand its market presence across the United States. 






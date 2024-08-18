# Supermarket-Sales-Analysis
## Project Summary
This dashboard gives insights into the sales performance of a supermarket. The dashboard covers various metrics highlighting the sales performance with respect to the profit by product, location, etc. It also gives insight into the returned orders and changes in the number in comparison to the previous year. The data dictates that it drops by 2.95% in comparison to the previous year. Moreover, highlights the increase in sales and profit.
## Data Preparation and Modelling
The data consists of two tables that were imported into Power BI for cleaning and deriving insights. The tables have information on the orders and their IDs to track the return orders.
### Data Modelling
The model contains two tables joined together in a relationship of many-to-many with a date table created using the DAX expression and the rest of the DAX expressions to calculate the metrics are confined in  the measure table as shown below:
#
![model](https://github.com/user-attachments/assets/491ba02d-6116-4366-acfa-8e4bbab66925)
### Measure Table
Measure table keeps all the measures in a single place to keep the workspace tidy. The measure table contains all the DAX expressions that are used to calculate the metrics that are essential to deliver the insight for the dashboard. The DAX expressions used for this dashboard are briefly discussed below:
#
**Profit:** The sum of all the profits gained on each transaction id. It is represented by:
```
Profit = SUM(Orders[Profit])
```
**Profit Previous Year:** This calculates the profit for the last year.
```
Profit Previous Year = 
CALCULATE(
    [Profit],
    SAMEPERIODLASTYEAR( 'Date Table'[Date]))
```
**Change in Previous Year Profit:** The expression gives the difference between the profit earned and the amount of profit earned last year.
```
Change Previous Year Profit = 
DIVIDE( [Profit] - [Profit Previous Year],
[Profit Previous Year])
```
**Sales:** Total sales done by the supermarket.
```
Sales = SUM(Orders[Sales])
```
**Sales Previous Year:** The amount of Sales done during the past year.
```
Sales Previous Year = 
CALCULATE(
    [Sales],
    SAMEPERIODLASTYEAR( 'Date Table'[Date]))
```
**Change in Previous Year Sales:** The difference in sales between the current and the last year.
```
Change Previous Year Sales = 
DIVIDE( [Sales] - [Sales Previous Year],
[Sales Previous Year])
```
**Percentage of Returned Orders:** This expression makes use of the relationship between the two tables hence enabling the tracking down of returned orders.
```
% of Returned Orders = 
 VAR total_order = DISTINCTCOUNT(Orders[Order ID])
 VAR returned_order = DISTINCTCOUNT(Returns2[Order ID])
 VAR percentage = DIVIDE( 
    returned_order, total_order)
RETURN
percentage
```
**Percentage of Returned Orders Previous Year: Similarly, to evaluate the returned orders during the previous year.
```
% of Returned Orders Previous Year = 
CALCULATE(
    [% of Returned Orders],
    SAMEPERIODLASTYEAR( 'Date Table'[Date]))
```
**Change in Previous Year Returned Orders: Finally, evaluation of the change in returned orders for the previous year. This metric can be a performance indicator for the supermarket.
```
Change Previous Year Return Orders = 

[% of Returned Orders] - [% of Returned Orders Previous Year]
```
## Dashboard Overview
In addition to the KPIs calculated through DAX expressions, this dashboard exhibits the key metrics such as sales by current year and previous year in a time series graph. Moreover, it illustrates the sales by product and each product segment. It also shows which states are more profitable than the others so we can further analyse the states with the least profit so that, the stakeholders can bring a solution that would eventually positively impact the sales growth.
#
![sales](https://github.com/user-attachments/assets/d2bc27ea-6f1c-45f6-9942-1975cc7b8852)

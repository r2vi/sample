Furniture shop

Data source Kaggle -  https://www.kaggle.com/zhoumeixing/furniture-superstore-2017-2018

Here three tables 1) orders   2) People   3) Returns

Step 1 – Connecting excel file to powerbi

Step 2- transform in power query editor 
Here order table  includes Product ID, product category, sub-category, Product name so I created sperate product dimension table by duplicating the orders table and removing all others columns and also removing these columns in order table and Product is the relation b/w this two tables

In the same way customers table – customer Id, customer name, segment, city, state, region.


=>  here there is no relationship orders and returns data because orders are from 2017 & 2018 years but returns are from 2012, 2013, 2014, 2015 
In returns table we extract the year from Order ID, 
So both are Independent tables no relationship among them 

Step 3 – There is blank cell in ship date & it is same day delivery so order date = ship date. Using if statement fill the blank cell with order date.
Ship date 1 = 
IF(Orders[Ship Date] = BLANK(),
  'Orders'[Order Date],
 Orders[Ship Date].[Date]
)

 ![m1](https://user-images.githubusercontent.com/86475444/138491158-b7acfa30-cdec-4a2f-978e-ff9d33da6b03.gif)




Step 4 – creating date table
Date = 
ADDCOLUMNS(
    CALENDAR(DATE(2017,1,1),DATE(2018,12,31)),
    "Year", YEAR([Date]),
    "Quarter", "Q" & QUARTER([Date]),
    "quarterNo", QUARTER([Date]),
    "Month No", MONTH([Date]),
    "Month", FORMAT([Date], "MMM"),
    "Day", FORMAT([Date], "DDD"),

)


Now we have customers, Date, Orders, Product, Returns table are there. (we remove people table because customers table is same).


Step 5 - 
For checking the number of return for specific time period 
Count returns = 
COUNTROWS(Returns)



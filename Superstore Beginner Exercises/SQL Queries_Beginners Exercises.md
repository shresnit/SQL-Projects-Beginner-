**SQL Beginner's Exercises - Super Store**
-------------------------------------------------------------
*The data for the exercises are in the Root Folder of this Project*
<br>
<br>
<br>

**Exercise 1** <br>
Select ALL the records from SUPERSTORE

        SELECT * 
        FROM SUPERSTORE
        ;

**Result** <br>
*Result is too large to display*
<br>
<br>


**Exercis 2** <br>
Select ALL the records from Superstore_Orders <br>
        --That are in the East Region<br>
        --That has a profit value greater than 200
        --Limit to 10

        SELECT * 
        FROM SUPERSTORE
        WHERE Region = 'East' AND PROFIT>200
        Limit 10
        ;

**Result** <br>
|ROW_ID|ORDER_ID      |ORDER_DATE|SHIP_DATE |SHIP_MODE     |CUSTOMER_ID|CUSTOMER_NAME  |SEGMENT    |COUNTRY      |
|------|--------------|----------|----------|--------------|-----------|---------------|-----------|-------------|
|55    |CA-2020-105816|2020-12-11|2020-12-17|Standard Class|JM-15265   |Janet Molinari |Corporate  |United States|
|319   |CA-2018-164973|2018-11-04|2018-11-09|Standard Class|NM-18445   |Nathan Mautz   |Home Office|United States|
|354   |CA-2020-129714|2020-09-01|2020-09-03|First Class   |AB-10060   |Adam Bellavance|Home Office|United States|
|370   |CA-2020-155516|2020-10-21|2020-10-21|Same Day      |MK-17905   |Michael Kennedy|Corporate  |United States|
|434   |CA-2020-127369|2020-06-06|2020-06-07|First Class   |DB-13060   |Dave Brooks    |Consumer   |United States|
|881   |CA-2021-111689|2021-11-30|2021-12-02|Second Class  |HP-14815   |Harold Pawlan  |Home Office|United States|
|925   |CA-2020-149797|2020-09-15|2020-09-20|Standard Class|AH-10075   |Adam Hart      |Corporate  |United States|
|1002  |CA-2019-124891|2019-07-31|2019-07-31|Same Day      |RH-19495   |Rick Hansen    |Consumer   |United States|
|1022  |CA-2019-124450|2019-04-27|2019-05-03|Standard Class|GT-14710   |Greg Tran      |Consumer   |United States|
|1023  |CA-2019-124450|2019-04-27|2019-05-03|Standard Class|GT-14710   |Greg Tran      |Consumer   |United States|
<br>
<br>


**Exercise 3** <br>
Select Unique Products from Superstore_Orders<br>
        --Those were sold in the South or Central Region  
        --That has a Sales value greater than 200 and less than 300  

        SELECT DISTINCT PRODUCT_ID,
            REGION,
            SALES
        FROM SUPERSTORE
        WHERE (REGION = 'South' OR REGION = 'Central') AND (SALES > 200 AND SALES < 300)


**Exercise 4** <br>
Select Unique Products from Superstore_Orders  
        --That have the letter ‘b’ in.  
        --Give two answers, one that is case sensitive and one that is case insensitive.  

--case sensitive
        
        SELECT DISTINCT PRODUCT_ID,
            PRODUCT_NAME
        FROM SUPERSTORE
        WHERE product_name like '%b%'
        ;

--case insensitive
        
        SELECT DISTINCT PRODUCT_ID,
            PRODUCT_NAME
        FROM SUPERSTORE
        WHERE lower(product_name) like '%b%' -- can also use 'ilike' function in Snowflake, recommend to use standard SQL 
        ;


**Exercise 5**  
Select ALL records from Superstore_Orders  
        --That are unprofitable  
        --That are either in the Central Region or in New York State  

        SELECT ROW_ID,
            PROFIT,
            REGION,
            STATE
        FROM SUPERSTORE
        WHERE PROFIT <= 0 AND (REGION = 'Central' OR STATE = 'New York')
        ;


**Exercise 6**  
Find the 10 largest sales values in Superstore_Orders  
        --One answer using TOP and another using LIMIT  
        --Remember to ORDER BY  

--Top

        SELECT TOP 10 ROW_ID,
            ORDER_ID,
            SALES
        FROM SUPERSTORE
        ORDER BY SALES DESC
        ;

--Limit

        SELECT ROW_ID,
            ORDER_ID,
            SALES
        FROM SUPERSTORE
        ORDER BY SALES DESC
        LIMIT 10
        ;


**Exercise 7**  
Find the Total Sales & Profit for each Region  

        SELECT REGION,
                SUM(SALES) AS Total_Sales,
                SUM(PROFIT) AS Total_Profit
        FROM SUPERSTORE
        GROUP BY REGION
        ;


**Exercise 8**  
Find the Average Discount by Segment & Ship Mode  
        --Alias the Avg Discount to something of your choice.  
        --Order from highest to lowest Avg Discount.  

         SELECT SEGMENT,
            SHIP_MODE,
            AVG(DISCOUNT) AS Average_Discount
         FROM SUPERSTORE
         GROUP BY SEGMENT, SHIP_MODE
         ORDER BY Average_Discount DESC
         ;


 **Exercise 9**  
 For the Central Region  
        --Find the Minimum Profit value per Sub-Category  
        --Alias the Minimum Profit field  
        --Order from lowest profit value to highest  

            SELECT REGION,
                SUB_CATEGORY,
                MIN(PROFIT) AS Minimum_Profit
            FROM SUPERSTORE
            WHERE REGION = 'Central'
            GROUP BY REGION, SUB_CATEGORY 
            ORDER BY Minimum_Profit ASC
            ;


 **Exercise 10**  
 Which Order Dates had a total profit greater than 2000?  
        --Alias your profit aggregation  
        --Sort from highest to lowest profit  

         SELECT ORDER_DATE,
            SUM(PROFIT) AS Total_Profit
         FROM SUPERSTORE
         GROUP BY ORDER_DATE
         HAVING SUM(PROFIT) > 2000
         ORDER BY Total_Profit DESC
         ;

 **Exercise 11**  
 For the Central Region, which Products had an average profit less than -400?  
        --Alias your profit aggregation  
        --Sort from lowest to highest avg profit  

         SELECT REGION,
            PRODUCT_ID,
            AVG(PROFIT) AS Avg_Profit
         FROM SUPERSTORE
         WHERE REGION = 'Central'
         GROUP BY REGION, PRODUCT_ID
         HAVING AVG(PROFIT) < -400
         ORDER BY Avg_Profit ASC
         ;


 **Exercise 12**  
 For Florida State in the Superstore_Joined table  
        --Find the total Sales value of items returned and not returned SUM(“Sales”)  
        --Find the total number of items returned and not returned COUNT(“Product Name”)  
        --Alias your fields  

         SELECT 
            IFF(RETURNED = 'Yes', 'Returned', 'Not returned') AS Return_Status,
            SUM(SALES) AS Total_Sales,
            COUNT(S.PRODUCT_NAME) AS Total_ItemCounts
         FROM SUPERSTORE AS S
         LEFT JOIN RETURNED_ORDERS AS R
         ON S.ORDER_ID = R.ORDER_ID
         WHERE STATE = 'Florida'
         GROUP BY R.RETURNED
         ;

 **Exercise 13**  
 For the Furniture Category in the Superstore_Joined table  
        --Find the top 10 order values for orders with a profit < 0 (Is Value Number of items in an order OR Total Sales of Order ID?? )  
        --Ensure the orders have not been returned
        --Alias your fields  

    
         SELECT TOP 10 S.ORDER_ID,
            IFF(RETURNED = 'Yes', 'Returned', 'Not returned') AS Return_Status,
            COUNT(PRODUCT_ID) AS Order_Values,
            SUM(PROFIT) AS Total_Profit
         FROM SUPERSTORE AS S
         LEFT JOIN RETURNED_ORDERS AS R
         ON S.ORDER_ID = R.ORDER_ID
         WHERE CATEGORY = 'Furniture'
         GROUP BY S.ORDER_ID, RETURNED
         HAVING SUM(PROFIT) < 0 AND IFF(RETURNED = 'Yes', 'Returned', 'Not returned') = 'Not returned'
         ORDER BY Order_Values DESC
         ;


 **Exercise 14**  
 Join Superstore_Orders to Superstore_Returns, selecting all columns.  
        --First do an Inner Join  
        --Then do a Left Join  
        --Then a Right Join  
        --Does the output change? And how? Why is it changing?  


-- Inner Join  

         SELECT *
         FROM SUPERSTORE AS S
         INNER JOIN RETURNED_ORDERS AS R
         ON S.ORDER_ID = R.ORDER_ID
         ;

  Note Inner join resulted in 3226 records. Matching records on both tables based on ORDER_ID.


         --Left Join
         SELECT *
         FROM SUPERSTORE AS S
         LEFT JOIN RETURNED_ORDERS AS R
         ON S.ORDER_ID = R.ORDER_ID
         ;

  Note: Left join resulted in 12420 records. Matching records from RETURNED_ORDERS table and all records FROM SUPERSTORE table based on ORDER_ID.


 --Right Join
 
         SELECT *
         FROM SUPERSTORE AS S
         RIGHT JOIN RETURNED_ORDERS AS R
         ON S.ORDER_ID = R.ORDER_ID
         ;

 Note: Right join resulted in 3226 records. Matching records from SUPERSTORE table and all records FROM RETURNED_ORDERS table based on ORDER_ID.  
 The result of the INNER and RIGHT join is the same because all the records from the RETURNED_ORDERS matched with the SUPERSTORE table.



**Exercise 15 PART 1**  
Join CUSTOMERS to CUSTOMER_SALES_REP  
        -- Can you work out how many customers do not have a Sales representative?   
        -- HINT: Use a LEFT JOIN.  

        SELECT COUNT(L.CUSTOMER_ID) AS Number_of_Customer
        FROM CUSTOMERS AS L
        LEFT JOIN CUSTOMER_SALES_REP AS R
        ON L.CUSTOMER_ID = R.CUSTOMER_ID
        WHERE IFF(R.sales_person_id IS NULL,'No Sales Rep', 'Sales Rep') = 'No Sales Rep'
        ;

**Exercose 15 PART 2**   
Join CUSTOMERS to CUSTOMER_SALES_REP   
        -- Can you work out how many customers do not have a Sales representative?   
        -- HINT: Use a LEFT JOIN.  
-- How could we go about counting the number of customers with and without a sales rep, creating a field to group them by?  

        SELECT IFF(R.sales_person_id IS NULL,'No Sales Rep', 'Sales Rep') AS Sales_Reps,
            COUNT(DISTINCT L.CUSTOMER_ID) AS Number_of_Customer
        FROM CUSTOMERS AS L
        LEFT JOIN CUSTOMER_SALES_REP AS R
        ON L.CUSTOMER_ID = R.CUSTOMER_ID
        GROUP BY Sales_Reps
        ;


**Exercise 15: Part 3**  
Add to your query from Part 2:  
        --Perform a further (INNER) Join to include the ORDERS table in your query.  
        --Why have the numbers changed?  

SELECT IFF(R.sales_person_id IS NULL,'No Sales Rep', 'Sales Rep') AS Sales_Reps,
    COUNT( DISTINCT L.CUSTOMER_ID) AS Number_of_Customer
FROM CUSTOMERS AS L
LEFT JOIN CUSTOMER_SALES_REP AS R
    ON L.CUSTOMER_ID = R.CUSTOMER_ID
INNER JOIN ORDERS AS O
    ON R.CUSTOMER_ID = O.CUSTOMER_ID
GROUP BY Sales_Reps
;

--Notes: As we included the Order tables the count of customer decreases and was limited to only those with Sales Rep.
        -- This number changed because only matched records were included i.e. all the customer with active orders had Sales Rep


**Exercise 16**   
Join ORDERS to PRODUCTS  
        --To find how many times each product was sold in each Year.  
        --Sort so we can see the best selling product for a given Year.  
        --HINT: In Snowflake YEAR(“date”) is a function.  
        --Remember to Alias.  

            SELECT YEAR(L.ORDER_DATE) AS Year,
                L.PRODUCT_ID,
                COUNT(*) AS TimesProductSold
            FROM ORDERS AS L
            INNER JOIN PRODUCTS AS R
                ON L.PRODUCT_ID = R.PRODUCT_ID
            GROUP BY Year, L.PRODUCT_ID
            ORDER BY TimesProductSold DESC
            ;


**Exercise 17**  
Using Superstore_Orders table  
        --How many Regions have at least 4 different States with a total Profit > 7000?

    SELECT COUNT(REGION) AS NumberOfRegion
    FROM
        (SELECT REGION, 
            COUNT( REGION) AS Count_Region
        FROM
                (SELECT REGION,
                    STATE,
                    SUM(PROFIT) AS Total_Profit
                FROM SUPERSTORE
                GROUP BY REGION, STATE
                HAVING SUM(PROFIT) > 7000
                ORDER BY REGION, STATE)
        GROUP BY REGION)
    WHERE COUNT_REGION >= 4
    ;
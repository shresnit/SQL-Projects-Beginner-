#Danny's Dinner

#Week 1 | Challenge

**Question 1** What is the total amount each customer spent at the resturant?

	  SELECT sales.customer_id AS "Customer ID"
		,sum(menu.price) AS "Total Amount"
	  FROM sales
		INNER JOIN menu ON sales.product_id = menu.product_id
	  GROUP BY customer_id;
  
  **Result**
  
  |Customer ID|Total Amount|
  |---|---|
  |A|76|
  |B|74|
  |C|36|
  
  
  

**Question 2** How many days has each customer visited the restaurant?

	SELECT sales.customer_id AS "Customer"
	, COUNT(DISTINCT [order date]) AS "Number of Days"
	FROM sales
	GROUP BY customer_id;
	
**Result**

|Customer|Number of Days|
|---|---|
|A	|4
|B	|6
|C	|2

  

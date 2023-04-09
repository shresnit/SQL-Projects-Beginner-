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



**Question 3** What was the first item from the menu purchased by each customer?

	SELECT TOP(4) sales.customer_id AS "Customer"
		, (sales.[order date]) AS "Order Date"
		, menu.product_name AS "Item"
	FROM sales INNER JOIN menu ON sales.product_id = menu.product_id
	ORDER BY sales.[order date]
	;
	
**RESULT**

|Customer|Order Date|Item|
|---|---|---|
|A	|2021-01-01	|sushi|
|A	|2021-01-01	|curry|
|B	|2021-01-01	|curry|
|C	|2021-01-01	|ramen|


**Question 4** What is the most purchased item on the menu and how many times was it purchased by all customers?


	SELECT sales.customer_id AS "Customer"
		, menu.product_name AS "Item"
		, COUNT(menu.product_name) AS "# of items"
	FROM menu INNER JOIN sales ON menu.product_id = sales.product_id
	WHERE sales.product_id = ( SELECT TOP(1) product_id 
						FROM sales
						GROUP BY product_id
						ORDER BY count(product_id) DESC)
	GROUP BY customer_id, menu.product_name
	;

 **RESULT**
 
 |Customer|Item|# of items|
 |---|---|---|
 |A	|ramen	|3|
 |B	|ramen	|2|
 |C	|ramen	|3|

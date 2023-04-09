**Question 1** What is the total amount each customer spent at the resturant?

  SELECT sales.customer_id AS "Customer ID"
		,sum(menu.price) AS "Total Amount"
  FROM sales
	INNER JOIN menu ON sales.product_id = menu.product_id
  GROUP BY customer_id;
  
  |Customer ID|Total Amount|
  |---|---|
  |A|76|
  |B|74|
  |C|36|
  
  

**Query #1** What is the total amount each customer spent at the restaurant?

    SELECT sa.customer_id, SUM(me.price) as Total_Spend
    FROM dannys_diner.sales sa
    INNER JOIN dannys_diner.menu me
    ON sa.product_id = me.product_id
    GROUP BY sa.customer_id;

| customer_id | total_spend |
| ----------- | ----------- |
| B           | 74          |
| C           | 36          |
| A           | 76          |

| id	| (Value * -1)| 
| ----- | ----------- |
| 1	    | 56		  | 	
| 2	    | -76		  | 
| 3	    | 84		  | 
| 4	    | -96		  | 
| 5	    | 47		  |

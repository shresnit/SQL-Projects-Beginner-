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

A	2021-01-01	1
A	2021-01-01	2
A	2021-01-07	2
A	2021-01-10	3
A	2021-01-11	3
A	2021-01-11	3
B	2021-01-01	2
B	2021-01-02	2
B	2021-01-04	1
B	2021-01-11	1
B	2021-01-16	3
B	2021-02-01	3
C	2021-01-01	3
C	2021-01-01	3
C	2021-01-07	3

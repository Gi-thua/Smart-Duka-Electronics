## Smart Duka Electronics Performance Dashboard

<img width="350" height="250" alt="Smartduka electronics assignment" src="https://github.com/user-attachments/assets/a419b776-64f3-45f1-acc1-909e380d0eca" />





## Original SQL query for optimization

`select c.customer_id, c.customer_name,
SUM(quantity * unit_price * (1 - discount / 100)) as total_revenue
from customers c
join orders o
on c.customer_id = o.customer_id
where o.order_status = 'Completed'
group by c.customer_id, c.customer_name
order by total_revenue desc;`

## EXPLAIN ANALYZE output.

<img width="350" height="250" alt="ExplainAnalyze" src="https://github.com/user-attachments/assets/d861df06-0439-4ff2-b9c3-a681b44b0d7f" />

## CREATE INDEX statement

`CREATE INDEX idx_orders_completed_customer
ON orders (customer_id)
INCLUDE (quantity, unit_price, discount)
WHERE LOWER(order_status) = 'completed';`

## EXPLAIN ANALYZE output.

<img width="350" height="250" alt="ExplainAnalyzeAFINDEX" src="https://github.com/user-attachments/assets/b0e2cc77-3e27-41ed-bb17-dbafde3da4c7" />


I used EXPLAIN ANALYZE command to examine the execution plan and performance of a query that calculates completed-order revenue for each customer. The initial execution plan was examined to identify opportunities for optimization. I then created a partial covering index on the orders table using customer_id and included the quantity, unit_price and discount columns. The index was designed to improve filtering and joining of completed orders. After creating the index, I updated the table statistics using ANALYZE and executed the same query again. I compared the execution times and execution plans before and after indexing to determine whether query performance improved.

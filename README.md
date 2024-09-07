# SQL-AND-POWER-BI-PIZZA-SALES-PROJECT
PIZZA SALES DASHBOARD-SQL+POWER BI

Select * from pizza_sales$
Select Sum(total_price) as Total_Revenue from pizza_sales$

2-Average Order Value
Select Sum(Total_price)/count(distinct order_id) as Average_ordervalue from pizza_sales$

3-Total Pizza Sold

Select sum(quantity) as Total_pizza_sold from pizza_sales$

4-Total Order Placed

Select Count(distinct order_id) as Total_orders from pizza_sales$

5-Average Pizza per order

Select round(sum(quantity)/count(distinct order_id),2) as Avg_pizza_perorder from pizza_sales$

6-Total Trend per order

Select DATENAME(weekday,order_date) as Days_name,count(distinct order_id) as Total_orders from pizza_sales$
group by DATENAME(weekday,order_date)
order by count(distinct order_id) 

7-Monthly trend per order

Select DATENAME(MONTH,order_date) as Month_name,count(distinct order_id) as Total_orders from pizza_sales$
group by DATENAME(MONTH,order_date)
order by count(distinct order_id) desc

8-Percentage of sales by pizza category

with total_price_cat as
(
Select pizza_category,Sum(total_price)as Total_price from pizza_sales$
group by pizza_category
)
Select pizza_category,Total_price,(100*total_price/(select sum(total_price) from pizza_sales$))
as Percentage_sales from total_price_cat

9-Percentage of Sales by Pizza Size

with Pizza_size as
(
Select pizza_size,round(Sum(total_price),2) as Total_salesbysize from pizza_sales$
Group by pizza_size
)
Select pizza_size,Total_salesbysize,round((100*Total_salesbysize)/
(select sum(total_price) from pizza_sales$),2) as Per_persize from Pizza_size
order by Total_salesbysize desc

10-Top 5 best sellers by revenue,total qty and total orders

Select * from pizza_sales$

Select Top 5 pizza_name,sum(total_price) as total_revenue
from pizza_sales$
group by pizza_name
order by sum(total_price) 

Select Top 5 pizza_name,sum(quantity) as Total_Qty
from pizza_sales$
group by pizza_name
order by sum(quantity)  desc

Select Top 5 pizza_name,Count(distinct order_id) as  Total_orders 
from pizza_sales$
group by pizza_name
order by Count(distinct order_id)  desc

# Retail Sales Data Analysis Using SQL
##  Overview
This project focuses on analyzing retail sales data using SQL to derive meaningful insights. The dataset includes information about transactions, customer demographics, sales details, and product categories. The analysis helps answer various business questions related to sales performance, customer behavior, and revenue trends.
## Objectives
- Calculate total sales and unique customer counts.
- Analyze sales trends across different product categories.
- Identify the best-performing months and peak selling times.
- Find top customers based on sales contribution.
- Generate category-wise and gender-based sales insights.
## Key Insights
- ✔ Top-selling categories and their revenue contribution.
- ✔ Customer purchasing behavior based on demographics.
- ✔ Peak sales hours and best-selling months.
- ✔ High-value transactions and top customers.
## Technologies Used 
- SQL (MySQL / PostgreSQL)
- Data Analysis Queries
- Aggregations and Window Functions
```
create database project;

CREATE TABLE reatail_sales 
( 
transactions_id int primary key,
sale_date date,
sale_time time,
customer_id int,
gender varchar(255),
age INT ,
category varchar(255),
quantiy int,
price_per_unit decimal(10,2),	
cogs decimal(10,2),
total_sale decimal(10,2)
);
```
## how many sales we have?
```
select count(*) as total_sales from reatail_sales;
```
## how many uniq custumors we have ?

```
select count(distinct customer_id) as total_customers from reatail_sales;
```
## category types?
```
select distinct category as catrgory_name from reatail_sales;
```
## data analyasis and bussines problems ?
## My Analysis & Findings

## Q.1 Write a SQL query to retrieve all columns for sales made on '2022-11-05
```
select * from reatail_sales
where sale_date = '2022-11-05' ;
```

## Q.2 Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is morethan or equals to 4 in the month of Nov-2022
```
select *from reatail_sales
where category= 'Clothing' 
and quantiy >=4 
and sale_date between '2022-11-01' and '2022-11-30'
 order by sale_date ;
```
 
 ## Q.3 Write a SQL query to calculate the total sales (total_sale) for each category.
 
```
select distinct category ,sum(total_sale) from reatail_sales
group by category;
```
## Q.4 Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.
```
select category,avg(age) as average_age from reatail_sales
where category = 'beauty' ;
```
## Q.5 Write a SQL query to find all transactions where the total_sale is greater than 1000.
```
select * from reatail_sales
where total_sale > 1000 order by total_sale;
```
## Q.6 Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.
```
select category,gender,count(transactions_id) as total_transactions from reatail_sales
group by gender , category order by category;
```
## Q.7 Write a SQL query to calculate the average sale for each month. Find out best selling month in each year
```
 select sale_year,sale_month,round(average_sale) 
 from (
     select
         year(sale_date) as sale_year,
         month(sale_date) as sale_month,
		avg (total_sale) as average_sale ,
         rank() over (partition by year(sale_date) order by avg(total_sale) desc) as sale_rank 
      from reatail_sales
      group by year(sale_date),month(sale_date) 
 )  as t1
 
 where sale_rank = 1 order by sale_year , sale_month;
 ```
 ## Q.8 Write a SQL query to find the top 5 customers based on the highest total sales 
``` 
select customer_id, sum(total_sale) as highest_sale from reatail_sales
group by customer_id
order by highest_sale desc limit 5;
```
## Q.9 Write a SQL query to find the number of unique customers who purchased items from each category.
```
select category , count(distinct customer_id) as unique_customers from reatail_sales
group by category;
```
## Q.10 Write a SQL query to create each shift and number of orders (Example Morning <=12, Afternoon Between 12 & 17, Evening >17)
```
select 
	case 
		when hour(sale_time) <= 12 THEN 'morning'
        when hour(sale_time) between 12 and 17 then 'afternoon'
        else 'evening' 
end as shift,
count(*) number_of_orders from reatail_sales
 group by shift;
 ```
## Q.11 write an sql query to find total sales of perticular customer in each categorty 
```
 select * from reatail_sales order by customer_id;
 select sum(total_sale) as tota_sales , customer_id,category from reatail_sales
 where customer_id = 33
 group by category;
```
## Finding & Conclusion
- 📌 The Clothing category had the highest number of transactions, while Electronics generated more revenue per sale.
- 📌 Sales peaked in the afternoon shift (12 PM – 5 PM), with lower activity in the morning.
- 📌 A few high-value customers contributed significantly to total revenue.
- 📌 Monthly sales trends indicate seasonal demand, helping plan inventory and marketing.
  
  -- ----------------------------------------------------------------  END  --------------------------------------------------------------------- --
 
        























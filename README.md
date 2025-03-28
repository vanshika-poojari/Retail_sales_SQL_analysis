# Retail_sales_SQL_analysis

create database retail_sale; 

-- total sales 

          select count(total_sale) from retail_table; 

-- number of unique customers 

        select count(distinct(customer_id)) from retail_table; 

-- number of unique category 

        select count(distinct (category)) from retail_table;

-- data analysis based on KPIs solving key problems 
-- Write a SQL query to retrieve all columns for sales made on '2022-11-05:


        select * from retail_table where sale_date = '2022-11-05' ; 

-- Write a SQL query to retrieve all transactions where the category is 'Clothing' 
-- and the quantity sold is more than 4 in the month of Nov-2022:

        select * from retail_table where category = 'Clothing' AND
        quantiy >= 4 AND Month(sale_date) = '11'; 

-- Write a SQL query to calculate the total sales (total_sale) for each category.:

        select sum(total_sale) , category from retail_table 
        group by category ; 

-- Write a SQL query to find the average age of customers 
-- who purchased items from the 'Beauty' category.:


        select round(avg(age),2) as avg_age from retail_table where category = 'Beauty' ; 

-- Write a SQL query to find all transactions where the total_sale is greater than 1000.:

      select ï»¿transactions_id as transactions, total_sale  from retail_table where total_sale >= 1000; 

-- Write a SQL query to find the total number of transactions 
-- (transaction_id) made by each gender in each category.:

      select gender, category , sum(ï»¿transactions_id) total_transactions from retail_table 
      group by gender, category
      order by gender; 



        select year (sale_date) as years, month(sale_date) as months, round(avg(total_sale)) as avg_sale from retail_table
        group by years, months 
        order by years, months; 

-- **Write a SQL query to find the top 5 customers based on the highest total sales **:

        select customer_id , (sum(total_sale)) as total_sale from retail_table 
        group by customer_id
        order by  total_sale DESC LIMIT 5 ; 

-- Write a SQL query to find the number of unique customers who purchased items from each category.:

        select count(distinct customer_id) unique_customer, category from retail_table 
        group by category; 

-- Write a SQL query to create each shift and number of orders 
-- (Example Morning <12, Afternoon Between 12 & 17, Evening >17):


        with hourly_sale as (select * , 
        case 
        when extract(hour from sale_time) < 12 then 'Morning' 
        when extract(hour from sale_time) between 12 and 17 then 'Afternoon' 
        else 'Evening'
        end as shift from retail_table
        ) select shift, count(*) as total_orders from hourly_sale 
        group by shift ; 

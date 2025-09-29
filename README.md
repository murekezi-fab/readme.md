                                         Window Functions Mastery Project
Step 1 Problem Definition
The problem of business scenario is DATA Challenge 
Our analysis needs to identify the top 3 best-selling products by revenue within each sales region for the last quarter. The problem we have is that we have to rank products within their specific regions, not globally.  Also we need to calculate the total revenue of each product.
 Here there are the business context
Company Type: (Niyibizi Tech solutions) a multinational electronics retailer 
Departments: Marketing & inventory management 
Industry:  E-commerce & Retail.
       What this business context are expected to help the business 
For Marketing Department: the target is to list the top-performing products per region to focus on localized digital advertising campaigns and promotional offers.
For Inventory Management Department: the Data to validate and optimize regional warehouse stock levels, ensuring high availability for top sellers while reducing overstock of slower-moving items 
Step 2: Success Criteria
1.	Top 5 products per region/quarter → RANK (): we use this to identify the best-selling electronics items in each region every quarter 
2.	2. Running monthly sales totals → SUM () OVER (): we will use this to calculate cumulative monthly sales totals to truck growth.
3.	Month-over-month revenue growth per product → we will apply LAG ()/LEAD () to compare each products revenue against the previous month and compare growth %
4.	Customer segmentation by spend classify customers into 4 quartiles (25% groups) with NTILE (4) based on lifetime electronics purchases.
5.	3-month moving average sales per product use → AVG () OVER () to smooth fluctuations in electronics sales trends 
Step 3: Database Schema
Design minimum 3 related tables with foreign keys
for the information related to customers will be stored in this table
<img width="544" height="263" alt="image" src="https://github.com/user-attachments/assets/b98e7e3f-318f-4f3d-8d95-941cd7966a99" />


Here there are table which store data from products
 
Also this is the table which show the information for transactions
 
Here we have the image which shows the entity relationship of those three tables 
 

Step 4: Window Functions Implementation
For Ranking: we start with: ROW_NUMBER ()
This is the codes used to ranking with ROW_NUMBER ()
select customer_ID, customer_names,region
 ,ROW_NUMBER() OVER(ORDER BY customer_names ASC) RNR from CUSTOMER; 
Here there are the screen shoot of how the table arranged
  

For Ranking with using RANK ()
This is the codes used to ranking with RANK ()
select customer_ID, customer_names,region
 ,RANK() OVER(ORDER BY customer_names ASC) RNK from CUSTOMER;
Here there are the screen shoot of how the table arranged
 
For Ranking with using DENSE_RANK ()
This is the codes used to ranking with DENSE_RANK ()
select customer_ID, customer_names,region
 ,DENSE_RANK() OVER(ORDER BY customer_names ASC) DRK from CUSTOMER;

Here there are the screen shoot of how the table arranged
 
For Ranking with using PERCENT_RANK ()
This is the codes used to ranking with PERCENT_RANK ()

select customer_ID, customer_names,region
 ,PERCENT_RANK() OVER(ORDER BY customer_names ASC) PRK from CUSTOMER;
Here there are the screen shoot of how the table arranged
 
By showing the image of ranking with using all categories hare there are screen shoot which show it 
    
 
   HERE THERE ARE THE SREEN SHOOT WHICH SHOWS HOW THE TABLES ARE JOINED 
FOR THE FIRST WE JOINED CUSTOMER TABLES WITH TRANSACTIONS TABLE THIS IS HOW IT LOOKS LI
 
So after joining table we are going to the step of AGGREGATE
Aggregate      FOR SUM () OF amount which are received in our company 
This table sum the total amount but also grouped by  customer_id and product_id





For the second aggregate of AVG () for average amount we calculated the average amount for every customer but are grouped by customer_id and product_id here we have the screen shoot that shows how the output is that I it for avg () in SQL
  
For min () is the other step we are going to show how it looks. Therefore we are going to looks like
 
The next is to find the max () amount in the transactions table 
Here we have the screen shoot of table which shows maximum amount 
 
For the other aggregate we are going to check for ROWS vs RANGE
For ROWS this is the table which shows how the rows are ordered by using amount
 
For RANGE here we have the screen shoot of how the table of range must look like
 

Navigation: LAG (), LEAD ()
We start with LAG () this is the table which shows the LAG () IN our table of transactions

 
For the next we are going to se the LEAD () navigation 
 
Distribution: NTILE (4), CUME_DIST ()
We have come from the distribution of our tables 
We are going to start with NTILE (4 here we have the screen shoot of how this function are shown and used 

	
 
After using NTILE (4 we are going to use the other navigation which called 
CUME_DIST () as we use this function here we have the screen shoot of our table which shows it in good way 
 

 

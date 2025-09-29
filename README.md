                                         Window Functions Mastery Project
 ## INTRODUCTION 
- *NAME:* MUREKEZI SANGWA Fabrice
- *Id:* 28395
- *course:* DATABASE DEVELOPMENT WITH PL/SQL INSY 8311 

---
   
## step 1: Problem definition 

The problem of business scenario is DATA Challenge Our analysis needs to identify the top 3 best products by revenue within each sales region for the last quarter. The problem we have is that we have to rank sellers within their specific regions, not globally.  Also we need to calculate the total revenue of each seller.
Here there are the business context
Company Type: (1000 hills entreprise) a multinational  retailer 
Departments: Marketing & Sales management 
Industry:  E-commerce & Retail.What this business context are expected to help the business For Marketing Department: the target is to list the top-performing products per region to focus on localized digital advertising campaign and promotional offers.
For Sales Management Department: the Data to validate and optimize regional accounting levels, ensuring high availability for top buyers while reducing overstock of slower-moving items

## Success Criteria 

1.	Top 5 products per region/quarter → RANK (): we use this to identify the best-selling electronics items in each region every quarter 
2.	2. Running monthly sales totals → SUM () OVER (): we will use this to calculate cumulative monthly sales totals to truck growth.3.	Month-over-month revenue growth per product → we will apply LAG ()/LEAD () to compare each products revenue against the previous month and compare growth %
4.	Customer segmentation by spend classify customers into 4 quartiles (25% groups) with NTILE (4) based on lifetime electronics purchases.
5.	3-month moving average sales per product use → AVG () OVER () to smooth fluctuations in electronics sales trends

6.	## Database Schema

7.	for the information related to customers will be stored in this table

<img width="489" height="197" alt="image" src="https://github.com/user-attachments/assets/a3f6f5ef-4b96-4f58-91cc-b405cdaae61f" />

Here there are table which store data from products

<img width="369" height="154" alt="image" src="https://github.com/user-attachments/assets/bfcb6871-4d7e-40cf-9e26-9b0efb681c6b" />

Also this is the table which show the information for transactions

<img width="556" height="151" alt="image" src="https://github.com/user-attachments/assets/88326ffa-ff05-4c49-817b-5e74647530ee" />

Here we have the image which shows the entity relationship of those three tables 

<img width="608" height="237" alt="image" src="https://github.com/user-attachments/assets/839c1fdf-93f4-462d-8b1a-0bc250358a7c" />

## Window Functions Implementation

For Ranking: we start with: ROW_NUMBER ()
This is the codes used to ranking with ROW_NUMBER ()
select customer_ID, customer_names,region
 ,ROW_NUMBER() OVER(ORDER BY customer_names ASC) RNR from CUSTOMER; 
Here there are the screen shoot of how the table arranged

<img width="281" height="79" alt="image" src="https://github.com/user-attachments/assets/668c98e0-3891-40b0-a3a8-b8e946e135f4" />
 
For Ranking with using RANK ()
This is the codes used to ranking with RANK ()
select customer_ID, customer_names,region
 ,RANK() OVER(ORDER BY customer_names ASC) RNK from CUSTOMER;Here there are the screen shoot of how the table arranged

<img width="279" height="78" alt="image" src="https://github.com/user-attachments/assets/9347d148-12cd-46ed-9122-c32d0082f092" />

For Ranking with using DENSE_RANK ()
This is the codes used to ranking with DENSE_RANK ()
select customer_ID, customer_names,region
 ,DENSE_RANK() OVER(ORDER BY customer_names ASC) DRK from CUSTOMER;
 Here there are the screen shoot of how the table arranged
<img width="279" height="78" alt="image" src="https://github.com/user-attachments/assets/ebeb7f15-915c-486f-b903-ab744d7a2df5" />

For Ranking with using PERCENT_RANK ()
This is the codes used to ranking with PERCENT_RANK ()
select customer_ID, customer_names,region
 ,PERCENT_RANK() OVER(ORDER BY customer_names ASC) PRK from CUSTOMER;
Here there are the screenshot of how the table arranged

<img width="435" height="78" alt="image" src="https://github.com/user-attachments/assets/55f04f0c-4f6d-4474-bdfa-4c0dfbf3fa8f" />

By showing the image of ranking with using all categories hare there are screen shoot which show it 

<img width="957" height="138" alt="image" src="https://github.com/user-attachments/assets/2ded55d9-a945-465a-bdb2-7ccc0124e2f2" />

   HERE THERE ARE THE SREEN SHOOT WHICH SHOWS HOW THE TABLES ARE JOINED 
FOR THE FIRST WE JOINED CUSTOMER TABLES WITH TRANSACTIONS TABLE THIS IS HOW IT LOOKS LI
<img width="747" height="169" alt="image" src="https://github.com/user-attachments/assets/88721be8-7526-41ee-872a-c85bc1eff27a" />

So after joining table we are going to the step of AGGREGATE
Aggregate      FOR SUM () OF amount which are received in our company 
This table sum the total amount but also grouped by  customer_id and product_id

<img width="260" height="81" alt="image" src="https://github.com/user-attachments/assets/1a3a26cf-3de7-4357-8639-df14f7a6fefe" />

For the second aggregate of AVG () for average amount we calculated the average amount for every customer but are grouped by customer_id and product_id here we have the screen shoot that shows how the output is that I it for avg () in SQL
<img width="845" height="263" alt="image" src="https://github.com/user-attachments/assets/807cc7f6-f6c1-4fe5-bcbf-fd47fdd8ec02" />
For min () is the other step we are going to show how it looks. Therefore we are going to looks like

<img width="840" height="287" alt="image" src="https://github.com/user-attachments/assets/7854f2db-87b7-413e-af7c-7fb49ae0219f" />
The next is to find the max () amount in the transactions table 
Here we have the screen shoot of table which shows maximum amount 

<img width="956" height="153" alt="image" src="https://github.com/user-attachments/assets/fb3b5056-0baa-443d-b490-52033692a663" />

For the other aggregate we are going to check for ROWS vs RANGE
For ROWS this is the table which shows how the rows are ordered by using amount

<img width="529" height="190" alt="image" src="https://github.com/user-attachments/assets/73b2d1c5-ebc7-49cc-844d-148d2bfd5372" />

For RANGE here we have the screen shoot of how the table of range must look like

<img width="594" height="241" alt="image" src="https://github.com/user-attachments/assets/7b8810c9-ab13-4a0b-acb9-19ab3d8427ed" />

Navigation: LAG (), LEAD ()
We start with LAG () this is the table which shows the LAG () IN our table of transactions

<img width="852" height="153" alt="image" src="https://github.com/user-attachments/assets/f98edea8-5c4b-4ff1-b05d-bfdbcb7c0f50" />

For the next we are going to se the LEAD () navigation 

<img width="492" height="75" alt="image" src="https://github.com/user-attachments/assets/b7a79368-c42f-4962-96c9-ddd558233787" />

Distribution: NTILE (4), CUME_DIST ()
We have come from the distribution of our tables 
We are going to start with NTILE (4 here we have the screen shoot of how this function are shown and used 
<img width="872" height="198" alt="image" src="https://github.com/user-attachments/assets/3316de06-9c82-499f-ac75-c4f482060e99" />
After using NTILE (4 we are going to use the other navigation which called 
CUME_DIST () as we use this function here we have the screen shoot of our table which shows it in good way 

<img width="880" height="194" alt="image" src="https://github.com/user-attachments/assets/7276a368-d6b3-4386-8db3-1e76dd535761" />

 #Step 6 — Results Analysis 

For each major finding, present:

Descriptive: the best products ( "Top 3 products in Kigali Q1: soja — 75,000 Rwf; porke — 45,000 Rwf").

Diagnostic: factors (promotions, seasonality, customer density).

Prescriptive: solution (increase inventory, run promo to lift 2nd product).

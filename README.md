[KMS SQL Project Answers.docx](https://github.com/user-attachments/files/21048487/KMS.SQL.Project.Answers.docx)# DSA-CAPSTONE-PROJECT-SQL-
SQL CASE STUDY, KULTRA MEGA STORE
# 🏢 Kultra Mega Stores Inventory – SQL Case Study

Hello! I'm **Christina Akindino**, and this is the second part of my DSA Data Analysis Capstone project — a business intelligence case study for Kultra Mega Stores (KMS), focused on data from 2009 to 2012.

I used **SQL Server Management Studio (SSMS)** to explore sales, customer behavior, and shipping performance.

---

## 🧠 Case Overview

KMS specializes in office supplies and furniture, servicing individuals, small businesses, and corporate clients across Nigeria.

As a Junior Data Analyst, I was asked to help the Abuja division answer questions like:
- Which product categories generate the most revenue?
- What shipping method is most cost-effective?
- Who are the most profitable and loyal customers?

---

## 🛠 Tools Used

- Microsoft SQL Server Management Studio (SSMS)
- SQL: `SELECT`, `GROUP BY`, `JOIN`, `SUM`, `ORDER BY`, `IF`, `COUNT`

---

## 📌 Case Scenario I – Questions Answered

| Q# | Question |
|----|----------|
| 1  | Which product category had the highest sales? |
| 2  | What are the Top 3 and Bottom 3 regions in terms of sales? |
| 3  | What were the total sales of appliances in Ontario? |
| 4  | Advise management on how to grow revenue from bottom 10 customers |
| 5  | Which shipping method incurred the most cost? |

---

## 📌 Case Scenario II – Questions Answered

| Q# | Question |
|----|----------|
| 6  | Who are the most valuable customers, and what do they buy? |
| 7  | Which small business customer had the highest sales? |
| 8  | Which corporate customer placed the most orders (2009–2012)? |
| 9  | Which consumer customer was the most profitable one? |
| 10 | Which customers returned items and their segments? |
| 11 | Did shipping method match order priority (cost vs speed)? |

---

## 🗂️ Files Included

- `KMS_Case_Study.sql` – All queries grouped by scenario and question
- `Order_Status.csv` – File imported for return tracking
- `KMS_Sql_Case_Study.csv` – Main dataset (2009–2012)

---[Uploadingselect top (1) product_category, 
sum(order_quantity) as Total_orders from dbo.kms_orders group by product_category order by Total_orders desc; Question1.sql…]()



## 📈 Sample Query

```sql
-- Q1: Product category with highest sales
SELECT [Product Category], SUM(Sales) AS Total_Sales
FROM kms_orders
GROUP BY [Product Category]
ORDER BY Total_Sales DESC;
T-- Top 3 and bottom 3 regions in terms of sales
-- Top 3
SELECT TOP (3) 
	Region,
	sum([Sales]) as Total_Sales
FROM [kms_project].[dbo].[kms_orders]
  	  group by region order by Total_Sales desc;
-- Bottom 3
SELECT top (3) 
	Region,
	sum([Sales]) as Total_Sales
FROM [kms_project].[dbo].[kms_orders]
  	  group by region order by Total_Sales asc;

[Uploading --Total sales of appliances in Ontario
select Region, SUM(sales) as Total_Sales from kms_orders where region = 'Ontario' and product_sub_category = 'Appliances' group by region;
Question3.sql…]()
--Bottom 10 Customers based on revenue
SELECT top (10) 
	Customer_Name,
	sum([Sales]) as RevenueFromCustomer
FROM [kms_project].[dbo].[kms_orders]
  	  group by Customer_Name order by RevenueFromCustomer asc;

[Uplo-- Shipping Method with most shipping cost
select top(1) 
	ship_mode, 
	sum(shipping_cost) AS ShippingCost 
from kms_orders 
group by ship_mode 
order by ShippingCost desc;ading Question5.sql…]()
--Bottom 10 Customers based on revenue
SELECT 
	Customer_Name,
	customer_segment,
	sum([Profit]) as RevenueFromCustomer
FROM [kms_project].[dbo].[kms_orders]
  	  group by Customer_Name, customer_segment order by RevenueFromCustomer desc;[Uplo
-- small business customer with the highest sales
select top(1) 
	customer_segment,
	customer_name, 
	sum(sales) AS Total_Sales 
from kms_orders 
where customer_segment = 'Small Business'
	group by customer_segment, customer_name 
	order by Total_Sales desc;ading Question7.sql…]()
[Upload-- corporate customer with most orders in 2009-2012

select top(1) 
	customer_segment,
	customer_name, 
	sum(order_quantity) AS Total_Orders
from kms_orders 
where customer_segment = 'Corporate' AND Order_Date between '2009-01-01' and '2012-12-31'
	group by customer_segment, customer_name 
	order by Total_Orders desc;

ing Question8.sql…]()


[Uplo-- Most profitable consumer customer

select top(1) 
	customer_segment,
	customer_name, 
	sum(profit) AS Total_Profit
from kms_orders 
where customer_segment = 'Consumer'
	group by customer_segment, customer_name 
	order by Total_Profit desc;

ading Question9.sql…]()

[UploadiSELECT 
    ko.Customer_Name, 
    ko.Customer_Segment, 
    COUNT(*) AS number_returned
FROM 
    kms_orders ko
INNER JOIN 
    order_status os ON ko.Order_ID = os.Order_ID
GROUP BY 
    ko.Customer_Name, ko.Customer_Segment
ORDER BY 
    number_returned DESC;ng Question10.sql…]()
### ❓ Q11: Did the company appropriately align shipping methods with order priorities?

**Answer:**

Based on the data, the company has **not appropriately aligned shipping methods with order priorities**.

- 🚚 **Delivery Truck**, while being the **most expensive and slowest** option, is used **extensively for Low and Medium priority orders**.
- ✈️ **Express Air** — the **fastest and cheapest** method — is **underutilized for Critical orders**.

🔍 A more efficient approach would be to:
- Use **fast shipping methods like Express Air** for **high-priority orders**
- Reserve **economical options like Delivery Truck** for **low-priority shipments**

This change would help optimize both **cost** and **service level**, improving logistics and customer satisfaction.



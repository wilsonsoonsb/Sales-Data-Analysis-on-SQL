I. **Introduction**: 

Cars R Us is a wholesale distributor of diecast cars which operates globally in over 15 countries. The company has approached us in hopes of uncovering key critical insights into their business and operations, and identifying areas of improvement. 
This will be done so by analysing data and extracting data from their sales records database, which will uncover KPIs and help facilitate informed data-driven decisions in potential future expansion

II. **Key points:**

To answer our client queries, we will analyse and extract data from the provided sales records database. Doing so will uncover KPIs and help facilitate informed data-driven decisions in future expansion discussions. In order to achieve this goal, this project will focus on the following questions that will provide actionable insights in regards to their operation:
1.  **What are the top 10 highly demanded products and its availability?**

2. **How should we adapt marketing and communication strategies to customers?**

3. **How much should be spent on acquiring new customers?**

III. **Dataset:**

To start off, the database schema which we will be working with consists of eight tables :

- Customers: customer data
- Employees: employee information
- Offices: sales office information
- Orders: customers' sales orders
- OrderDetails: information for each sales order
- Payments: customers' payment records
- Products: List of scale model cars
- ProductLines: Categories of scale model cars

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/12f8528b-8e07-495c-b4d3-0a2f2b5d9dbf/7c72c2d9-30a8-4954-aca0-0e26574a9a6f/image.png)

**Question 1.** 
**Which Products Should We Order More of or Less of? (Determining the top 10 highly demanded products and its availability)**

The question pertains to inventory reports, specifically focusing on two aspects: identifying low stock items (i.e., products in demand) and analyzing product performance. By addressing these areas, the aim is to enhance supply optimization and improve user experience by preventing popular products from running out of stock. Priority for restocking is then given to products that fulfill two criterias: 1.high product performance and 2. lowstock. This approach ensures that the most successful and sought-after products are replenished promptly, aligning with the goal of maintaining adequate inventory levels and meeting customer demands.

-- low stock / high-demand products
WITH
lowStock AS (
  SELECT P.productCode,
         P.productName,
         P.productLine,
ROUND( SUM(O.quantityOrdered *1.0)/P.quantityInStock , 2) AS low_Stock
    FROM products AS P
    JOIN orderdetails AS O
      ON P.productCode = O.productCode
GROUP BY P.productCode
ORDER BY low_Stock DESC
LIMIT 10
),

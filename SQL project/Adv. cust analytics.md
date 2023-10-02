
1. **Which locations in New York received at least 3 orders in January, and how many orders did they each receive?**

   ```sql
   SELECT location, COUNT(orderID) AS NumberOfOrders
   FROM BIT_DB.JanSales
   WHERE location LIKE '%, New York, NY%'
   GROUP BY location
   HAVING COUNT(orderID) >= 3;
   ```

| Location                               | Number of Orders |
|-------------------------------------------|------------------|
| 148 Elm St, New York City, NY 10001    | 3                |
| 515 Lincoln St, New York City, NY 10001| 3                |
| 916 Pine St, New York City, NY 10001   | 3                |
| 961 Jefferson St, New York City, NY 10001 | 4                |


2. **How many of each type of headphone were sold in February?**

   ```sql
   SELECT Product, SUM(Quantity) AS TotalQuantity
   FROM BIT_DB.FebSales
   WHERE Product LIKE '%Headphones%'
   GROUP BY Product;
   ```

| Product                 | Total Quantity |
| -------------------------- | -------------- |
| Wired Headphones        | 50             |
| Bose SoundSport Headphones | 30             |

3. **What was the average amount spent per account in February?**

   ```sql
   SELECT SUM(f.Quantity * f.price) / COUNT(DISTINCT c.acctnum) AS AverageAmountSpentPerAccount
   FROM BIT_DB.FebSales AS f
   JOIN BIT_DB.customers AS c ON f.orderID = c.order_id;
   ```

| Average Amount Spent Per Account |
| -------------------------------- |
| 150.75                           |

4. **What was the average quantity of products purchased per account in February?**

   ```sql
   SELECT SUM(f.Quantity) / COUNT(DISTINCT c.acctnum) AS AverageQuantityPerAccount
   FROM BIT_DB.FebSales AS f
   JOIN BIT_DB.customers AS c ON f.orderID = c.order_id;
   ```

| Average Quantity Per Account |
| ---------------------------- |
| 2.5                          |

5. **Which product brought in the most revenue in January and how much revenue did it bring in total?**

   ```sql
   SELECT Product, MAX(TotalRevenue) AS MaxRevenue
   FROM (
     SELECT Product, SUM(Quantity * price) AS TotalRevenue
     FROM BIT_DB.JanSales
     GROUP BY Product
   );
   ```

| Product | Max Revenue |
| ------- | ----------- |
| iPhone  | 265300      |


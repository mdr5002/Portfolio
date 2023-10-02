### 1. How many units sold?

```sql
SELECT SUM(Quantity) AS TotalUnitsSold
FROM BIT_DB.JanSales;
```


| &nbsp;Total Units Sold in January&nbsp; |
|:----------------------------------------|
|             10,868                      |  


### 2. How many Iphone sales?

```sql 
SELECT SUM(Quantity) AS iPhoneSales
FROM BIT_DB.JanSales
WHERE Product = 'iPhone';
```

| iPhone Sales in January |
|------------------------|
| 379                    |

### 3. Select the customer account numbers for all the orders that were placed in February. 

```sql
SELECT c.acctnum
FROM BIT_DB.customers AS c
JOIN BIT_DB.FebSales AS f ON c.order_id = f.orderID;
```

| Customer Account Numbers |
|-------------------------|
| 78848136                |
| 78848136                |
| 78848136                |
| 78848136                |
| 78848136                |
| 78848136                |

### 4. Which product was the cheapest one sold in January, and what was the price? 

```sql 
SELECT Product, MIN(price) AS CheapestPrice
FROM BIT_DB.JanSales;
```

| Product               | Cheapest Price |
|-----------------------|----------------|
| AAA Batteries (4-pack) | 2.99           |


### 5. What is the total revenue for each product sold in January? (Revenue can be calculated using the number of products sold and the price of the products). 

```sql
SELECT Product, SUM(Quantity * price) AS TotalRevenue
FROM BIT_DB.JanSales
GROUP BY Product;
```

| Product                   | Total Revenue        |
|---------------------------|----------------------|
| 20in Monitor              | 23647.85             |
| 27in 4K Gaming Monitor    | 121676.88            |
| 27in FHD Monitor          | 62845.81             |
| 34in Ultrawide Monitor    | 119316.86            |
| AA Batteries (4-pack)     | 5472.00              |
| AAA Batteries (4-pack)    | 4772.04              |
| Apple Airpods Headphones  | 122100               |
| Bose SoundSport Headphones| 65893.41             |
| Flatscreen TV             | 72900                |
| Google Phone              | 190800               |
| LG Dryer                  | 23400                |
| LG Washing Machine        | 25200                |
| Lightning Charging Cable  | 17207.45             |
| Macbook Pro Laptop        | 399500               |
| Product                   | 0                    |
| ThinkPad Laptop           | 216997.83            |
| USB-C Charging Cable      | 15343.80             |
| Vareebadd Phone           | 50000                |
| Wired Headphones          | 12961.19             |
| iPhone                    | 265300               |


### 6. Which products were sold in February at 548 Lincoln St, Seattle, WA 98101, how many of each were sold, and what was the total revenue? 

```sql
SELECT Product, SUM(Quantity) AS TotalQuantity, SUM(Quantity * price) AS TotalRevenue
FROM BIT_DB.FebSales
WHERE location = '548 Lincoln St, Seattle, WA 98101'
GROUP BY Product;
```

| Product               | Total Quantity | Total Revenue |
|-----------------------|----------------|---------------|
| AA Batteries (4-pack) | 2              | 7.68          |


### 7. How many customers ordered more than 2 products at a time in February, and what was the average amount spent for those customers?

```sql
SELECT COUNT(DISTINCT orderID) AS NumberOfCustomers, AVG(Quantity * price) AS AverageAmountSpent
FROM BIT_DB.FebSales
WHERE Quantity > 2;
```

| Number of Customers | Average Amount Spent |
|---------------------|----------------------|
| 265                 | 11.57                |













### 1. Show Customers (their full names, customer ID, and country) who are not in the US

#### Query

```sql
SELECT CustomerId, FirstName || ' ' || LastName AS FullName, Country
FROM Customers
WHERE Country != 'USA';
```
#### Sample Output

| CustomerId | FullName              | Country        |
|------------|-----------------------|----------------|
| 1          | Luís Gonçalves        | Brazil         |
| 2          | Leonie Köhler         | Germany        |
| 3          | François Tremblay     | Canada         |
| 4          | Bjørn Hansen          | Norway         |
| 5          | František Wichterlová | Czech Republic |

---

### 2. Show only the Customers from Brazil

#### Query

```sql
SELECT CustomerId, FirstName || ' ' || LastName AS FullName, Country
FROM Customers
WHERE Country = 'Brazil';
```
#### Sample Output

| CustomerId | FullName         | Country |
|------------|------------------|---------|
| 1          | Luís Gonçalves   | Brazil  |
| 10         | Eduardo Martins  | Brazil  |
| 11         | Alexandre Rocha  | Brazil  |
| 12         | Roberto Almeida  | Brazil  |
| 13         | Fernanda Ramos   | Brazil  |

---

### 3. Find the Invoices of customers who are from Brazil. The resulting table should show the customer's full name, Invoice ID, Date of the invoice, and billing country

#### Query

```sql
SELECT c.FirstName || ' ' || c.LastName AS FullName, i.InvoiceId, i.InvoiceDate, i.BillingCountry
FROM Invoices i
JOIN Customers c ON i.CustomerId = c.CustomerId
WHERE c.Country = 'Brazil';
```
#### Sample Output

| FullName        | InvoiceId | InvoiceDate          | BillingCountry |
|-----------------|-----------|----------------------|----------------|
| Luís Gonçalves  | 98        | 2010-03-11 00:00:00  | Brazil         |
| Luís Gonçalves  | 121       | 2010-06-13 00:00:00  | Brazil         |
| Luís Gonçalves  | 143       | 2010-09-15 00:00:00  | Brazil         |
| Luís Gonçalves  | 195       | 2011-05-06 00:00:00  | Brazil         |
| Luís Gonçalves  | 316       | 2012-10-27 00:00:00  | Brazil         |

---

### 4. Show the Employees who are Sales Agents

#### Query

```sql
SELECT EmployeeId, FirstName || ' ' || LastName AS FullName, Title
FROM Employees
WHERE Title = 'Sales Support Agent';
```
#### Sample Output

| EmployeeId | FullName       | Title             |
|------------|----------------|-------------------|
| 3          | Jane Peacock   | Sales Support Agent |
| 4          | Margaret Park  | Sales Support Agent |
| 5          | Steve Johnson  | Sales Support Agent |

---

### 5. Find a unique/distinct list of billing countries from the Invoice table

#### Query

```sql
SELECT DISTINCT BillingCountry
FROM Invoices;
```
#### Sample Output

| BillingCountry |
|----------------|
| Germany        |
| Norway         |
| Belgium        |
| Canada         |
| USA            |

---

### 6. Provide a query that shows the invoices associated with each sales agent. The resulting table should include the Sales Agent's full name

#### Query

```sql
SELECT e.FirstName || ' ' || e.LastName AS SalesAgent, i.InvoiceId
FROM Invoices i
JOIN Customers c ON i.CustomerId = c.CustomerId
JOIN Employees e ON c.SupportRepId = e.EmployeeId;
```

#### Sample Output

| SalesAgent   | InvoiceId |
|--------------|-----------|
| Jane Peacock | 98        |
| Jane Peacock | 121       |
| Jane Peacock | 143       |
| Jane Peacock | 195       |
| Jane Peacock | 316       |

---
### 7. Show the Invoice Total, Customer name, Country, and Sales Agent name for all invoices and customers

#### Query

```sql
SELECT i.Total AS InvoiceTotal, c.FirstName || ' ' || c.LastName AS CustomerName, c.Country, e.FirstName || ' ' || e.LastName AS SalesAgent
FROM Invoices i
JOIN Customers c ON i.CustomerId = c.CustomerId
JOIN Employees e ON c.SupportRepId = e.EmployeeId;
```
#### Sample Output

| InvoiceTotal | CustomerName   | Country | SalesAgent  |
|--------------|----------------|---------|-------------|
| 3.98         | Luís Gonçalves | Brazil  | Jane Peacock |
| 3.96         | Luís Gonçalves | Brazil  | Jane Peacock |
| 5.94         | Luís Gonçalves | Brazil  | Jane Peacock |
| 0.99         | Luís Gonçalves | Brazil  | Jane Peacock |
| 1.98         | Luís Gonçalves | Brazil  | Jane Peacock |

---

### 8. How many Invoices were there in 2009?

#### Query

```sql
SELECT COUNT(*) AS InvoiceCount
FROM Invoices
WHERE strftime('%Y', InvoiceDate) = '2009';
```
#### Sample Output

| InvoiceCount |
|--------------|
| 83           |

---

### 9. What are the total sales for 2009?

#### Query

```sql
SELECT SUM(Total) AS TotalSales
FROM Invoices
WHERE strftime('%Y', InvoiceDate) = '2009';
```
#### Sample Output

| TotalSales  |
|-------------|
| 449.46      |

---

### 10. Write a query that includes the purchased track name with each invoice line ID

#### Query

```sql
SELECT il.InvoiceLineId, t.Name AS TrackName
FROM invoice_items il
JOIN tracks t ON il.TrackId = t.TrackId;
```
#### Sample Output

| InvoiceLineId | TrackName                                |
|---------------|------------------------------------------|
| 579           | For Those About To Rock (We Salute You)  |
| 1             | Balls to the Wall                        |
| 1154          | Balls to the Wall                        |
| 1728          | Fast As a Shark                          |
| 2             | Restless and Wild                        |

---
### 11. Write a query that includes the purchased track name AND artist name with each invoice line ID

#### Query

```sql
SELECT il.InvoiceLineId, t.Name AS TrackName, a.Name AS ArtistName
FROM invoice_items il
JOIN tracks t ON il.TrackId = t.TrackId
JOIN albums al ON t.AlbumId = al.AlbumId
JOIN artists a ON al.ArtistId = a.ArtistId;
```
#### Sample Output

| InvoiceLineId | TrackName                                | ArtistName  |
|---------------|------------------------------------------|-------------|
| 579           | For Those About To Rock (We Salute You)  | AC/DC       |
| 1             | Balls to the Wall                        | Accept      |
| 1154          | Balls to the Wall                        | Accept      |
| 1728          | Fast As a Shark                          | Accept      |
| 2             | Restless and Wild                        | Accept      |

---

### 12. Provide a query that shows all the Tracks, and include the Album name, Media type, and Genre

#### Query

```sql
SELECT t.Name AS TrackName, al.Title AS AlbumName, mt.Name AS MediaType, g.Name AS Genre
FROM tracks t
JOIN albums al ON t.AlbumId = al.AlbumId
JOIN media_types mt ON t.MediaTypeId = mt.MediaTypeId
JOIN genres g ON t.GenreId = g.GenreId;
```
#### Sample Output

| TrackName                               | AlbumName                             | MediaType               | Genre  |
|-----------------------------------------|---------------------------------------|-------------------------|--------|
| For Those About To Rock (We Salute You) | For Those About To Rock We Salute You | MPEG audio file         | Rock   |
| Balls to the Wall                       | Balls to the Wall                     | Protected AAC audio file| Rock   |
| Fast As a Shark                         | Restless and Wild                     | Protected AAC audio file| Rock   |
| Restless and Wild                       | Restless and Wild                     | Protected AAC audio file| Rock   |
| Princess of the Dawn                    | Restless and Wild                     | Protected AAC audio file| Rock   |

---

### 13. Show the total sales made by each sales agent

#### Query

```sql
SELECT e.FirstName || ' ' || e.LastName AS SalesAgent, SUM(i.Total) AS TotalSales
FROM invoices i
JOIN customers c ON i.CustomerId = c.CustomerId
JOIN employees e ON c.SupportRepId = e.EmployeeId
GROUP BY e.EmployeeId;
```
#### Sample Output

| SalesAgent    | TotalSales  |
|---------------|-------------|
| Jane Peacock  | 833.04      |
| Margaret Park | 775.40      |
| Steve Johnson | 720.16      |

---

### 14. Which sales agent made the most dollars in sales in 2009?

#### Query

```sql
SELECT e.FirstName || ' ' || e.LastName AS SalesAgent, SUM(i.Total) AS TotalSales
FROM invoices i
JOIN customers c ON i.CustomerId = c.CustomerId
JOIN employees e ON c.SupportRepId = e.EmployeeId
WHERE strftime('%Y', i.InvoiceDate) = '2009'
GROUP BY e.EmployeeId
ORDER BY TotalSales DESC
LIMIT 1;
```
#### Sample Output

| SalesAgent   | TotalSales  |
|--------------|-------------|
| Steve Johnson| 164.34      |

---


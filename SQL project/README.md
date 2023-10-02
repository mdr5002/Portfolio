# SQL Learning Project

## Overview

This repository contains a collection of SQL exercises aimed at learning and familiarizing myself with SQL queries and database operations. The project consists of SQL queries designed to solve specific problems, accompanied by their expected outputs.

## Structure

The project is organized into sections, each detailing a specific SQL query problem. For each section, you will find:

- The SQL query question
- The actual SQL query code
- Sample output of the SQL query

## What You Will Learn

- SQL SELECT statements
- JOIN operations
- Aggregation functions
- Filtering and sorting
- And much more

## Prerequisites

- Basic understanding of SQL
- A SQL database to run the queries (examples were run on SQLite)

## Sample Query

```sql
SELECT CustomerId, FirstName || ' ' || LastName AS FullName, Country
FROM Customers
WHERE Country != 'USA';


CustomerId	FullName	Country
1	Luís Gonçalves	Brazil
2	Leonie Köhler	Germany


```

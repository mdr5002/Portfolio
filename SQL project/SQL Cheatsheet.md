
1. **SELECT statement:** 
   - To retrieve all data from a table:
   
   ```sql
   SELECT * FROM netflix_titles_info LIMIT 5;
   ```
   
| show_id | type    | title                 | country       | date_added              | release_year | rating | duration  | listed_in                                                                       |
|---------|---------|-----------------------|---------------|-------------------------|--------------|--------|-----------|---------------------------------------------------------------------------------|
| s1      | Movie   | Dick Johnson Is Dead  | United States | 2021-09-25 00:00:00     | 2020         | PG-13  | 90 min    | Documentaries                                                                   |
| s2      | TV Show | Blood & Water         | South Africa  | 2021-09-24 00:00:00     | 2021         | TV-MA  | 2 Seasons | International TV Shows, TV Dramas, TV Mysteries                                 |
| s3      | TV Show | Ganglands             | NULL          | 2021-09-24 00:00:00     | 2021         | TV-MA  | 1 Season  | Crime TV Shows, International TV Shows, TV Action & Adventure                   |
| s4      | TV Show | Jailbirds New Orleans | NULL          | 2021-09-24 00:00:00     | 2021         | TV-MA  | 1 Season  | Docuseries, Reality TV                                                          |
| s5      | TV Show | Kota Factory          | India         | 2021-09-24 00:00:00     | 2021         | TV-MA  | 2 Seasons | International TV Shows, Romantic TV Shows, TV Comedies                          |
   
##### To retrieve specific columns from a table:
   
   ```sql
   SELECT show_id, title, release_year FROM netflix_titles_info LIMIT 5;
   ```

   | show_id | title                 | release_year |
   |---------|-----------------------|--------------|
   | s1      | Dick Johnson Is Dead  | 2020         |
   | s2      | Blood & Water         | 2021         |
   | s3      | Ganglands             | 2021         |
   | s4      | Jailbirds New Orleans | 2021         |
   | s5      | Kota Factory          | 2021         |
   

2. **WHERE clause:**
   - To filter the data based on certain conditions:
   
   ```sql
   SELECT * FROM netflix_titles_info WHERE rating='PG-13';
   ```

  | show_id | type  | title                | country       | date_added              | release_year | rating | duration | listed_in          |
  |---------|-------|----------------------|---------------|-------------------------|--------------|--------|----------|--------------------|
  | s1      | Movie | Dick Johnson Is Dead | United States | 2021-09-25 00:00:00     | 2020         | PG-13  | 90 min   | Documentaries      |
  | s10     | Movie | The Starling         | United States | 2021-09-24 00:00:00     | 2021         | PG-13  | 104 min  | Comedies, Dramas   |
   
1. **ORDER BY clause:**
   - To sort the data:
   
   ```sql
   SELECT * FROM netflix_titles_info ORDER BY release_year DESC LIMIT 5;
   ```

  | show_id | type    | title               | country  | date_added              | release_year | rating | duration  | listed_in                                     |
  |---------|---------|---------------------|----------|-------------------------|--------------|--------|-----------|-----------------------------------------------|
  | s2      | TV Show | Blood & Water       | South Africa | 2021-09-24 00:00:00     | 2021         | TV-MA  | 2 Seasons | International TV Shows, TV Dramas, TV Mysteries |
  | s3      | TV Show | Ganglands           | NULL     | 2021-09-24 00:00:00     | 2021         | TV-MA  | 1 Season  | Crime TV Shows, International TV Shows, TV Action & Adventure |
  | s4      | TV Show | Jailbirds New Orleans | NULL     | 2021-09-24 00:00:00     | 2021         | TV-MA  | 1 Season  | Docuseries, Reality TV |
  | s5      | TV Show | Kota Factory        | India    | 2021-09-24 00:00:00     | 2021         | TV-MA  | 2 Seasons | International TV Shows, Romantic TV Shows, TV Comedies |
  | s6      | TV Show | Midnight Mass       | NULL     | 2021-09-24 00:00:00     | 2021         | TV-MA  | 1 Season  | TV Dramas, TV Horror, TV Mysteries |

4. **COUNT function:**
   - To count the number of rows:
   
   ```sql
   SELECT COUNT(*) FROM netflix_titles_info;
   ```

| count |
|--------|
|  20     |


5. **GROUP BY clause:**
   - To group the data based on certain columns:
   
   ```sql
   SELECT type, COUNT(*) FROM netflix_titles_info GROUP BY type;
   ```

| type    | count |
|---------|-------|
| Movie   | 7     |
| TV Show | 13    |
 
6. **JOIN clause:**
   - To combine rows from two or more tables based on a related column:
   
   ```sql
   SELECT nti.show_id, nti.title, np.director 
   FROM netflix_titles_info nti 
   JOIN netflix_people np ON nti.show_id = np.show_id LIMIT 5;
   ```

| show_id | title                | director        |
|---------|----------------------|-----------------|
| s1      | Dick Johnson Is Dead | Kirsten Johnson |
| s2      | Blood & Water        | NULL            |
| s3      | Ganglands            | Julien Leclercq |
| s5      | Kota Factory         | NULL            |
| s6      | Midnight Mass        | Mike Flanagan   |

   

For the `INSERT`, `UPDATE`, and `DELETE` operations, they don't return data, but you would see a confirmation message indicating the number of rows affected. You could use a `SELECT` statement to verify the changes.


7. **INSERT statement:**
   - To insert new rows into a table:

   ```sql
   INSERT INTO netflix_titles_info(show_id, type, title) VALUES ('s21', 'Movie', 'New Movie');
   ```
   
   This operation won't return data, but if we subsequently run the following SELECT statement:

   ```sql
   SELECT * FROM netflix_titles_info WHERE show_id='s21';
   ```

   The output would be:

| show_id | type  | title     | country | date_added | release_year | rating | duration | listed_in |
|---------|-------|-----------|---------|------------|--------------|--------|----------|-----------|
| s21     | Movie | New Movie | NULL    | NULL       | NULL         | NULL   | NULL     | NULL      |


8. **UPDATE statement:**
   - To modify existing rows in a table:

   ```sql
   UPDATE netflix_titles_info SET rating='PG' WHERE show_id='s21';
   ```

   This operation also won't return data, but if we subsequently run the following SELECT statement:

   ```sql
   SELECT * FROM netflix_titles_info WHERE show_id='s21';
   ```

   The output would be:

| show_id | type  | title     | country | date_added | release_year | rating | duration | listed_in |
|---------|-------|-----------|---------|------------|--------------|--------|----------|-----------|
| s21     | Movie | New Movie | NULL    | NULL       | NULL         | PG     | NULL     | NULL      |


9. **DELETE statement:**
   - To delete rows from a table:

   ```sql
   DELETE FROM netflix_titles_info WHERE show_id='s21';
   ```

   This operation doesn't return data either, but if we subsequently run the following SELECT statement:

   ```sql
   SELECT * FROM netflix_titles_info WHERE show_id='s21';
   ```

   The output would be an empty table because the row with `show_id` 's21' has been deleted.

10. **LIKE operator:**
    - To search for a specified pattern in a column:

    ```sql
    SELECT * FROM netflix_titles_info WHERE title LIKE '%Dead%' LIMIT 5;
    ```

    The output would be:

| show_id | type    | title                 | country       | date_added              | release_year | rating | duration  | listed_in                                                                   |
|---------|---------|-----------------------|---------------|-------------------------|--------------|--------|-----------|----------------------------------------------------------------------------|
| s1      | Movie   | Dick Johnson Is Dead  | United States | 2021-09-25 00:00:00     | 2020         | PG-13  | 90 min    | Documentaries                                                               |
| s16     | TV Show | Dear White People     | United States | 2021-09-22 00:00:00     | 2021         | TV-MA  | 4 Seasons | TV Comedies, TV Dramas                                                      |


11. **DISTINCT operator:**
    - To remove duplicate values in the result set:

    ```sql
    SELECT DISTINCT rating FROM netflix_titles_info;
    ```

    The output would be:

| rating |
|--------|
| PG-13  |
| TV-MA  |
| PG     |
| TV-14  |
| TV-PG  |

12. **LIMIT clause:**
    - To specify the number of records to return from the top:

    ```sql
    SELECT * FROM netflix_titles_info LIMIT 5;
    ```

    The output would be:

| show_id | type    | title                 | country       | date_added              | release_year | rating | duration  | listed_in                                                                       |
|---------|---------|-----------------------|---------------|-------------------------|--------------|--------|-----------|---------------------------------------------------------------------------------|
| s1      | Movie   | Dick Johnson Is Dead  | United States | 2021-09-25 00:00:00     | 2020         | PG-13  | 90 min    | Documentaries                                                                   |
| s2      | TV Show | Blood & Water         | South Africa  | 2021-09-24 00:00:00     | 2021         | TV-MA  | 2 Seasons | International TV Shows, TV Dramas, TV Mysteries                                 |
| s3      | TV Show | Ganglands             | NULL          | 2021-09-24 00:00:00     | 2021         | TV-MA  | 1 Season  | Crime TV Shows, International TV Shows, TV Action & Adventure                  |
| s4      | TV Show | Jailbirds New Orleans | NULL          | 2021-09-24 00:00:00     | 2021         | TV-MA  | 1 Season  | Docuseries, Reality TV                                                          |
| s5      | TV Show | Kota Factory          | India         | 2021-09-24 00:00:00     | 2021         | TV-MA  | 2 Seasons | International TV Shows, Romantic TV Shows, TV Comedies                          |


13. **MIN and MAX functions:**
    - To find the smallest and largest value of the selected column:

    ```sql
    SELECT MIN(release_year), MAX(release_year) FROM netflix_titles_info;
    ```

    The output would be:

| min  | max  |
|------|------|
| 1993 | 2021 |


14. **AVG, SUM functions:**
    - To find the average and total sum of the numeric column (let's assume there's a 'views' column):

    ```sql
    SELECT AVG(views), SUM(views) FROM netflix_titles_info;
    ```

    The output would be:

| avg  | sum   |
|------|-------|
| 1000 | 20000 |


15. **BETWEEN operator:**
    - To filter the result set within a certain range:

    ```sql
    SELECT * FROM netflix_titles_info WHERE release_year BETWEEN 2000 AND 2020;
    ```

    The output would be a table with rows where the 'release_year' is between 2000 and 2020.


16. **IN operator:**
    - To specify multiple possible values for a column:

    ```sql
    SELECT * FROM netflix_titles_info WHERE rating IN ('PG-13', 'PG');
    ```

    The output would be a table with rows where the 'rating' is either 'PG-13' or 'PG'.


17. **AS keyword:**
    - To rename a column or table:

    ```sql
    SELECT title AS Name, release_year AS 'Release Year' FROM netflix_titles_info LIMIT 5;
    ```

    The output would be:

| Name                 | Release Year |
|----------------------|--------------|
| Dick Johnson Is Dead | 2020         |
| Blood & Water        | 2021         |
| Ganglands            | 2021         |
| Jailbirds New Orleans | 2021         |
| Kota Factory         | 2021         |


18. **NULL values:**
    - To select rows where there are null (or not null) values in the columns:

    ```sql
    SELECT * FROM netflix_titles_info WHERE country IS NULL;
    ```

    The output would be a table with rows where the 'country' is null.
```sql
SELECT SUM(Quantity) AS TotalUnitsSold
FROM BIT_DB.JanSales;
```



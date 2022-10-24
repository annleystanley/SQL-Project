*What are your risk areas? Identify and describe them.*

My main risk area is my lack of experience, both with data, and ecommerce as a whole. 
I am working to further my knowledge of SQL, but at the moment, may not notice where code doesn't make sense and may therefore giving incorrect information.

Finding meaningful relationships between data, without familiarity of the data, or the industry it's from, can be difficult. It is also difficult being sure of where typos, etc.




# QA Process:
*Describe your QA process and include the SQL queries used to execute it.*

*Did not include coding examples as these were repeated many times throughout the process*

-   Counted new rows after every join
-   Counted rows after making new tables
-	Tested code in isolated segments before adding them to a larger query
-   Discussed issues with classmates within the cohort to make sure my reasonings made sense
-   Had look over my all code, as well as the rest of my assignment, for readability issues


*SQL Queries:*
### Finding the Central Tendancies For Main Tables

#### Products Table

```sql
-- Central Tendency Values for products table

-- mean restock time = 12
SELECT
	CAST(AVG(restockingleadtime) as int) AS mean_restock_time
FROM products


-- median restock time = 12
SELECT
	restockingleadtime AS median_restock_time
FROM 
	products
ORDER BY 
	restockingleadtime
LIMIT 1
-- Using an offset to find the middle point of the table
OFFSET
	((SELECT
	COUNT (*)
	FROM products)/2)


--mode restock time = 14 (occurs 86 time)
-- looks like restock times over 18 are rare
SELECT
	restockingleadtime,
	COUNT (*)
FROM 
	products
GROUP BY
	restockingleadtime
ORDER BY 
	COUNT(*) DESC


-- counting total that seem to be outliers = 79
-- comfortable excluding these 79/1092
SELECT
	COUNT (*)
FROM 
	products
WHERE restockingleadtime >=19
ORDER BY 
	COUNT(*) DESC
```

### Al_Sessions Table

```SQL
-- Central Tendency Values for cleaned_all_sessions table
-- mean price = 33

SELECT
	CAST(AVG(productprice) as int) AS mean_price
FROM cleaned_all_sessions
WHERE productprice !=0


-- median price = 18.99

SELECT
	productprice AS median_price
FROM 
	cleaned_all_sessions
WHERE productprice !=0
ORDER BY 
	productprice
LIMIT 1
-- Using an offset to find the middle point of the table
OFFSET
	((SELECT
	COUNT (*)
	FROM cleaned_all_sessions)/2)


--mode price - 16.99, OCURRING 778 TIMES
SELECT
	productprice,
	COUNT (*)
FROM 
	cleaned_all_sessions
WHERE productprice !=0
GROUP BY
	productprice
ORDER BY 
	COUNT(*) DESC
LIMIT 1

```


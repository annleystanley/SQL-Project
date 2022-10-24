Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


*SQL Queries:*

```sql
SELECT
-- rank of transaction amounts
	DENSE_RANK() OVER (
		ORDER BY SUM(clean.totaltransactionrevenue) desc
	),
	loc.country,
	loc.city,
	SUM(clean.totaltransactionrevenue) AS total_transaction_amount
FROM
	cleaned_all_sessions clean
INNER JOIN
		cleaned_location loc USING (primary_key)
GROUP BY 
	loc.country,
	loc.city
LIMIT 10;
```


*Answer:*

The United States, specifically the city of San Francisco have the highest level of transaction revenues. 


Top 10 Shown Below

![image](./images/q1%20table.png)



**Question 2: What is the average number of products ordered from visitors in each city and country?**


*SQL Queries:*
```sql
SELECT
	country,
	city,
	ROUND(AVG(quantity_ordered),0) AS average_ordered
FROM clean_data
GROUP BY
	city,
	country
ORDER BY
	average_ordered DESC,
	country,
	city
```


*Answer:*

Visitors from Tel-Aviv, Isreal, order more on average, than users from other cities.

![image](./images/q2%20table.png)




**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


**SQL Queries:**
```sql
SELECT
	loc.country,
	loc.city,
	clean.primarycat,
	COUNT(clean.primarycat) as cat_count
-- selecting only where transactions have been made
FROM 
	(SELECT *
	FROM clean_data
	WHERE totaltransactionrevenue !=0) AS clean
JOIN cleaned_location loc USING (primary_key)
WHERE quantity_ordered >0
AND clean.primarycat NOT LIKE '%${escCatTitle}%'
AND clean.primarycat NOT LIKE '%not%'
GROUP BY
	clean.primarycat,
	loc.city,
	loc.country
ORDER BY
	cat_count DESC,
	loc.city
```


*Answer:*

Cannot descern any specific pattern for the kinds of products ordered from different cities.


![image](./images/q3%20table.png)





**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


*SQL Queries:*
```sql
SELECT
-- Ranking based by the total revenue per product
	DENSE_RANK() OVER(
	ORDER BY
	SUM(als.totaltransactionrevenue) DESC),
	loc.country,
	loc.city,
	cd.productname,
	ROUND(SUM(als.totaltransactionrevenue),2) AS  totalrevenue
FROM
-- Specifically choosing from data where a transaction has been made
	(
	SELECT *
	FROM cleaned_all_sessions
	WHERE totaltransactionrevenue >0
	) AS als
JOIN cleaned_all_sessions cd USING (primary_key)
JOIN cleaned_location loc USING (primary_key)
GROUP BY
	als.totaltransactionrevenue,
	cd.productname,
	loc.country,
	loc.city
ORDER BY als.totaltransactionrevenue DESC
```



*Answer:*

The top selling item of all time is a reusable shopping back. This may seem odd in comparison to other kinds of items, but since it's a cheap item, many people can and will buy it in bulk.

Other popular items appear to be Nest security items, which also makes sense since these are in heavily populated cities with higher crime rates.


![image](./images/q4%20table.png)





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

*SQL Queries:*
```sql
-- showing avg/min/max rev per city
SELECT 
	loc.country,
	loc.city,
	ROUND(AVG(al.totaltransactionrevenue),2) as avg_revenue,
	ROUND(MIN(al.totaltransactionrevenue),2) as min_revenue,
	ROUND(MAX(al.totaltransactionrevenue),2) as max_revenue
FROM cleaned_location loc
JOIN cleaned_all_sessions al USING (primary_key)
WHERE al.totaltransactionrevenue >0
GROUP BY
	loc.country,
	loc.city
ORDER BY max_revenue DESC
```

```sql
-- showing avg/min/max rev per country only
SELECT 
	loc.country,
	ROUND(AVG(al.totaltransactionrevenue),2) as avg_revenue,
	ROUND(MIN(al.totaltransactionrevenue),2) as min_revenue,
	ROUND(MAX(al.totaltransactionrevenue),2) as max_revenue
FROM cleaned_all_sessions al
JOIN cleaned_location loc USING (primary_key)
WHERE al.totaltransactionrevenue >0
GROUP BY
	loc.country
ORDER BY max_revenue DESC
```

*Answer:*

On average, most american cities tend to bring in a similar amount of revenues, however Atlanta, in the United States, overall, brings in the most overall revenue.

Overall, the United States has the highest amount of revenue, but this data is also biased towards the United States, with the majority of purchasing customers being from there.

We can assume that this is an American store, which may lead to these results.

### Sorted by Country & City ###
![image](./images/q5%20table%20countrycity.png)

### Sorted by City Only ###
![image](./images/q5%20table%20country%20only.png)








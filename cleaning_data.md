
# Cleaning Data

## Data Cleaning Checklist:

## Remove unwanted/irrelevant observations

- Remove anything that is not related to, or does not fit, the problem


## Ensure accurate data types

- Make sure data types are uniform (e.g. make sure strings are termed as numeric, numeric aren't termed as booleans, etc)


## Address missing values

- Are there so many missing values in this column that the entire column should be deleted?
- Am I able to estimate the missing data by performing linear regression, or replacing with the median value?


## Fix typos

- Check strings specifically for typos, as they rely heavily on spelling and cases





# Queries:
Below, provide the SQL queries you used to clean your data.



```sql
-- Changing all currency codes to USD, since price is on supplier-side and not consumer-side

SELECT
    currencycode,
    CASE
        WHEN currencycode IS NULL then 'USD'
        ELSE currencycode
    END AS corrected_currencycode,
	primary_key
FROM all_sessions


-- changing nulls to 0s, and adjusting prices

SELECT
    CASE
        WHEN totaltransactionrevenue IS NULL then '$0'
        ELSE SUM(totaltransactionrevenue/1000000)
    END AS corrected_totaltransactionrevenue,	
	CASE
        WHEN transactions IS NULL then 0
        ELSE transactions
    END AS corrected_transactions,
	CASE
        WHEN productrefundamount IS NULL then '$0'
        ELSE SUM(productrefundamount/1000000)
    END AS corrected_productrefundamount,
	CASE
        WHEN productquantity IS NULL then 0
        ELSE productquantity
    END AS corrected_productquantity,
	    CASE
        WHEN productprice IS NULL then '$0'
        ELSE SUM(productprice/1000000)
    END AS corrected_productprice,	
    CASE
        WHEN productrevenue IS NULL then '$0'
        ELSE SUM(productrevenue/1000000)
    END AS corrected_productrevenue,
	primary_key
FROM all_sessions
GROUP BY primary_key
ORDER BY productrevenue


-- cleaning out unavailable cities and countries

SELECT
    city cleaned_city,
	country cleaned_country,
	primary_key
FROM all_sessions
WHERE
	city NOT LIKE '%(not set)%'
	AND
	city NOT LIKE '%not available%'
	AND
	country NOT LIKE '%(not set)%'
	AND
	country NOT LIKE '%not available%'
ORDER BY primary_key 




--splitting product category into a more easily organizable format by splitting by '/'

SELECT
	v2productname,
	SPLIT_PART (v2Productcategory,'/',1) primary_category,
	SPLIT_PART (v2Productcategory,'/',2) subcat1,
	SPLIT_PART (v2Productcategory,'/',3) subcat2,
	SPLIT_PART (v2Productcategory,'/',4) subcat3,
	primary_key
FROM all_sessions
GROUP BY
	v2productcategory,
	v2productname,
	primary_key
ORDER BY primary_key*/

SELECT * 
FROM analytics


-- Updating product categories to be cleaner
SELECT 
	PRIMARYCAT, 
	SUBCAT1,
	subcat2,
	subcat3,
	CASE
		WHEN primarycat LIKE '%Nest%'
		THEN 'Electronics'
		WHEN primarycat LIKE '%Shop By Brand%'
		AND subcat2 LIKE '%Android%'
		OR subcat2 LIKE '%Google%'
		OR primarycat LIKE '%Waze%'
		THEN 'Electronics'
		ELSE primarycat
	END as prod_cat1

FROM CLEAN_DATA


UPDATE clean_data
SET primarycat = 'Electronics'
WHERE primarycat LIKE '%Shop By Brand%'
		AND subcat2 LIKE '%Android%'
		OR subcat2 LIKE '%Google%'
		OR primarycat LIKE '%Waze%' */


#### All feedback is welcome! Let me know what functions would be good to add. I plan on improving and expanding this cheat sheet in the future to include more query functions and managing database functions.

## WITH  cte  AS
-- Creates a temporary table in a single query, can be used with a join to the main table. It's common to name the table "cte" but this is only a variable.

```
WITH cte AS
	(SELECT shipment_id,
		SUM(weight) AS total_weight)
	FROM amazon_shipment
	GROUP BY 1)
SELECT amazon_shipment *
	total_weight
FROM amazon_shipment
JOIN cte ON amazon_shipment_id = cte.shipment_id
```

## SELECT
-- Used to select which columns the output will contain.

```
SELECT company, continent
FROM forbes_global_2010_2014
ORDER BY profits DESC
LIMIT 1
```

## AS
-- Allows you to rename the feature in the SELECT statement.

```
SELECT company AS global_company, continent
FROM forbes_global_2010_2014
ORDER BY profits DESC
LIMIT 1
```

## DISTINCT
-- Finds unique entries when used with SELECT statement.
```
SELECT DISTINCT business_name, inspection_date, inspection_score
FROM sf_restaurant_health_violations
WHERE inspection_score < 50
```

## COUNT
-- Counts the number of entries for a given feature, using * returns all records.
```
SELECT DISTINCT variety, COUNT(*)
FROM iris
GROUP BY variety
```

## SUM
-- If a feature is an int or float type, it provides the total.
```
SELECT SUM(salary), department
FROM worker
GROUP BY department
```

## STRPOS 
-- Returns the position of a nested substring.
```
SELECT STRPOS(FIRST_NAME, 'a') as position_of_letter_a
FROM worker
WHERE first_name = 'Amitah'
```

## FROM
-- Establishes which table the data will come from.
```
SELECT company as global_company, continent
FROM forbes_global_2010_2014
ORDER BY profits DESC
LIMIT 1
```

## JOIN
INNER JOIN
-- Combines two tables only if entries from both tables match the criteria. It is acceptable to just write JOIN instead of INNER JOIN.
```
SELECT first_name, worker_title
FROM worker
INNER JOIN title ON worker.worker_id = title.worker_ref_id
WHERE worker_title = 'Manager'
```

LEFT JOIN
-- Combines two tables under conditions like an inner join, but it also holds all records from the first referenced table and only adds items from the second table if the entries meet the conditions. The syntax is the same as Inner Join.

RIGHT JOIN
-- It's the same as left join but reversed.

## WHERE
-- Applies criteria to the search results.
```
SELECT DISTINCT business_name, inspection_date, inspection_score
FROM sf_restaurant_health_violations
WHERE inspection_score < 50
```

## AND
-- Apply multiple conditions to a WHERE statement.
```
SELECT year
FROM uber_advertising
WHERE advertising_channel = 'celebrities' AND customers_acquired > 2000
```

## IN
-- Useful for nested queries where you must get the output of one query and match an id with the main query.
```
SELECT employee. first_name, employee.last_name
FROM employee
	WHERE employee.emp_id IN (
		SELECT works_with.emp_id
		FROM works_with
		WHERE works_with.total_sales > 30000	
		)
```

## GROUP BY
-- Groups the query data by a feature.
```
SELECT SUM(salary), department
FROM worker
GROUP BY department
```

## Dealing with Dates
-- DATE_PART: allows you to pick out the year, month, or day from a datetime variable.
```
SELECT *DATE_PART*('day', post_date::date)
GROUPBY date_part('day', post_date::date)
```

## LIMIT
-- Used to limit the amount of entries in the output.
```
SELECT client.client_name
FROM client
WHERE client.branch_id = (
	SELECT branch.branch_id
	FROM branch
	WHERE branch.mgr_id = 102
	LIMIT 1
)
```


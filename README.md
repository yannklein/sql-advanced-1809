# Lecture notes

## CRUD in SQL

```
-- READ 
-- SELECT * FROM Students s 

-- CREATE
-- INSERT INTO Students (name, age)
-- VALUES('Duong', 12)

-- UPDATE
-- UPDATE Students 
-- SET age = 22, name = 'Super Duong'
-- WHERE id = 27 OR id = 28

-- DELETE
-- DELETE FROM Students 
-- WHERE id = 29
```

## SQLITE functions

```
SELECT 
	name,
	SUBSTRING(name, 1, 3) substring_fct,
	TRIM(name, 'Kan') trim_fct,
	LTRIM(name, 'Kan') ltrim_fct,
	RTRIM(name, 'Kan') rtrim_fct,
	LENGTH(name) length_fct,
	UPPER(name) upper_fct,
	LOWER(name) lower_fct,
	REPLACE(name,'a','@') replace_a_fct,
	REPLACE(name,'an','@') replace_an_with_at_fct,
	REPLACE(name,'an','@') replace_an_fct,
	REPLACE(name,'n','@') replace_an_fct,
	INSTR(name, 'a') instr_fct
FROM Students 
```

## Window functions

```
SELECT 
	*,
	RANK() OVER (
		PARTITION BY o.customer_id 
		ORDER BY o.ordered_at
	) AS order_rank
FROM orders o
```

```
SELECT 
	*,
	SUM(amount)	OVER (
		PARTITION BY o.customer_id 
		ORDER BY o.ordered_at
	) AS cumulative_amount
FROM orders o 
```

## With clause
```
WITH matches_per_month AS(
	SELECT 
		STRFTIME('%Y-%m', DATE(m.date)) period,
		COUNT(m.id) match_count
	FROM Match m 
	GROUP BY period
)
SELECT
	*,
	SUM(match_count) OVER (
		ORDER BY period
	) AS cumul_count
FROM matches_per_month
```
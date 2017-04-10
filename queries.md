Gotchas/tips and tricks
- use single quotes for string declarations
- `tablename.*` selects all from tablename(when you do a JOIN)
- `c column_name/t` table_name allows you to later refer to said table/column by the given alias

# Queries

## select

1. Give me a list of all artists
```SQL
SELECT * FROM invoices
```

2. Give me a list of all artists
```SQL
SELECT * FROM artists
```

3. Give me the name of every artist
```SQL
SELECT name FROM artists
```

4. Give me the first and last names of every employee
```SQL
SELECT first_name, last_name FROM employees
```

5. Give me the names of every media type

```SQL
SELECT name FROM media_types
```

## order by

6. Give me a list of every employee by hire date in descending order

```SQL
SELECT * FROM employees
ORDER BY hire_date DESC
```

7. Give me the hire date, first name, and last name of all employees hired before February 15, 2011

```SQL
SELECT hire_date, first_name, last_name FROM employees
WHERE hire_date < 'February 15, 2011';
```

## where

8. Give me a list of all employees whose name begins with "A"

```SQL
SELECT * FROM employees
WHERE first_name LIKE 'A%'
```

9. Give me a list of all invoices from Redmond, WA

```SQL
SELECT * FROM invoices
WHERE billing_city = 'Redmond'
AND billing_state = 'WA'
```

10. Give me a list of all invoices from Berlin, Germany

```SQL
SELECT * FROM invoices
WHERE billing_city = 'Berlin'
AND billing_country = 'Germany'
```

11. Give me a list of all invoices from Canada

```SQL
SELECT * FROM invoices
WHERE billing_country = 'Canada'
```

12. Give me a list of all invoices from Alberta (AB), Canada

```SQL
SELECT * FROM invoices
WHERE billing_country = 'Canada'
AND billing_state = 'AB'
```

13. Give me a list of all invoices from Edmonton, Alberta (AB), Canada

```SQL
SELECT * FROM invoices
WHERE billing_country = 'Canada'
AND billing_state = 'AB'
AND billing_city = 'Edmonton'
```

14. Give me the billing addresses from every invoice from Redmond, WA

```SQL
SELECT billing_address FROM invoices
WHERE billing_state = 'WA'
AND billing_city = 'Redmond'
```

15. Give me a list of all invoices for more than $5.00 from Reno, NV

```SQL
SELECT * FROM invoices
WHERE total > 5
AND billing_city = 'Reno'
AND billing_state = 'NV'
```

16. Give me a list of every track without a composer

```SQL
SELECT * FROM tracks
WHERE composer = ''
OR composer IS NULL
```

17. Give me a list of every customer not associated with a company

```SQL
SELECT * FROM customers
WHERE company = ''
OR company IS NULL
```

18. Give me a list of all invoices from Redmond, WA sorted from low-to-high by total

```SQL
SELECT * FROM invoices
WHERE billing_city = 'Redmond'
AND billing_state = 'WA'
ORDER BY total
```

19. Give me a list of all invoices from Redmond, WA sorted from high-to-low by total

```SQL
SELECT * FROM invoices
WHERE billing_city = 'Redmond'
AND billing_state = 'WA'
ORDER BY total DESC
```

20. Give me a list of all invoices from Germany sorted from high-to-low by total

```SQL
SELECT * FROM invoices
WHERE billing_country = 'Germany'
ORDER BY total DESC
```

21. Give me a list of the 10 most expensive invoices from Germany

```SQL
SELECT * FROM invoices
WHERE billing_country = 'Germany'
ORDER BY total DESC
LIMIT 10
```

22. Give me a list of the 10 most expensive invoices from Boston, MA

```SQL
SELECT * FROM invoices
WHERE billing_city = 'Boston'
AND billing_state = 'MA'
ORDER BY total DESC
LIMIT 10
```

23. Give me a list of the 10 least expensive invoices from Boston, MA

```SQL
SELECT * FROM invoices
WHERE billing_city = 'Boston'
AND billing_state = 'MA'
ORDER BY total
LIMIT 10
```

23. Give me a list of the 10 least expensive invoices from Boston, MA

```SQL
SELECT * FROM invoices
WHERE billing_city = 'Boston'
AND billing_state = 'MA'
ORDER BY total
LIMIT 10
```

24. Give me the street addresses of the 3 most expensive invoices from Cupertino, CA

```SQL
SELECT billing_address FROM invoices
WHERE billing_city = 'Cupertino'
AND billing_state = 'CA'
ORDER BY total DESC
LIMIT 3
```

25. Give me a list of all invoices from either Cupertino, CA or Mountain View, CA

```SQL
SELECT * FROM invoices
WHERE billing_city = 'Cupertino'
AND billing_state = 'CA'
OR billing_city = 'Mountain View'
AND billing_state = 'CA'
```

33. Give me a list of the top 5 cities by number of invoices in descending order

```SQL
SELECT billing_city, COUNT(id) FROM invoices
GROUP BY billing_city
ORDER BY COUNT(id) DESC
LIMIT 5
```

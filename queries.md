Gotchas/tips and tricks
- use single quotes for string declarations
- `tablename.*` selects all from tablename(when you do a JOIN)
- `table_name t` allows you to later refer to said column by the given alias

# Queries

1. Give me a list of all invoices
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

26. Find the number of invoices sent to the city of "Santiago"

```SQL
SELECT COUNT(id) FROM invoices
WHERE billing_city = 'Santiago'
GROUP BY billing_city
```

27. Give me a count of the number of customers by country

```SQL
SELECT country, COUNT(id) FROM customers
GROUP BY country
```

28. Give me a count of the number of tracks by unit price

```SQL
SELECT unit_price, COUNT(id) FROM tracks
GROUP BY unit_price
```

29. Give me a list of all names of artists whose name contains "smith".

```SQL
SELECT name FROM artists
WHERE name LIKE '%smith%'
```

30. Give me a list of all names of artists whose name ends with "smith".

```SQL
SELECT name FROM artists
WHERE name LIKE '%smith'
```

31. Give me a count of the number of employees by city

```SQL
SELECT city, COUNT(id) FROM employees
GROUP BY city
```

32. Give me a count of the number of employees by city

```SQL
SELECT country, COUNT(id) FROM customers
GROUP BY country
ORDER BY COUNT(id) DESC
LIMIT 3
```

33. Give me a list of the top 5 cities by number of invoices in descending order

```SQL
SELECT billing_city, COUNT(id) FROM invoices
GROUP BY billing_city
ORDER BY COUNT(id) DESC
LIMIT 5
```

34. List all artist names alongside the titles of their albums

```SQL
SELECT name, title FROM artists
JOIN albums ON artists.id = artist_id
```

35. List all album names along with their track titles

```SQL
SELECT name, title FROM albums
JOIN tracks ON albums.id = album_id
```

36. List all artist names alongside the titles of their albums, in alphabetical order by artist name

```SQL
SELECT name, title FROM albums
JOIN artists ON artists.id = artist_id
ORDER BY name
```

36. List all artist names alongside the titles of their albums, in alphabetical order by artist name

```SQL
SELECT name, title FROM albums
JOIN artists ON artists.id = artist_id
ORDER BY name
```

36. List all artist names alongside the titles of their albums, in alphabetical order by artist name

```SQL
SELECT name, title FROM albums
JOIN artists ON artists.id = artist_id
ORDER BY name
```

37. List all customers' first and last names next to the totals on their invoices, ordered by total, high to low

```SQL
SELECT first_name, last_name, total FROM customers
JOIN invoices ON customers.id = customer_id
ORDER BY total DESC
```

38. Give me the customer (and their invoice) with the highest invoice total

```SQL
SELECT * from customers
JOIN invoices ON customers.id = customer_id
ORDER BY total DESC
LIMIT 1
```

39. Give me a list of every Aerosmith album

```SQL
SELECT * FROM albums
JOIN artists ON artists.id = artist_id
WHERE name = 'Aerosmith'
```

40. Give me a list of every Iron Maiden album

```SQL
SELECT * FROM albums
JOIN artists ON artists.id = artist_id
WHERE name = 'Iron Maiden'
```

41. Give me a list of albums that contains a song called "Midnight"

```SQL
SELECT * FROM albums
JOIN tracks ON albums.id = album_id
WHERE name = 'Midnight'
```

42. Give me a list of every artist who has performed the song "Midnight"

```SQL
SELECT ar.name FROM albums al, artists ar, tracks t
WHERE ar.id = al.artist_id
AND t.album_id = al.id
AND t.name = 'Midnight'
```

43. Give me a count of the number of albums by Iron Maiden

```SQL
SELECT COUNT(al.id) FROM albums al, artists ar
WHERE ar.id = artist_id
AND ar.name = 'Iron Maiden'
```

44. List all artists and the number of albums they each have, ordered by the artist's name

```SQL
SELECT artists.name, COUNT(albums.id) FROM artists, albums
WHERE artist_id = artists.id
GROUP BY artists.id
ORDER BY name
```

45. List all albums next to the number of tracks they each have, ordered by the number of tracks and then the album name

```SQL
SELECT albums.title, COUNT(tracks.id) FROM albums, tracks
WHERE album_id = albums.id
GROUP BY albums.id
ORDER BY COUNT(tracks.id) DESC, title
```

46. Find the artist with the most albums

```SQL
SELECT artists.*, COUNT(artists.name) FROM artists, albums
WHERE artist_id = artists.id
GROUP BY artists.id
ORDER BY COUNT(artists.name) DESC
LIMIT 1
```

47. Find the album with the most tracks
```SQL
SELECT albums.*, COUNT(albums.id) FROM albums, tracks
WHERE tracks.album_id = albums.id
GROUP BY albums.id
ORDER BY COUNT(albums.id) DESC
LIMIT 1
```

48. List the names of the top five customers based on the sums of their invoice totals

```SQL
SELECT customers.first_name, customers.last_name, SUM(invoices.total) FROM customers, invoices
WHERE invoices.customer_id = customers.id
GROUP BY customers.id
ORDER BY SUM(invoices.total) DESC
LIMIT 5
```

49. Give me a list of all artists sorted alphabetically by first name

```SQL
SELECT * FROM artists
ORDER BY name
```

50. List all albums next to the number of tracks they each have in descending order

```SQL
SELECT albums.*, COUNT(albums.id) FROM albums, tracks
WHERE albums.id = tracks.album_id
GROUP BY albums.id
ORDER BY COUNT(albums.id) DESC
```

51. List all albums next to the number of tracks they each have in descending order

```SQL
SELECT artists.*, COUNT(artists.id) FROM artists, albums
WHERE artists.id = albums.artist_id
GROUP BY artists.id
ORDER BY COUNT(artists.id) DESC, name
```

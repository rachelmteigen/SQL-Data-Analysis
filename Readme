# This is SQL homework using Pagila database
=====================================================================================
You can install Pagila database from [here](https://github.com/anupamlalwani/SQL_Pagila/tree/master/Get%20Pagila%20Database)

##### 1
a. You need a list of all the actors.  display the first and last names of all actors from the table actor.

```
SELECT
	first_name, 
	last_name
FROM 
	actor;
```

b. Display the first and last name of each actor in a single column in upper case letters. Name the column Actor Name.

```
SELECT
	CONCAT(UPPER(first_name), ' ', UPPER(last_name)) as "Actor Name"
FROM 
	actor;
```

##### 2
a. You need to find the ID number, first name, and last name of an actor, of whom you know only the first name, "Joe." What is one query would you use to obtain this information?

```
SELECT
	actor_id,
	first_name,
	last_name
FROM 
	actor
WHERE 
	first_name = 'JOE';
```

b. Find all actors whose last name contain the letters GEN:

```
SELECT
	first_name,
    last_name
FROM 
	actor
WHERE 
	last_name like '%GEN%';
```

c. Find all actors whose last names contain the letters LI. This time, order the rows by last name and first name, in that order
Make this case insensitive.

```
SELECT
	first_name,
    last_name
FROM 
	actor
WHERE 
	last_name ilike '%LI%'
ORDER BY 
	last_name, first_name;
```

d. Using IN, display the country_id and country columns of the following countries: Afghanistan, Bangladesh, and China:

```
SELECT
	country_id,
    country
FROM 
	country
WHERE 
	country in ('Afghanistan', 'Bangladesh', 'China');```
```

##### 3
a. Add a middle_name column to the table actor. Specify the appropriate column type

```
ALTER TABLE 
	actor
ADD COLUMN 
	middle_name VARCHAR(180);
```

b. You realize that some of these actors have tremendously long last names. Change the data type of the middle_name column to something that can hold more than varchar.

```
ALTER TABLE 
	actor
ALTER COLUMN 
	middle_name TYPE bytea USING middle_name::bytea; --converting datatype to Blob
```
c. Now write a query that would remove the middle_name column.

```
ALTER TABLE 
	actor
DROP COLUMN 
	middle_name;
```

##### 4
a. List the last names of actors, as well as how many actors have that last name.

```
SELECT 
	last_name,
	COUNT(last_name) AS actors_with_this_lastname
FROM 
	actor
GROUP BY 
	last_name
ORDER BY 
	COUNT(last_name) DESC;
```
b. List last names of actors and the number of actors who have that last name,but only for names that are shared by at least two actors

```
SELECT 
	last_name,
	COUNT(last_name) AS actors_with_lastname
FROM 
	actor
GROUP BY 
	last_name
HAVING 
	COUNT(last_name) >= 2 
ORDER BY 
	COUNT(last_name) DESC;
```

c. Oh, no! The actor HARPO WILLIAMS was accidentally entered in the actor table as GROUCHO WILLIAMS, the name of Harpo's second cousin's husband's yoga teacher. Write a query to fix the record.

```
UPDATE 
	actor
SET 
	first_name  = 'HARPO'
WHERE 
	first_name = 'GROUCHO' and last_name = 'WILLIAMS';
```

d. Perhaps we were too hasty in changing GROUCHO to HARPO. It turns out that GROUCHO was the correct name after all! In a single query, if the first name of the actor is currently HARPO, change it to GROUCHO. 
Otherwise, change the first name to MUCHO GROUCHO, as that is exactly what the actor will be with the grievous error. 
BE CAREFUL NOT TO CHANGE THE FIRST NAME OF EVERY ACTOR TO GROUCHO, HOWEVER! (Hint: update the record using a unique identifier.)

```
UPDATE 
	actor
SET first_name  = 
( 
	CASE WHEN first_name = 'HARPO' THEN 'GROUCHO'
	ELSE 'MUCHO GROUCHO'
    END
)     
WHERE 
	actor_id = 172;
```

##### 5

1.What’s the difference between a left join and a right join. 
=> When two tables are joined by a left join, the output includes all the rows from left table and all the rows with common values in both tables from right table. When tables are joined by a right join, the output includes all the rows from right table and all the rows with common values in both tables from left table.

example tables for below Q5 subquestions: 

**Table A**    

|id   | name |
|---- | ---- |
|1 | a |
|2 | b |
|3 | c |
|4 | d |
|5 | e | 

**Table B**

|id | name |
|----|----|
|1	|	p |
|2	|	q |
|3	|	a |
|4	|	b |
|5	|	r |


_LEFT JOIN EXAMPLE_:
```
SELECT *
FROM A
LEFT JOIN B
ON A.id = B.id
```

Will return 5 rows with name values (a,b,c,d,e,f) and 2 columns(id, name)from table A, as table B has a and b as common values from table B.

_RIGHT JOIN EXAMPLE_:
```
SELECT *
FROM A
RIGHT JOIN B
ON A.id = B.id
```

Will return 5 rows with name values(p,q,a,b,r) and 2 columns (id, name) from table B, as table A has a and b as common values with table B.


2.What about an inner join and an outer join? 
=> When two tables are joined by an inner join, the output table shows the rows that are common in both the tables.
Whereas when two tables are joined by an outer join, the output table is like a union of two tables.

_INNER JOIN EXAMPLE_:
```
SELECT *
FROM A
INNER JOIN B
ON A.id = B.id
```

Will return 2 rows with name values (a,b) and 2 columns (id, name) which are common values in both tables.

_OUTER JOIN EXAMPLE_:
```
SELECT * 
FROM A
OUTER JOIN B
ON A.id = B.id 
```

Will return 8 rows with name values (a,b,c,d,e,p,q,r) and 2 columns (id, name). column that does not have common value across both tables will show NULL value in that row. 


3.When would you use rank? 
=> In situations when we need to find out class rankings of students I can use rank a windows function, that will be a nice use case of rank function. If there is a tie between two students who rank 2nd, next highest score will get a 4th ranking because there are 2 students on 2nd rank. 

4.What about dense_rank? 
=> when we want to maintain the density of rankings and don't want to skip a rank in case there is a tie, dense ranking can be used. A use case can be, if we want to find out best sales employee of the month, if two emplyees have bring the equal sales revenue, the second highest sales revenue will be given 2nd rank and not 3rd when dense ranked.

5.When would you use a subquery in a select? 
=> There can be multiple use cases of subqueries - when we want to  filter something in where clause without a join, 
when we want to filter something but we don't know the exact value of the filter that is best use case of subquery. Subqueries can also be used instead of inline views or multiple joins to reduce the query cost/increase performace.

6.When would you use a right join?
=> When there are multiple left joins going on in a query, the left side of equation gets bulky and has many columns, and we can do a right join to filter down to something specifically in right table. 

7.When would you use an inner join over an outer join?
=> if two tables have any column row values or columns, inner join can help getting precise results over outer join and cn help filter out rows efficiently even without using a WHERE clause.

8.What’s the difference between a left outer and a left join
=> There is no difference. Different name of same type of join.

9.When would you use a group by?
=> If query has any aggregation going on in it, all the columns called out in select clause (except the aggregation column) will be called in group by clause.

10.Describe how you would do data reformatting?
=> There are multiple ways to reformat data: CAST(), CONVERT(), FORMAT()
Example
```
SELECT CAST(4.25 AS int); returns --> 4
SELECT CONVERT(float, '4.25'); returns --> 4.25
SELECT CONVERT(datetime, '2017-09-25'); returns --> 2017-09-25 00:00:00.000
SELECT FORMAT(now(), 'YYYY-MM-DD'); returns --> 2017-09-26 
```

11.When would you use a with clause?
=> If there are multiple joins or subqueries going on in the query, its better to use with clause, which acts as an in-line view that gives the advantage of a view without creating a permanent view. Querying off of an in-line view helps strucure the query in a better way. 

12.BONUS: When would you use a self join?
=> Self join can be used to identify/remove duplicate values from a table. It can also be used when we need to find out if there is any relationship between rows of same table. 
For example, if there is an employee information table that also has a column of employee supervisor_id, doing a self join on employee table can help get the name of supervisor with help of just supervisor_id and name column.

##### 6
a. Use JOIN to display the first and last names, as well as the address, of each staff member. Use the tables staff and address:

```
SELECT
	s.first_name,
	s.last_name,
	a.address
FROM 
	staff s
INNER JOIN 
	address a
	ON s.address_id = a.address_id
```

b. Use JOIN to display the total amount rung up by each staff member in January of 2007. Use tables staff and payment.

```
SELECT
	s.first_name,
	s.last_name,
	SUM(p.amount) as Total_Amt
FROM 
	staff s
INNER JOIN payment p 
	ON s.staff_id = p.staff_id
WHERE
	EXTRACT(month FROM payment_date) = 1 AND 
    EXTRACT(year FROM payment_date) = 2007
GROUP BY 
	s.first_name, s.last_name
```

c. List each film and the number of actors who are listed for that film. Use tables film_actor and film. Use inner join.

```
SELECT
	f.film_id,
	f.title,
	COUNT(fa.actor_id) as Number_of_Actors
FROM 
	film f
INNER JOIN film_actor fa
	ON f.film_id = fa.film_id
GROUP BY 
	f.film_id,f.title
ORDER BY
	film_id;
```

d. How many copies of the film Hunchback Impossible exist in the inventory system?

```
SELECT
	f.title as film_title,
	COUNT(i.film_id) AS stock
FROM 
	film f
INNER JOIN inventory i
ON f.film_id = i.film_id
WHERE 
	f.title = 'HUNCHBACK IMPOSSIBLE'
GROUP BY 
	f.title;
```

e. Using the tables payment and customer and the JOIN command, list the total paid by each customer. List the customers alphabetically by last name:

```
SELECT
	c.first_name,
	c.last_name,
	SUM(p.amount) as Total_Amount_Paid
FROM 
	customer c
JOIN payment p
ON c.customer_id = p.customer_id
GROUP BY 
	c.first_name, c.last_name
ORDER BY c.last_name;
```

##### 7
a. The music of Queen and Kris Kristofferson have seen an unlikely resurgence. As an unintended consequence, 
films starting with the letters K and Q have also soared in popularity. Use subqueries to display the titles of movies starting with the letters K and Q whose language is English.

_using subquery in from clause_
```
SELECT
	title
FROM
(	
    SELECT 
    	f.title
    FROM
    	film f
    JOIN language l
    ON l.language_id = f.language_id
    where 
    	f.title like 'K%' OR title like 'Q%'
    AND l.name = 'English'
)as something;
```

_another method using subquery in WHERE clause_

```
SELECT 
	title
FROM 
	film
WHERE 
	title in
(
	SELECT 
    	title
	FROM 
    	film
	WHERE
    	title LIKE 'K%' OR title LIKE 'Q%'
		AND language_id = 1
)
ORDER BY
	title;
```

b. Use subqueries to display all actors who appear in the film Alone Trip.

_Method 1: using 2 subqueries in nested loop with cost = 26.76_
```
SELECT
	first_name,
	last_name
FROM 
	actor
WHERE 
	actor_id IN
(
    SELECT actor_id 
    FROM film_actor
    WHERE film_id IN
	(
    	SELECT film_id
    	FROM film
    	WHERE title = 'ALONE TRIP'
	)
);
```

_Method 2: Using 1 subquery with cost = 24.15_

```
SELECT
	first_name,
	last_name
FROM 
	actor
WHERE 
	actor_id IN
(
    SELECT actor_id 
    FROM film_actor
    WHERE film_id = 17

);
```

_Method 3: using joins with cost = 4.74_
```
SELECT
	first_name, 
    last_name
FROM
	actor a
JOIN
	film_actor fa
ON a.actor_id = fa.actor_id
JOIN
	film f
ON f.film_id = fa.film_id
WHERE 
	f.title = 'ALONE TRIP';
```

c. You want to run an email marketing campaign in Canada, for which you will need the names and email addresses of all Canadian customers. Use joins to retrieve this information.
```
SELECT
	c.first_name, 
	c.last_name,
	c.email,
	a.address,
	co.country
FROM 
	customer c
LEFT JOIN address a
ON c.address_id = a.address_id
LEFT JOIN city ci
ON a.city_id = ci.city_id
LEFT JOIN country co
ON ci.country_id = co.country_id
WHERE co.country = 'Canada';
```

d. Sales have been lagging among young families, and you wish to target all family movies for a promotion. 
Identify all movies categorized as a family film
```
SELECT 
	f.title as "Family movies list"
FROM
	film f
LEFT JOIN 
	film_category fc
ON f.film_id = fc.film_id
LEFT JOIN
	category c
ON c.category_id = fc.category_id
WHERE
	c.name iLIKE '%Family%';
```

e. Display the most frequently rented movies in descending order.
```
SELECT
	f.title,
    f.film_id,
    COUNT(rental_id) AS "Number of times rented"
FROM 
	film f
LEFT JOIN inventory i
ON f.film_id = i.film_id
LEFT JOIN rental r
ON r.inventory_id = i.inventory_id
GROUP BY 
	f.film_id,
    f.title
order by count(rental_id) DESC;
```

f. Write a query to display how much business, in dollars, each store brought in.
```
select
	s.store_id as "Store Number",
    SUM(p.amount) as "Total Business(in $)"
FROM
	store s
INNER JOIN customer c
ON c.store_id = s.store_id
INNER JOIN payment p
ON p.customer_id = c.customer_id
GROUP by 
	s.store_id
ORDER BY 
	s.store_id;
```

g. Write a query to display for each store its store ID, city, and country.
```
SELECT
	s.store_id as "Store Number",
    c.city,
    co.country
FROM
	store s
LEFT JOIN address a
ON s.address_id = a.address_id
LEFT JOIN city c
ON c.city_id = a.city_id
LEFT JOIN country co
ON c.country_id = co.country_id
```

h. List the top five genres in gross revenue in descending order. 

_Method 1: Multiple joins with cost = 3532.82_
```
SELECT
	c.name AS "Genre",
    --f.title,
    SUM(p.amount) AS "Gross Revenue (in $)" 
FROM
	film f
LEFT JOIN film_category fc
ON fc.film_id = f.film_id
LEFT JOIN category c
ON fc.category_id = c.category_id
LEFT JOIN inventory i
ON i.film_id = f.film_id
LEFT JOIN rental r
ON r.inventory_id = i.inventory_id
LEFT JOIN payment p
ON p.rental_id = r.rental_id
WHERE p.amount IS NOT NULL
GROUP BY c.name
ORDER BY SUM(p.amount) DESC
LIMIT 5;
```
_Method 2: Subquery with cost = 1719_
```
SELECT
	a.name as "Genre",
    SUM(amount) as "Gross Revenue(in $)"
FROM
(	
    SELECT
		c.name, f.title, p.amount 
	FROM film f
	LEFT JOIN film_category fc
	ON fc.film_id = f.film_id
	LEFT JOIN category c
	ON fc.category_id = c.category_id
	LEFT JOIN inventory i
	ON i.film_id = f.film_id
	LEFT JOIN rental r
	ON r.inventory_id = i.inventory_id
	LEFT JOIN payment p
	ON p.rental_id = r.rental_id
	WHERE p.amount IS NOT NULL
) a

GROUP BY name
ORDER BY sum(amount) desc
LIMIT 5;
```

##### 8
a. In your new role as an executive, you would like to have an easy way of viewing the Top five genres by gross revenue. Use the solution from the problem above to create a view.

```
DROP VIEW IF EXISTS top_five_genres;

CREATE VIEW top_five_genres
AS

SELECT
	a.name as "Genre",
    SUM(amount) as "Gross Revenue(in $)"
FROM
(	
    SELECT
		c.name, f.title, p.amount 
	FROM film f
	LEFT JOIN film_category fc
	ON fc.film_id = f.film_id
	LEFT JOIN category c
	ON fc.category_id = c.category_id
	LEFT JOIN inventory i
	ON i.film_id = f.film_id
	LEFT JOIN rental r
	ON r.inventory_id = i.inventory_id
	LEFT JOIN payment p
	ON p.rental_id = r.rental_id
	WHERE p.amount IS NOT NULL
) a

GROUP BY name
ORDER BY sum(amount) desc
LIMIT 5;
```

b. How would you display the view that you created in 8a?
```
SELECT * 
FROM
	top_five_genres;
```

c. You find that you no longer need the view top_five_genres. Write a query to delete it.
```
DROP VIEW top_five_genres;
```
----------------------------------- ~~ ~~~x~~~ ~~~x~~~ ~~~x~~~ ~~ -----------------------------------------










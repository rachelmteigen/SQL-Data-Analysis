# SQL_Homework
SQL Homework Assignment

Pavan is happy to do a 1 on 1 with you to go over anything in particular. Please message him on slack

1a. You need a list of all the actors’ first name and last name 

select a.first_name, a.last_name
FROM actor a;

1b. Display the first and last name of each actor in a single column in upper case letters. Name the column Actor Name  --CONCAT

select concat(first_name, ' ', last_name) AS ACTOR_NAME
from actor;



2a. You need to find the id, first name, and last name of an actor, of whom you know only the first name of "Joe." What is one query would you use to obtain this information? 

SELECT a.actor_id, a.first_name
 FROM actor a
 WHERE a.first_name = 'JOE';

2b. Find all actors whose last name contain the letters GEN. Make this case insensitive ILKE

SELECT * 
FROM actor
WHERE  last_name iLIKE '%GEN%';

2c. Find all actors whose last names contain the letters LI. This time, order the rows by last name and first name, in that order. Make this case insensitive.

SELECT * 
FROM actor
WHERE  last_name iLIKE '%LI%'
ORDER BY last_name, first_name;


2d. Using IN, display the country_id and country columns of the following countries: Afghanistan, Bangladesh, and China:

select * 
FROM country
WHERE country IN ('Afghanistan', 'Bangladesh', 'China');

3a. Add a middle_name column to the table actor. Specify the appropriate column type

ALTER TABLE actor ADD COLUMN middle_name varchar(255);

3b. You realize that some of these actors have tremendously long last names. Change the data type of the middle_name column to something that can hold more than varchar. VARCHAR(max)
Now we didn’t explicitly cover this in class so exercise your googling skills. 

ALTER TABLE actor ALTER COLUMN middle_name varchar(max);

3c. Now write a query that would remove the middle_name column. 

ALTER TABLE actor DROP COLUMN middle_name;

4a. List the last names of actors, as well as how many actors have that last name. COUNT 

select a.last_name, count(*) as count
  from actor a
  group by a.last_name
  order by count desc;
  
4b. List last names of actors and the number of actors who have that last name, but only for names that are shared by at least two actorS HAVING

select a.last_name, count(*) as count
  from actor a
  group by a.last_name
  HAVING COUNT (a.last_name)  > 2;
  
4c. Oh, no! The actor HARPO WILLIAMS was accidentally entered in the actor table as GROUCHO WILLIAMS. Write a query to fix the record.

UPDATE actor
SET first_name = 'HARPO'
WHERE first_name = 'GROUCHO', last_name = 'WILLIAMS';

4d. Perhaps we were too hasty in changing GROUCHO to HARPO. It turns out that GROUCHO was the correct name after all! 
In a single query, 
if the first name of the actor is currently HARPO, change it to GROUCHO. UPDATE
Otherwise, change the first name to MUCHO GROUCHO, as that is exactly what the actor will be with the grievous error. 
BE CAREFUL NOT TO CHANGE THE FIRST NAME OF EVERY ACTOR TO MUCHO GROUCHO
(Hint: update the record using a unique identifier.)

UPDATE actor
SET first_name = 'GROUCHO'
WHERE first_name = 'HARPO', last_name = 'WILLIAMS';

5a. 
What’s the difference between a left join and a right join.
LEFT JOIN: joins left table with right table
RIGHT JOIN: joins right table with left table

What about an inner join and an outer join? 
INNER JOIN: selects data/columns that have matching values in both tables
OUTER JOIN: or full join will take all the data for all tables regardless if there is a matching column

When would you use rank? 
Rank would be used when you would like to treat equal rows the same but this produces gaps between groups or it assigns a value to each unique row.

What about dense_rank? 
Dense_rank would be used you would like NO gaps in ranking--it provides consecutive order.

When would you use a subquery in a select? 
SQL subquery is usually added in the WHERE Clause of the SQL statement. Most of the time, a subquery is used when you know how to search for a value using a SELECT statement, but do not know the exact value in the database

When would you use a right join?
Right joins are not commonly used--if you want all records from table2 even if they don't have a col that matches table1's (also included are table1 records with matches).

When would you use an inner join over an outer join?
Inner Join:  when you ONLY want matching data values
Outer Join: When you want ALL data regardless if aligns or matches.

What’s the difference between a left outer and a left join?
They are the same thing!

When would you use a group by?
The GROUP BY clause will gather all of the rows together that contain data in the specified column(s) and will allow aggregate functions to be performed on the one or more columns.

Describe how you would do data reformatting
Combining and cleaning up data and tables. 

When would you use a with clause?
WITH clause allows you to give a sub-query block a name a process also called sub-query refactoring, which can be referenced in several places within the main SQL query.

6a. Use a JOIN to display the first and last names, as well as the address, of each staff member. Use the tables staff and address:
SELECT a.address, s.last_name, s.first_name
FROM address a
RIGHT JOIN staff s
ON a.address_id = s.address_id;


6b. Use a JOIN to display the total amount rung up by each staff member in August of 2005. Use tables staff and payment.
WITH pay_jan_oh_sevent AS (SELECT EXTRACT(MONTH FROM p.payment_date) AS month, EXTRACT(YEAR FROM p.payment_date) AS year, s.staff_id, s.first_name, s.last_name, p.amount
FROM payment p
LEFT JOIN staff s
ON p.staff_id = s.staff_id
WHERE EXTRACT(MONTH FROM p.payment_date) = 1 AND EXTRACT(YEAR FROM p.payment_date) = 2007)
SELECT staff_id, first_name, last_name, SUM(amount)
FROM pay_jan_oh_sevent
GROUP BY staff_id, first_name, last_name;



You’ll have to google for this one, we didn’t cover it explicitly in class. 
6c. List each film and the number of actors who are listed for that film. Use tables film_actor and film. Use inner join.
SELECT p.film_id, p.title, c.actor_id, COUNT(c.actor_id)
FROM film p
INNER JOIN film_actor c
ON p.film_id = c.film_id
GROUP BY p.film_id, c.actor_id
ORDER BY p.film_id;


6d. How many copies of the film Hunchback Impossible exist in the inventory system?
WITH S1 AS
(SELECT p.film_id, p.title, inv.inventory_id
FROM film p
LEFT JOIN inventory inv
ON p.film_id = inv.film_id
WHERE title iLIKE '%Hunchback Impossible%')
SELECT COUNT(title)
FROM S1;



6e. Using the tables payment and customer and the JOIN command, list the total paid by each customer. List the customers alphabetically by last name:
SELECT c.last_name, SUM(p.amount)
FROM payment p
LEFT JOIN customer c
ON p.customer_id = c.customer_id
GROUP BY c.last_name 
ORDER BY last_name ASC;



7a. The music of Queen and Kris Kristofferson have seen an unlikely resurgence. As an unintended consequence, films starting with the letters K and Q have also soared in popularity. display the titles of movies starting with the letters K and Q whose language is English.
SELECT f.title, l.language_id, l.name
FROM film f
LEFT JOIN language l
ON f.language_id = l.language_id  
WHERE title iLIKE 'Q%' OR  title iLIKE 'K%' OR name iLIKE 'English%'
GROUP BY f.title, l.name, l.language_id;
7b. Use subqueries to display all actors who appear in the film Alone Trip.
SELECT f.title, fa.actor_id, a.last_name
FROM film f
LEFT JOIN film_actor fa
ON f.film_id = fa.film_id
LEFT JOIN actor a
ON fa.actor_id = a.actor_id
WHERE title = 'ALONE TRIP';
7c. You want to run an email marketing campaign in Canada, for which you will need the names and email addresses of all Canadian customers. Use joins to retrieve this information.
SELECT co.country, a.address, cu.email, cu.last_name, cu.first_name
FROM city c
RIGHT JOIN address a
ON c.city_id = a.city_id
LEFT JOIN country co
ON c.country_id = co.country_id
RIGHT JOIN customer cu
ON a.address_id = cu.address_id
WHERE country = 'Canada';


7d. Sales have been lagging among young families, and you wish to target all family movies for a promotion. Identify all movies categorized as a family film.
SELECT f.title, cat.name
FROM category cat
LEFT JOIN film_category fc
ON cat.category_id = fc.category_id
LEFT JOIN film f
ON fc.film_id = f.film_id
WHERE name = 'Family' OR name = 'Children';

Now we mentioned family film, but there is no family film category. There’s a category that resembles that. In the real world nothing will be exact.
7e. Display the most frequently rented movies in descending order.
SELECT f.title, COUNT(p.rental_id) as total
FROM rental r
LEFT JOIN inventory i
ON r.inventory_id = i.inventory_id
LEFT JOIN film f
ON i.film_id = f.film_id
LEFT JOIN payment p
ON r.rental_id = p.rental_id
GROUP BY f.title
ORDER BY total DESC;


7f. Write a query to display how much business, in dollars, each store brought in.
SELECT s.store_id, SUM(p.amount) AS total
FROM payment p
LEFT JOIN staff s
ON p.staff_id = s.staff_id
GROUP BY s.store_id
ORDER BY total;

7g. Write a query to display for each store its store ID, city, and country.
SELECT  s.store_id, a.address, c.city, co.country
FROM city c
RIGHT JOIN address a
ON c.city_id = a.city_id
LEFT JOIN country co
ON c.country_id = co.country_id
RIGHT JOIN store s
ON a.address_id = s.address_id;


7h. List the top five genres in gross revenue in descending order. 
SELECT  c.name, SUM(p.amount) AS total
FROM rental r
LEFT JOIN inventory i
ON r.inventory_id = i.inventory_id
LEFT JOIN film_category fc
ON i.film_id = fc.film_id
LEFT JOIN category c
ON fc.category_id = c.category_id
LEFT JOIN payment p
ON r.rental_id = p.rental_id
GROUP BY c.name 
ORDER BY c.name DESC;

8a. In your new role as an executive, you would like to have an easy way of viewing the Top five genres by gross revenue. Use the solution from the problem above to create a view. 
CREATE VIEW as top_five_genres
SELECT  c.name, SUM(p.amount) AS total
FROM rental r
LEFT JOIN inventory i
ON r.inventory_id = i.inventory_id
LEFT JOIN film_category fc
ON i.film_id = fc.film_id
LEFT JOIN category c
ON fc.category_id = c.category_id
LEFT JOIN payment p
ON r.rental_id = p.rental_id
GROUP BY c.name 
ORDER BY c.name DESC
LIMIT 5;

8b. How would you display the view that you created in 8a?
SELECT * from top_five_genres
limit 10;

8c. You find that you no longer need the view top_five_genres. Write a query to delete it.
DROP VIEW top_five_genres;



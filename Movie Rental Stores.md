In this project I wrote more advanced SQL queries on a database designed to resemble a real-world database system - MySQL’s Sakila Sample Database.
The Sakila sample database is designed to represent a DVD rental store. 

I wrote SQL to manage a chain of movie rental stores, for example,
- Track the inventory level and determine whether the rental can happen 
- Manage customer in formation and identify loyalty customers
- Monitor customers’ owing balance and find overdue DVDs

This project can be considered as a typical retail-related business case, because it has the main metrics that can be found in any retailer’s real database, such Walmart, Shoppers, Loblaws, Amazon...

## Exercise 1
Before doing any exercise, data exploration came first. For Exercise 1, product-related data should be focused on, which is the film (DVD) in this project. Please explore the product-related tables (actor, film_actor, film, language, film_category, category) by using ‘SELECT *’ – do not forget to limit the number of records
```
SELECT * FROM actor limit 100;
SELECT * FROM film_actor limit 100;
SELECT * FROM film limit 100;
SELECT * FROM language limit 100;
SELECT * FROM film_category limit 100;
SELECT * FROM category limit 100;
```

## Exercise 2: Use *film* table
### What is the largest rental_rate for each rating?
```
SELECT rating, max(rental_rate)
FROM film
GROUP BY rating;
```

### How many films in each rating category?
```
SELECT rating, COUNT(DISTINCT film_id) AS number_of_films
FROM film
GROUP BY rating;
```

### Create a new column film_length to segment different films by length: length < 60 then ‘short’; length < 120 then ‘starndard’; lengh >=120 then ‘long’, then count the number of files in each segment.
```
SELECT CASE WHEN length > 0 AND length < 60 THEN 'short'			
		    WHEN length >= 60 AND length < 120 THEN 'standard'            
		    WHEN length >=120 THEN 'long'           
                         ELSE 'others'            
                         END as film_length, 
                         count(film_id) FROM film            
                         group by 1
                         order by 2;
```

## Exercise 3: Use *actor* table
### Which actors have the last name ‘Johansson’
```
SELECT * 
FROM actor 
WHERE last_name= 'Johansson';
```

### How many distinct actors’ last names are there?
```
SELECT COUNT(DISTINCT last_name) AS Distinct_last_names
FROM actor;
```

### Which last names are not repeated? Hint: use COUNT() and GROUP BY and HAVING
```
SELECT last_name,
COUNT(*) AS num_last_name
FROM actor
GROUP BY last_name
HAVING COUNT(*) = 1;
```

### Which last names appear more than once?
```
SELECT last_name,
COUNT(*) AS num_last_name
FROM actor
GROUP BY last_name
HAVING COUNT(*) > 1;
```

## Exercise 3: Use *film_actor* table
### Count the number of actors in each film, order the result by the number of actors with descending order
```
SELECT film_id,
COUNT(DISTINCT actor_id) AS num_of_actor
FROM film_actor
GROUP BY film_id
ORDER BY num_of_actor DESC;
```

### How many films each actor played in?
```
SELECT actor_id,
COUNT(DISTINCT film_id) AS num_of_film
FROM film_actor
GROUP BY actor_id 
ORDER BY num_of_film DESC;
```

## Exercise 4
### Find language name for each film by using table Film and Language
```
SELECT film.*, language.name AS language_name
FROM film LEFT JOIN language ON film.language_id = language.language_id;
```

### In table Film_actor, there are actor_id and film_id columns. I want to know the actor name for each actor_id, and film tile for each film_id. Hint: Use multiple table Inner Join
```
SELECT film_actor.*, actor.first_name, actor.last_name, film.title
FROM film_actor JOIN actor ON film_actor.actor_id = actor.actor_id
JOIN film ON film_actor.film_id = film.film_id;
```

### In table Film, there are no category information. I want to know which category each film belongs to. Hint: use table film_category to find the category id for each film and then use table category to get category name
```
SELECT f.*, c.name AS category_name
FROM film AS f LEFT JOIN film_category AS fc ON f.film_id = fc.film_id
LEFT JOIN category AS c ON fc.category_id = c.category_id;
```

### Select films with rental_rate > 2 and then combine the results with films with rating G, PG-13 or PG
```
SELECT * 
FROM film 
WHERE rating IN ('G', 'PG-13', 'PG')
UNION
SELECT *
FROM film 
WHERE rental_rate > 2;
```

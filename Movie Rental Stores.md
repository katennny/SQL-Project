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

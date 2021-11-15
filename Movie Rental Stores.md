In this project I wrote more advanced SQL queries on a database designed to resemble a real- world database system - MySQL’s Sakila Sample Database.
Development of the Sakila sample database began in early 2005. Early designs were based on the database used in the Dell whitepaper (Three Approaches to MySQL Applications on Dell PowerEdge Servers).
The Sakila sample database is designed to represent a DVD rental store. The Sakila sample database still borrows film and actor names from the Dell sample database.

I wrote SQL to manage a chain of movie rental stores, for example,
- Tracktheinventorylevelanddeterminewhethertherentalcanhappen 
- Managecustomerinformationandidentifyloyaltycustomers
- Monitorcustomers’owingbalanceandfindoverdueDVDs
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

## Exercise 2
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


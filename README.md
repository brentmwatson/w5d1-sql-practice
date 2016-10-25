# w5d1-sql-practice
(bonus**) How many items are in the items table?
`SELECT count(*) FROM items;`
100

(bonus**) How many books are in the items table?
`SELECT count (*) FROM items WHERE category LIKE "%Book%";`
10

How many users are there?
`SELECT count(*) FROM users;`
50

What are the 5 most expensive items?
`SELECT title,price FROM items ORDER BY price DESC LIMIT 5`
Small Cotton Gloves   |9984
Small Wooden Computer |9859
Awesome Granite Pants |9790
Sleek Wooden Hat      |9390
Ergonomic Steel Car   |9341

What's the cheapest book? (Does that change for "category is exactly 'book' "versus "category contains 'book'"?)

`SELECT title FROM items WHERE category = "Books" ORDER BY price LIMIT 1;`
Ergonomic Granite Chair

`SELECT title  FROM items WHERE category LIKE "%Book%" ORDER BY price LIMIT 1;`
Ergonomic Granite Chair

Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
`SELECT first_name,last_name FROM users WHERE id IN (SELECT user_id FROM addresses WHERE street LIKE "6439 Zetta Hills");`
Corrine|Little

`SELECT street,city,state,zip FROM addresses WHERE user_id IN (SELECT id FROM users WHERE (first_name LIKE "Corrine") AND (last_name LIKE "little"));`
6439 Zetta Hills|Willmouth|WY|15029
54369 Wolff Forges|Lake Bryon|CA|31587
YES

Correct Virginie Mitchell's address to "New York, NY, 10108".
`UPDATE addresses SET city="New York",state="NY",zip="10108" WHERE user_id IN (SELECT id FROM users WHERE (first_name LIKE "Virginie") AND (last_name LIKE "Mitchell"));`
12263 Jake Crossing|New York|NY|10108
83221 Mafalda Canyon|New York|NY|10108

How much would it cost to buy one of each tool?
`SELECT SUM (items.price) FROM items WHERE category like "%tool%";`
46477

How many total items did we sell?
`SELECT SUM (quantity) FROM orders;`
2125

How much was spent on books?
`SELECT SUM (items.price*orders.quantity) FROM orders INNER JOIN items ON items.id = orders.item_id WHERE items.category LIKE "%Book%";`
1081352

Simulate buying an item by inserting a User for yourself and an Order for that User.
`INSERT INTO users (first_name,last_name,email) VALUES ("Brent","Watson","brentmwatson@gmail.com");`

`INSERT INTO orders(user_id,item_id,quantity) VALUES(51,60,1);`
378|51|60|1|

`UPDATE orders SET created_at = STRFTIME('%Y-%m-%d %H:%M:%f', 'NOW') WHERE user_id IN (SELECT id FROM users WHERE (first_name LIKE "Brent") AND (last_name LIKE "Watson"));`
378|51|60|1|2016-10-25 00:17:42.960

What item was ordered most often? Grossed the most money?

What user spent the most?

What were the top 3 highest grossing categories?

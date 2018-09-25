# SQL
## SQL commands and exercises using customers, product, and order tables.  contains query, join, and aggregate commands.  (XAMPP server, PHPMyAdmin)


![](https://github.com/smandekar1/SQL/blob/master/images/customer_list.JPG)

UPDATE customers 
SET email = 'updatedemail@gmail.com' 
where id = 3;

DELETE from customers
where id = 4;

ALTER TABLE customers
MODIFY COLUMN testCol int(11);

ALTER TABLE customers 
DROP testCol;

SELECT * from customers;

SELECT first_name, last_name FROM customers;

SELECT * FROM customers WHERE id = 2;

SELECT * FROM customers ORDER BY last_name;

SELECT DISTINCT state FROM customers;

SELECT * FROM customers WHERE age < 30;

SELECT * FROM customers WHERE city like '%chi%';

SELECT * FROM customers WHERE state IN ('il')
CREATE INDEX Cindex ON customers(city);

## Creating foreign keys to customers and products tables 

CREATE TABLE orders ( id INT NOT NULL AUTO_INCREMENT, orderNUMBER INT, productID INT, customerID INT, orderDate DATETIME DEFAULT CURRENT_TIMESTAMP, PRIMARY KEY(id), FOREIGN KEY(customerID) REFERENCES customers(id), FOREIGN KEY(productID) REFERENCES products(id) )

## Inner Join – matches on the foreign key fields from another table 

![](https://github.com/smandekar1/SQL/blob/master/images/Inner_Join.JPG)

SELECT customers.first_name, customers.last_name, orders.orderNUMBER
FROM customers
INNER JOIN orders 
ON customers.id = orders.customerID
ORDER BY customers.last_name;

SELECT customers.first_name, customers.last_name, orders.orderNUMBER, orders.orderDate
FROM customers
LEFT JOIN orders ON customers.id = orders.customerID
ORDER BY customers.last_name

SELECT orders.orderNUMBER, customers.first_name, customers.last_name
FROM orders
RIGHT JOIN customers
ON orders.customerID = customers.id
ORDER BY orders.orderNUMBER


## Join of three tables on product and customer id fields

SELECT orders.orderNUMBER, customers.first_name, customers.last_name, products.name
FROM orders
	INNER JOIN products
    	ON orders.productID = products.id
    INNER join customers
    	ON orders.customerID = customers.id
ORDER BY orders.orderNUMBER;

## Aliases make it allow for easier to read labels for your columns

SELECT CONCAT(first_name, ‘ ‘, last_name) AS ‘Name’, address, city, state FROM customers;

## Aliases can be used for tables as well 

Ex: FROM customers AS c, orders AS o

## SQL Aggregate Functions Examples: 

SELECT AVG(age) FROM customers

SELECT COUNT(age) FROM customers

SELECT SUM(age) FROM cusomers 

Ex: If we were looking to group customers by age

SELECT age, COUNT(age) 
FROM customers 
WHERE age > 30
GROUP BY age;

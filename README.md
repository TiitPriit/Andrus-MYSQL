# Andrus-MYSQL
SELECT * FROM books;
SELECT title, release_date, price, type FROM books WHERE release_date >= '2010' AND type != 'ebook' AND type != 'used'ORDER BY title ASC; 
SELECT title, YEAR(release_date) AS year, price, type FROM books WHERE release_date < '1970' AND type = 'used' AND price < 20;
SELECT YEAR(order_date) AS Aasta, COUNT(*) AS 'Tellimuste arv' FROM orders GROUP BY YEAR(order_date);
SELECT YEAR(o.order_date) AS Aasta, COUNT(o.id) AS `Tellimuste arv`, ROUND(SUM(b.price), 2) AS `Müükide summa` FROM orders o LEFT JOIN books b ON o.book_id = b.id WHERE o.status IN ('sent', 'paid', 'ordered') GROUP BY YEAR(o.order_date);
SELECT YEAR(o.order_date) AS Aasta, COUNT(o.id) AS `Tellimuste arv`, ROUND(SUM(b.price), 2) AS `Müükide summa` FROM orders o LEFT JOIN books b ON o.book_id = b.id WHERE o.status IN ('sent', 'paid', 'ordered')  AND YEAR(o.order_date) = (SELECT MAX(YEAR(order_date)) FROM orders) GROUP BY YEAR(o.order_date);
SELECT clients.id, clients.username, SUM(books.price) AS 'Total amount spent' FROM clients JOIN orders ON clients.id = orders.client_id JOIN books ON orders.book_id = books.id WHERE YEAR(orders.order_date) = (SELECT MAX(YEAR(order_date)) FROM orders)  GROUP BY clients.id ORDER BY SUM(books.price) DESC;
SELECT books.title, COUNT(*) AS 'Müüdud eksemplaride arv' FROM orders LEFT JOIN books ON orders.book_id = books.id WHERE YEAR(orders.order_date) = (SELECT MAX(YEAR(order_date)) FROM orders) GROUP BY orders.book_id ORDER BY COUNT(*) DESC LIMIT 10;
SELECT * FROM books WHERE price > (SELECT AVG(price) FROM books);

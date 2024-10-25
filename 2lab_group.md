# Лабораторная работа № 2
### 1. Найти и вывести на экран количество товаров каждого цвета, исключив из поиска товары, цена которых меньше 30.
``` SQL
SELECT color, COUNT(*) as product_count
FROM production.product
WHERE list_price >= 30
GROUP BY color;
```
### 2. Найти и вывести на экран список, состоящий из цветов товаров, таких, что минимальная цена товара данного цвета более 100.
``` SQL
SELECT color
FROM production.product
GROUP BY color
HAVING MIN(list_price) > 100;
```
### 3. Найти и вывести на экран номера подкатегорий товаров и количество товаров в каждой категории.
``` SQL
SELECT product_subcategory_id, COUNT(*) as product_count
FROM production.product_subcategory
GROUP BY product_subcategory_id;
```
### 4. Найти и вывести на экран номера товаров и количество фактов продаж данного товара (используется таблица SalesORDERDetail).
``` SQL
SELECT sales_order_id, COUNT(*) as sales_count
FROM sales.sales_order_detail
GROUP BY sales_order_id;
```
### 5. Найти и вывести на экран номера товаров, которые были куплены более пяти раз.
``` SQL
SELECT product_id
FROM purchasing.purchase_order_detail
GROUP BY product_id
HAVING SUM(order_qty) > 5;
```
### 6. Найти и вывести на экран номера покупателей, CustomerID, у которых существует более одного чека, SalesORDERID, с одинаковой датой.
``` SQL
SELECT customer_id
FROM sales.sales_order_header
GROUP BY customer_id, order_date
HAVING COUNT(sales_orderid) > 1;
```
### 7. Найти и вывести на экран все номера чеков, на которые приходится более трех продуктов.
``` SQL
SELECT sales_order_id
FROM sales.sales_order_detail
GROUP BY sales_order_id
HAVING COUNT(product_id) > 3;
```
#### 8. Найти и вывести на экран все номера продуктов, которые были куплены более трех раз.
``` SQL SELECT productid
FROM sales.sales_order_detail
GROUP BY product_id
HAVING COUNT(*) > 3;
```
### 9. Найти и вывести на экран все номера продуктов, которые были куплены или три или пять раз.
``` SQL
SELECT product_id
FROM sales.sales_order_detail
GROUP BY product_id
HAVING COUNT(*) IN (3, 5);
```
### 10. Найти и вывести на экран все номера подкатегорий, в которым относится более десяти товаров.
``` SQL
SELECT product_subcategory_id
FROM production.product_subcategory
GROUP BY product_subcategory_id
HAVING COUNT(*) > 10;
```
### 11. Найти и вывести на экран номера товаров, которые всегда покупались в одном экземпляре за одну покупку.
``` SQL
SELECT product_id
FROM sales.sales_order_detail
GROUP BY product_id
HAVING MAX(orderqty) = 1 AND MIN(orderqty) = 1;
```
### 12. Найти и вывести на экран номер чека, SalesORDERID, на который приходится с наибольшим разнообразием товаров купленных на этот чек.
``` SQL
SELECT sales_order_id
FROM sales.sales_order_detail
GROUP BY sales_order_id
ORDER BY COUNT(DISTINCT product_id) DESC
LIMIT 1;
```
### 13. Найти и вывести на экран номер чека, SalesORDERID с наибольшей суммой покупки, исходя из того, что цена товара – это UnitPrice, а количество конкретного товара в чеке – это ORDERQty.
``` SQL
SELECT sales_order_id
FROM sales.sales_order_detail
GROUP BY sales_order_id
ORDER BY SUM(unit_price * order_qty) DESC
LIMIT 1;
```
### 14. Определить количество товаров в каждой подкатегории, исключая товары, для которых подкатегория не определена, и товары, у которых не определен цвет.
``` SQL
SELECT product_subcategory_id, COUNT(*) AS product_count
FROM production.product
WHERE product_subcategory_id IS NOT NULL AND color IS NOT NULL
GROUP BY product_subcategory_id;
```
### 15. Получить список цветов товаров в порядке убывания количества товаров данного цвета.
``` SQL
SELECT color, COUNT(*) AS product_count
FROM production.product
GROUP BY color
ORDER BY product_count DESC;
```
### 16. Вывести на экран ProductID тех товаров, что всегда покупались в количестве более 1 единицы на один чек, при этом таких покупок было более двух.
``` SQL
SELECT productid
FROM sales.sales_order_detail
GROUP BY productid
HAVING MIN(orderqty) > 1 AND COUNT(*) > 2;
```
### 17. Найти все цвет товаров, такие что, товаров этого цвета не менее 2 и не более 5 в данном магазине
``` SQL
SELECT color
FEOM production.product
GROUP BY color
HAVING count(*) >= 2 and count(*) <= 5
```
### 18, Найти все товары, их ProductID, которые были куплены более чем на три чека
``` SQL
SELECT product_id 
FROM sales.sales_order_detail
GROUP BY product_id 
HAVING count(order_qty) > 3
```
### 19. Вывести подкатегории у которых количество товаров > 5
``` SQL
SEELCT product_subcategory_id
FEOM production.product
GROUP BY product_subcategory_id
HAVING count (*) > 5
```
### 20. Найти товары которые были куплены более трех раз при этом цена товара была более 100
``` SQL
SELECT product_id 
FROM sales.sales_order_detail
WHERE sales.sales_order_detail.unit_price > 100
GROUP BY product_id
HAVING count(*) > 3
```

### 21. Вывести самый продаваемый товар (productid), с ценой <= 100
``` SQL
SELECT product_id 
FROM sales.sales_order_detail
ORDER BY max(sales.sales_order_detail.unit_price) <= 100 desc
limit 1
```

### 22. Вывести подкатегорию с наибольшим разнообразием товаров в ней
``` SQL
SELECT product_subcategory_id
FROM production.product_subcategory
GROUP BY product_subcategory_id
ORDER BY max(distinct product_subcategory_id) desc
limit 1;
```

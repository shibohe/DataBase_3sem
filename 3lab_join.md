### 1. Вывести название предметов, которые были куплены хотя бы один раз

```SQL
SELECT p.name 
FROM production.product as p
JOIN sales.sales_order_detail as pc 
on p.product_id=pc.product_id
GROUP BY p.name 
HAVING count(*)>=1
```

### 2. Выведите название категории товаров в порядке количества продаж по возрастанию

``` SQL
SELECT psc.name 
FROM production.product as p
JOIN production.product_subcategory as pc
on p.product_subcategory_id=pc.product_subcategory_id
JOIN production.product_category as psc
on pc.product_category_id=psc.product_category_id
JOIN sales.sales_order_detail as w
on p.product_id=w.product_id
GROUP BY psc.name 
ORDER BY count(*) asc

### 3. Вывести названия товаров которые не были проданы ни разу

``` SQL
SELECT p.name
FROM production.product as p
LEFT JOIN sales.sales_order_detail as pc 
on p.product_id=pc.product_id
WHERE pc.product_id is null 
GROUP BY p.name 
```

### 4. Вывести названия товаров синего цвета проданные более 2х раз

``` SQL
SELECT p.name
FROM production.product as p
JOIN sales.sales_order_detail as pc 
on p.product_id=pc.product_id
WHERE color ='Blue'
GROUP BY p.name 
HAVING count(*) > 2
```

### 5. Вывести сколько различных товаров продано в каждой категории товаров 

``` SQL
SELECT psc.name, count(DISTINCT p.product_id)
FROM production.product as p
JOIN production.product_subcategory as pc
on p.product_subcategory_id=pc.product_subcategory_id
JOIN production.product_category as psc
on pc.product_category_id=psc.product_category_id
JOIN sales.sales_order_detail as w
on p.product_id=w.product_id
GROUP BY psc.name 
```

### 6. Вывести список поставщиков отсортированных по количеству поставляемых товаров в порядке возрастания

``` SQL
SELECT p.name
FROM purchasing.vendor as p
JOIN purchasing.product_vendor as pc
on p.business_entity_id=pc.business_entity_id
JOIN production.product as psc
on psc.product_id=pc.product_id
GROUP BY p.name 
ORDER BY count(*) asc
```

### 7. Вывести первые 2 категории отсортированные по возрастанию количества продуктов

``` SQL
SELECT psc.name
FROM production.product as p
JOIN production.product_subcategory as pc
on p.product_subcategory_id=pc.product_subcategory_id
JOIN production.product_category as psc
on pc.product_category_id=psc.product_category_id
GROUP BY psc.name 
ORDER BY count(*) asc
limit 2
```

### 8. Вывести названия категорий в которых более 20 товаров

``` SQL
SELECT psc.name
FROM production.product as p
JOIN production.product_subcategory as pc
on p.product_subcategory_id=pc.product_subcategory_id
JOIN production.product_category as psc
on pc.product_category_id=psc.product_category_id
GROUP BY psc.name 
ORDER BY count(*) > 20
```

### 9. Вывести названия подкатегорий, в которых есть хотя бы один товаров с красным цветом

``` SQL
SELECT pc.name
FROM production.product as p
JOIN production.product_subcategory as pc
on p.product_subcategory_id=pc.product_subcategory_id
WHERE color = 'Red'
GROUP BY pc.name 
HAVING count(*) >= 1
```

### 10. Вывести названия товаров, которые продавались два раза, у которых цвет голубой и вывести их подкатегории

``` SQL
SELECT p.name, psc.name 
FROM production.product as p 
JOIN production.product_subcategory as pc 
on p.production_subcategory_id=pc.production_subcategory_id
JOIN production.product_category as psc
on pc.production_category_id=psc.production_category_id
JOIN sales.sales_order_detail as w 
on p.product_id=w.product_id
WHERE color=‘Blue’
GROUP BY p.name, psc.name 
HAVING count(*) = 2
```

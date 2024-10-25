# Вводная лабораторная.
### 1. Найти и вывести на экран названия продуктов, их цвет и размер.
``` SQL
SELECT name, color, size
FROM production.product
```
### 2. Найти и вывести на экран названия, цвет и размер таких продуктов, у которых цена более 100.
``` SQL
SELECT name, color, size
FROM production.product
WHERE list_price > 100
```
### 3. Найти и вывести на экран название, цвет и размер таких продуктов, у которых цена менее 100 и цвет Black.
``` SQL
SELECT name, color, size
FROM production.product
WHERE color = 'Black' and list_price < 100
```
### 4. Найти и вывести на экран название, цвет и размер таких продуктов, у которых цена менее 100 и цвет Black, упорядочив вывод по возрастанию стоимости продуктов.
``` SQL
SELECT name, color, size
FROM production.product
WHERE list_price < 100 and color = 'Black'
ORDER BY list_price asc
```
### 5. Найти и вывести на экран название и размер первых трех самых дорогих товаров с цветом Black.
``` SQL
SELECT name, size
FROM production.product
WHERE color = 'Black'
ORDER BY list_price desc
limit 3
```

### 6. Найти и вывести на экран название и цвет таких продуктов, для которых определен и цвет, и размер.
``` SQL
SELECT name, color
FROM production.product
WHERE color IS NOT NULL and size IS NOT NULL
```
### 7. Найти и вывести на экран не повторяющиеся цвета продуктов, у которых цена находится в диапазоне от 10 до 50 включительно.
``` SQL
SELECT DISTINCT color
FROM production.product
WHERE list_price BETWEEN 10 AND 50
```
### 8. Найти и вывести на экран все цвета таких продуктов, у которых в имени первая буква ‘L’ и третья ‘N’.
``` SQL
SELECT color
FROM production.product
WHERE name like 'L_N%'
```
### 9. Найти и вывести на экран названия таких продуктов, которых начинаются либо на букву ‘D’, либо на букву ‘M’, и при этом длина имени – более трех символов.
``` SQL 
SELECT name
FROM production.product
WHERE (name LIKE 'D%' or name LIKE 'M%') AND length(name) > 3
```
### 10. Вывести на экран названия продуктов, у которых дата начала продаж – не позднее 2012 года.
``` SQL
SELECT name
FROM production.product
WHERE sells_start_date <= '2012-12-31'
```
### 11. Найти и вывести на экран названия всех подкатегорий товаров.
``` SQL
SELECT product_subcategory_id
FROM production.product
```
### 12. Найти и вывести на экран названия всех категорий товаров.
``` SQL
SELECT product_category_id
FROM production.product
```

### 13. Найти и вывести на экран имена всех клиентов из таблицы Person, у которых обращение (Title) указано как «Mr.».
``` SQL 
SELECT *
FROM peson.person
WHERE title = 'Mr.'
```
### 14. Найти и вывести на экран имена всех клиентов из таблицы Person, для которых не определено обращение (Title).      
``` SQL
SELECT *
FROM person.person
WHERE title IS NULL
```
### 15. Получить все названия товаров в системе, в названии которых третий символ – либо буква “s”, либо буква “r”. Решить задачу как минимум двумя способами.
``` SQL
SELECT name
FROM production.product
WHERE name LIKE '__s%' OR name '__r%'
```

``` SQL
SELECT name
FROM production.product
WHERE name LIKE '__s%' or name LIKE '__r%'
```
### 16. Получить все названия товаров в системе, в названии которых ровно 5 символов. 
``` SQL
SELECT name
FROM production.product
WHERE length(name) = 5
```
### 17. Написать запрос, который возвращает названия товаров, которые были в продаже между мартом 2011 года и мартом 2012 года включительно (необходимо учитывать формат даты)
``` SQL
SELECT *
FROM production.product
WHERE sell_start_date BETWEEN '2011-03-01' AND '2012-03-31'
```

### 18. Найти максимальную стоимость товара (отпускная цена ListPrice) из тех, которые были произведены, начиная с марта 2011 года. 
```SQL
SELECT MAX(list_price) AS list_price
FROM production.product
WHERE sell_start_date >= '2011-03-31'
```
### 18. Найти и вывести на экран названия продуктов, для которых определен цвет, но не определен размер.
``` SQL
SELECT name 
FROM production.product 
WHERE color is not null and size is null
```
### 19. Найти и вывести на экран названия продуктов, у которых номер подкатегории равен или 1 или 3.                                 
``` SQL
SELECT name 
FROM production.product_subcategory 
WHERE product_subcategory_id = '1' or product_subcategory_id = '3'
```

### 20. Найти и вывести на экран названия продуктов, у которых цена лежит в диапазоне от 40 до 300, не включая границы диапазона.                                  
``` SQL
SELECT name 
FROM production.product
WHERE list_price > 40 and list_price < 300
```

### 21. Найти и вывести на экран названия продуктов, у которых цена меньше 40 или больше 300     
``` SQL
SELECT name 
FROM production.product
where list_price<40 or list_price>300
```

### 22. Найти и вывести на экран названия продуктов, у которых цена лежит в диапазоне от 40 до 300, включая границы диапазона.                                       
``` SQL
SELECT name, list_price 
FROM production.product
where list_price >= 40 and  list_price <= 300
```

### 23. Найти и вывести на экран названия подкатегорий с номерами 1, 3, 5
``` SQL
SELECT name 
FROM production.product_subcategory
WHERE product_subcategory_id = '1' or product_subcategory_id = '3' or product_subcategory_id = '5'
```
### 24. Найти и вывести на экран названия категорий с номерами 1, 3, 7
```SQL
SELECT name 
FROM production.product_category
WHERE product_category_id = '1' or product_category_id = '3' or product_category_id = '7'
```
### 25. Найти и вывести на экран имена клиентов (таблица Person), у которых среднее имя (MiddleName) состоит более чем из одной буквы
``` SQL
SELECT first_name 
From person.person
WHERE middle_name not LIKE '_.' and middle_name not LIKE '_'
```

### 26. Найти и вывести на экран названия продуктов, у которых третья буква названии или “u” или “o”     
``` SQL 
SELECT name  
FROM production.product 
WHERE SUBSTRING(name from 3 for 1)='u' or SUBSTRING(name from 3 for 1)='o'             
```
``` SQL 
SELECT name  
FROM production.product 
WHERE name LIKE '__u%' or name LIKE'__o%'
```

### 27. Найти и вывести на экран названия продуктов, у которых в названии нет букв: a, d, g, k, l
```SQL 
SELECT name  
FROM production.product 
WHERE name NOT LIKE '%a%' and name NOT LIKE '%d%' and name NOT LIKE '%g%' and
name NOT LIKE '%k%' and name NOT LIKE '%l%'
```

### 28. Найти и вывести на экран названия продуктов, у которых ProductNumber содержит два символа дефис
``` SQL
SELECT name,productnumber 
FROM production.product 
WHERE product_number like '%-%-%'
```
### 29. Найти и вывести на экран имена клиентов (таблица Person), у которых Suffix определен, и не равен “Jr.” 
``` SQL 
SELECT firstname,suffix from person.person
WHERE suffix IS NOT NULL and suffix NOT LIKE 'Jr.'
```

``` SQL
select firstname,suffix from person.person
WHERE suffix IS NOT NULL and suffix!='Jr.'
```

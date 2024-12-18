# Домашнее задание к занятию «SQL. Часть 2» - Козырев Роман

### Задание 1

Одним запросом получите информацию о магазине, в котором обслуживается более 300 покупателей, и выведите в результат следующую информацию: 
- фамилия и имя сотрудника из этого магазина;
- город нахождения магазина;
- количество пользователей, закреплённых в этом магазине.

### Решение 1

```sql
SELECT c.store_id, s2.first_name, s2.last_name, c2.city, count(c.store_id)
FROM customer c
JOIN store s1 ON s1.store_id = c.store_id 
JOIN staff s2 ON s1.manager_staff_id = s2.staff_id 
JOIN address a ON s1.address_id = a.address_id 
JOIN city c2 ON c2.city_id = a.city_id 
GROUP BY store_id
HAVING count(c.store_id) > 300;
```
![image](https://github.com/user-attachments/assets/7909222e-a425-413a-b566-6855bd4d969e)

### Задание 2

Получите количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.

### Решение 2

```sql
SELECT count(f.`length`)
FROM film f 
WHERE f.`length` > (SELECT avg(`length`) FROM film f);
```
![image](https://github.com/user-attachments/assets/6bd8eea8-deea-4642-b360-403fde3c7c24)

### Задание 3

Получите информацию, за какой месяц была получена наибольшая сумма платежей, и добавьте информацию по количеству аренд за этот месяц.

### Решение 3

```sql
SELECT month (payment_date) AS mounth, count(payment_id) AS payments, sum(amount) AS amount
FROM payment
GROUP BY month(payment_date)
ORDER BY count(payment_id) DESC LIMIT 1 ;
```
![image](https://github.com/user-attachments/assets/bda8cd3d-b62f-4526-8f85-5067e998a442)

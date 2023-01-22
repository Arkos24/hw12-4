# Домашнее задание к занятию "`SQL. Часть 2`" - `Мельников Семен`




### Задание 1


SELECT  
	CONCAT ( sakila.s.first_name, ' ', sakila.s.last_name) as Сотрудник,
	sakila.c2.city as Город,
	COUNT (sakila.c.store_id) as Покупателей
FROM sakila.staff s 
JOIN sakila.customer c ON sakila.c.store_id = sakila.s.store_id
JOIN sakila.address a  ON sakila.a.address_id  = sakila.s.address_id
JOIN sakila.city c2 ON sakila.c2.city_id =  sakila.a.city_id 
GROUP BY sakila.s.staff_id  HAVING Покупателей > 300

![image](https://user-images.githubusercontent.com/114281054/213910690-5a2b619e-3eac-47c5-98d8-df9f8d411c32.png)




---

### Задание 2


SELECT COUNT(1) as 'Длиннее среднего'
FROM sakila.film
WHERE `length` > (SELECT AVG(`length`) FROM sakila.film)length`) FROM film)

![image](https://user-images.githubusercontent.com/114281054/213910861-bf966599-58c3-416e-9e9e-cd47ad30dd0c.png)


### Задание 3
Не уверен, что верно понял задание, месяцы каждого года по отдельности(не складывал июли с июлями и т.д..)


SELECT x_period, x_summ, COUNT(r.rental_id) as x_times
FROM
(SELECT x_period, x_summ FROM
		(
		SELECT  DATE_FORMAT(payment_date, '%M-%Y') as x_period, SUM(amount) as x_summ 
		FROM payment p  
		GROUP BY DATE_FORMAT(payment_date, '%M-%Y')
		)
tab1 ORDER BY x_summ  DESC Limit 1
)
tab2 JOIN rental r on DATE_FORMAT(r.rental_date, '%M-%Y') = tab2.x_period
GROUP BY x_period, x_summ 

![image](https://user-images.githubusercontent.com/114281054/213911500-0d40de80-783c-4eee-847c-3bbb3f7ae275.png)



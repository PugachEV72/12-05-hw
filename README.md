# Домашнее задание к занятию 12.5. «Индексы» - Пугач Евгений.


---

## `Задание 1`

### Решение: 

SELECT
TABLE_SCHEMA AS `database`,        
CONCAT(ROUND(SUM(DATA_LENGTH / 1024 / 1024) + SUM(INDEX_LENGTH / 1024 / 1024) ,2) ,' MB') AS total_size ,  
CONCAT(ROUND(SUM(DATA_LENGTH / 1024 / 1024) , 2) ,' MB') AS data_size ,  
CONCAT(ROUND(SUM(INDEX_LENGTH / 1024 / 1024) , 2) ,' MB') AS index_size ,  
CONCAT(ROUND((SUM(INDEX_LENGTH) / SUM(DATA_LENGTH)) *100.0 ,2), ' %') AS percentage_ratio  
FROM INFORMATION_SCHEMA.TABLES  
WHERE TABLE_SCHEMA = 'sakila';


![Скриншот 1](https://github.com/PugachEV72/Images/blob/master/2023-03-26_00-06-08.png)


---

## `Задание 2`

### Решение:

![Скриншот 2](https://github.com/PugachEV72/Images/blob/master/2023-03-26_00-20-43.png)

Составное условие WHERE можно переписать как JOIN, убрать операторы distinct, over (partition by c.customer_id, f.title),  
таблицы film, rental и inventory на результат не влияют - их можно убрать из запроса.

select   
concat(c.last_name, ' ', c.first_name) as "Full Name",   
sum(p.amount) as "Total Amount"  
from payment p   
join rental r on p.payment_date = r.rental_date  
join customer c on r.customer_id = c.customer_id   
where date(p.payment_date) = '2005-07-30'  
group by c.customer_id;


![Скриншот 3](https://github.com/PugachEV72/Images/blob/master/2023-03-26_10-31-56.png)

После корректировки запроса, время получения ответа значительно сократилось:

![Скриншот 4](https://github.com/PugachEV72/Images/blob/master/2023-03-26_10-34-10.png)

---

### Доработка

![Скриншот 5](https://github.com/PugachEV72/Images/blob/master/2023-03-29_23-47-06.png)

![Скриншот 6](https://github.com/PugachEV72/Images/blob/master/2023-03-29_23-49-14.png)

![Скриншот 7](https://github.com/PugachEV72/Images/blob/master/2023-03-30_00-12-00.png)

![Скриншот 8](https://github.com/PugachEV72/Images/blob/master/2023-03-30_00-15-19.png)





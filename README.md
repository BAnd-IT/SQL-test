# Вопрос 2
# В БД есть таблица с регистрацией клиентов вида CustomerId, RegistrationDateTime, Name (допустим 'reg')
# и таблица с покупками клиентов вида CustomerId, PurchaiseDatetime, ProductName (допустим 'orders'). 
# Напишите SQL запрос, который выберет имена клиентов, которые когда-либо покупали молоко, но не покупали сметану за последний месяц.

SELECT DISTINCT reg.Name
FROM reg
JOIN orders ON orders.CustomerId = reg.CustomerId AND orders.ProductName = "молоко"
and reg.CustomerId not in
(
select orders.CustomerId 
FROM orders
JOIN reg ON orders.CustomerId=reg.CustomerId
where orders.ProductName='сметана'
and orders.PurchaiseDatetime > NOW() - INTERVAL 30 DAY
)

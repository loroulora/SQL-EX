## 1
### Найдите номер модели, скорость и размер жесткого диска для всех ПК стоимостью менее 500 дол. Вывести: model, speed и hd

```
select 
	model, 
	speed, 
	hd
from 
	PC
where 
	price < 500
```

## 2 
### Найдите производителей принтеров. Вывести: maker

```
SELECT 
	DISTINCT maker
FROM 
	Product
WHERE 
	type='Printer'
```

## 3 
### Найдите номер модели, объем памяти и размеры экранов ПК-блокнотов, цена которых превышает 1000 дол.

```
select 
	model, 
	ram, 
	screen
from 
	laptop
where 
	price > 1000
```

## 4 
### Найдите все записи таблицы Printer для цветных принтеров.

```
select 
	* 
from 
	Printer 
where
	color = 'y'
```

## 5 
### Найдите номер модели, скорость и размер жесткого диска ПК, имеющих 12x или 24x CD и цену менее 600 дол.

```
select 
	model, 
	speed, 
	hd 
from 
	pc
where 
	(cd = '12x' or cd = '24x') 
  and 
	price < 600
```

## 6 
### Для каждого производителя, выпускающего ПК-блокноты c объёмом жесткого диска не менее 10 Гбайт, найти скорости таких ПК-блокнотов. Вывод: производитель, скорость.

```
select 
	distinct maker,
	speed
from 
	product 
inner join 
	laptop 
on 
	product.model = laptop.model 
where 
	laptop.hd >= 10
```

## 7 
### Найдите номера моделей и цены всех имеющихся в продаже продуктов (любого типа) производителя B (латинская буква).

```
select 
	distinct pc.model,
  	price 
from 
  	product 
join 
  	pc 
on 
  	product.model = pc.model
where 
  	maker = 'B'

union

select 
  	distinct printer.model,
  	price 
from 
 	product
join 
  	printer 
on 
  	product.model = printer.model
where 
  	maker = 'B'

union

select 
  	distinct laptop.model,
  	price 
from 
  	product
join 
  l	aptop 
on 
  	product.model = laptop.model
where 
  	maker = 'B'
```

## 8
### Найдите производителя, выпускающего ПК, но не ПК-блокноты.

```
select 
  	distinct maker 
from 
  	Product
where 
  	type = 'PC' 

except 

select 
  	distinct maker 
from 
  	Product
where 
  	type = 'Laptop'
```

## 9
### Найдите производителей ПК с процессором не менее 450 Мгц. Вывести: Maker

```
select 
  	distinct Product.maker 
from 
  	Product
join 
  	pc 
on 
  	Product.model = pc.model
where 
  	pc.speed >= 450
```

## 10
### Найдите модели принтеров, имеющих самую высокую цену. Вывести: model, price

```
select 
  	distinct model, 
 	 price
from 
  	Printer
where 
  	price = (select 
               		max(price)
            	from 
                	Printer)
```

## 11
### Найдите среднюю скорость ПК.

```
select 
  	avg(speed) as Avg_speed
from 
  	pc
```

## 12
### Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.

```
select 
  	avg(speed) as avg_speed
from 
  	Laptop
where 
  	price > 1000
```

## 13
### Найдите среднюю скорость ПК-блокнотов, цена которых превышает 1000 дол.

```
select 
  	avg(speed) as avg_speed 
from 
  	pc 
inner join 
  	product 
on 
  	product.model = pc.model
where 
  	product.maker = 'A'
```


## 14
### Найдите класс, имя и страну для кораблей из таблицы Ships, имеющих не менее 10 орудий.

```
select 
  	ships.class,
  	name,
  	country 
from 
  	classes
join 
  	ships 
on 
  	classes.class = ships.class
where 
  	numGuns >= 10
```

## 15
### Найдите размеры жестких дисков, совпадающих у двух и более PC. Вывести: HD

```
select 
  	hd
from 
  	pc
group by 
  	hd 
having 
  	count(hd) >= 2
```

## 16
### Найдите пары моделей PC, имеющих одинаковые скорость и RAM. В результате каждая пара указывается только один раз, т.е. (i,j), но не (j,i), Порядок вывода: модель с большим номером, модель с меньшим номером, скорость и RAM.

```
select
  	distinct A.model as modei_1, 
  	B.model as model_2,
  	A.speed ,
  	A.ram 
from 
  	pc AS A, 
  	pc AS B
where 
  	A.speed = B.speed
  and 
    	A.ram = B.ram
  and 
    	A.model > B.model
```

## 17
### Найдите модели ПК-блокнотов, скорость которых меньше скорости каждого из ПК. Вывести: type, model, speed

```
select 
  	distinct type, 
  	laptop.model, 
  	speed
from 
  	product 
join 
  	laptop 
on 
  	product.model = laptop.model 
where 
  	speed < ALL 	(select 
                 		speed
                	from 
                   		pc)
```

## 18
### Найдите производителей самых дешевых цветных принтеров. Вывести: maker, price

```
SELECT 
	DISTINCT maker,
	price
FROM 
  	product
JOIN 
  	printer 
ON 
  	product.model = printer.model
WHERE 
  	price = (SELECT 
              		min(price) 
           	FROM 
              		printer 
           	WHERE 
             		color = 'y') 
AND 
  	color = 'y'
```

## 19
### Для каждого производителя, имеющего модели в таблице Laptop, найдите средний размер экрана выпускаемых им ПК-блокнотов. Вывести: maker, средний размер экрана.

```
select 
	maker, 
	avg(screen) as avg_screen 
from 
	laptop 
join 
	product 
on
	laptop.model = product.model 
group by 
	maker
```

## 20
### Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.

```
select 
	maker, 
	count(model) as count_model
from 
	product
where 
	type = 'PC'
group by 
	maker
having 
	count(model) >= 3
```

## 21
### Найдите производителей, выпускающих по меньшей мере три различных модели ПК. Вывести: Maker, число моделей ПК.

```
select 
	maker, 
	max(price) as max_price
from 
	pc 
join 
	product 
on 
	product.model = pc.model
group by 
	maker
```


## 22
### Для каждого значения скорости ПК, превышающего 600 МГц, определите среднюю цену ПК с такой же скоростью. Вывести: speed, средняя цена.

```
select 
	speed,
	avg(price) as avg_price 
from 
	pc 
where 
	speed > 600
group by 
	speed
```

## 23
### Найдите производителей, которые производили бы как ПК со скоростью не менее 750 МГц, так и ПК-блокноты со скоростью не менее 750 МГц. Вывести: Maker

```
select 
	maker 
from 
	product 
join 
	pc 
on 
	product.model = pc.model
where 
	pc.speed >= 750
group by 
	maker

intersect 

select 
	maker 
from 
	product 
join 
	laptop 
on 
	product.model = laptop.model
where 
	laptop.speed >= 750
group by 
	maker
```

## 24
### Перечислите номера моделей любых типов, имеющих самую высокую цену по всей имеющейся в базе данных продукции.

```
with rev as (
	select 
		model, price
	from 
		pc

union 

	select 
		model, price
	from 
		laptop 

union 

	select 
		model, price
	from 
		printer 
) 

select 
	model 
from 
	rev
where price = (select 
               max(price) as max_price 
               from rev)
```

## 25 
### Найдите производителей принтеров, которые производят ПК с наименьшим объемом RAM и с самым быстрым процессором среди всех ПК, имеющих наименьший объем RAM. Вывести: Maker

```
select 
	distinct maker 
from 
	product
where 
	type = 'Printer'
and 
	maker in 
				(select 
					maker
				 from 
				 	product
				 join 
				 	pc 
				 ON product.model = pc.model
				 where 
				 	speed =
							 (select 
							 	max(speed)
							  from 
								  	(select 
										speed 
									 from 
									 	pc 
									 where 
									 	ram = (select 
												min(ram) 
										       from 
										       		pc)) 
													as ze)
				AND 
				ram = (select 
						min(ram) 
					   from 
					   	pc))
```

## 26 
### Найдите среднюю цену ПК и ПК-блокнотов, выпущенных производителем A (латинская буква). Вывести: одна общая средняя цена.

```
select 
	avg(price) as avg_price 
from (
  select 
  	price 
  from 
  	pc 
  join 
	product
  on 
  	pc.model = product.model 
  where 
  	maker = 'A'
union all 
   select 
   	price 
   from 
   	laptop 
   join 
	product
   on 
   	laptop.model = product.model
   where 
   	maker = 'A'
  ) as rv
```

## 27
### Найдите средний размер диска ПК каждого из тех производителей, которые выпускают и принтеры. Вывести: maker, средний размер HD.

```
select 
	maker, 
	AVG(pc.hd) as avg_hd 
from 
	product
join 
	pc 
on 
	pc.model = product.model 
where 
	maker in (select 
			maker 
		  from 
			product 
		  where 
			type = 'Printer')
group by 
	maker
```

## 28
### Используя таблицу Product, определить количество производителей, выпускающих по одной модели.

```


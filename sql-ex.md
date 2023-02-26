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
  laptop 
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

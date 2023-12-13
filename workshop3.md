# da-in-gamedev
# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Селянина Виктория Андреевна
- РИ220936
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице. 
- Задание 2.
- Создайте 10 сцен на Unity с изменяющимся уровнем сложности.
- Задание 3.
- Заполнить google-таблицу данными из Python.
- Выводы.

## Цель работы
Разработать оптимальный баланс для десяти уровней игры Dragon Picker

## Задание 1
### Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице. 

- Переменные, влияющие на балнс:
  - timeBetweenEggDrops - время между сбросом яиц
  - leftRightDistance - расстояние между рамками поля, в котором может дивгаться дракон
  - chanceDirection - шанс изменения направления дракона
  - speed - скорость дракона
 
Так как координация и скорость внимания игрока напрямую вляют на успех в игре, то сложность будет возрастать экспоненциально. Для того, чтобы сложность возрастала с каждым уровнем, необходимо каждый раз увеличивать расстояние между рамками поля, скорость дракона, шанс зименения направления дракона и уменьшать время между сбросом яиц. Для визуализации в гугл-таблице была составленна данная формула:

```py

difficulty factor = chanceDirection / timeBetweenEggDrops * speed * leftRightDistance

```
Динамику сложности уровней Вы можете увидеть в 3 задании.

## Задание 2
### Создайте 10 сцен на Unity с изменяющимся уровнем сложности.

С результатом данного задания вы можете ознакомиться по ссылке : https://github.com/Eiasav/dragon-picker.git

## Задание 3
### Заполнить google-таблицу данными из Python.
Результат заполнения таблицы данными:
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/a0cd6f89-9867-425d-b00e-b4d56203b865)
Для заполнения таблицы данными я написала код:
```py

import gspread
import numpy as np
import matplotlib.pyplot as plt

gc = gspread.service_account(filename = 'worshop-3-19e26d47d10f.json')
sh = gc.open("difficulty factor")
speed = [4]
leftRightDistance  = [10]
timeBetweenEggDrops  = [2]
chanceDirection = [0.01]
level = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
def _update(column, start, end, delta):
    i = 0
    count = 2
    array = []
    while count < 11:
        count += 1
        array.append(random.uniform(start, end) + delta * i)
        sh.sheet1.update((column + str(count)), random.uniform(start, end) + delta * i)
        start, end = start + delta, end + delta
        i += 1
    return array

speed += (_update('B', 4.00, 5.00, 0.8))
timeBetweenEggDrops  += (_update('C', 1.5, 1.6, -0.09))
leftRightDistance  += (_update('D', 10.00, 11.00, 0.74))
chanceDirection += (_update('E', 0.01, 1.00, 0.33))

plt.plot(speed, level)
plt.title("speed")
plt.ylabel("level number")
plt.xlabel("speed")
plt.show()

plt.plot(timeBetweenEggDrops, level)
plt.title("time")
plt.ylabel("level")
plt.xlabel("time")
plt.show()

plt.plot(leftRightDistance, level)
plt.title("distance")
plt.ylabel("level")
plt.xlabel("distance")
plt.show()

plt.plot(chanceDirection, level)
plt.title("chance")
plt.ylabel("level")
plt.xlabel("chance")
plt.show()

```
Визуализация данных в Python:

![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/99f87f2a-adf8-4605-8f2c-c86a0738b5e8)
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/c14f8f5e-f133-412e-b3e4-725969ca112f)
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/2a5d4c67-4b17-4fea-9c04-6c5dea9a7f26)
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/28307074-4628-4152-a861-bd7a45b71454)


## Выводы

В ходе данной лабораторной работы я настроила баланс на примере игры Dragon Picker, создала 10 различных сцен в Unity на основе данных, полученных из Google таблицы, с помощью кода на языке C# и визуализировала изменение переменных с помощью библиотеки matplotlib.

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**

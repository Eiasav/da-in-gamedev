# da-in-gamedev
# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Селянина Виктория Андреевна
- РИ220936
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | # | 20 |
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


## Задание 3
### Заполнить google-таблицу данными из Python.

![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/17f702e4-9e64-4403-b49c-02b7450adf6b)

```py

import gspread
import numpy as np
import matplotlib.pyplot as plt
import time

gc = gspread.service_account(filename = 'worshop-3-19e26d47d10f.json')
sh = gc.open("difficulty factor")
speed = 4.00
distance = 10.00
timeBeet = 2.00
chance = 0.01
i = 0
end = 8
while i <= 8:
    temp = np.random.randint(-100, 100, 3) 
    i += 1
    if i == 0:
        continue
    else:
        sh.sheet1.update(('A' + str(i + 1)), str(i))
        sh.sheet1.update(('B' + str(i + 2)), speed + 0.7 * i + (temp[0] / 1000))
        sh.sheet1.update(('C' + str(i + 2)), timeBeet - 0.2 * i + (temp[1] / 1000))
        sh.sheet1.update(('D' + str(i + 2)), distance + 0.3 * i + (temp[2] / 1000))
        sh.sheet1.update(('E' + str(i + 2)), chance - 0.0002 * i)

```
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/99f87f2a-adf8-4605-8f2c-c86a0738b5e8)


## Выводы

Я познакомилась с визуализацией данных из GoogleSheets в Unity и работой со звуковыми эффектами в Unity с помощью скриптов на Python и C#.

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**

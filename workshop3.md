# da-in-gamedev
# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
- Селянина Виктория Андреевна
- РИ220936
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | # | 60 |
| Задание 2 | # | 20 |
| Задание 3 | # | 20 |

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
### С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в выбранной игре (в качестве таких переменных может выступать игровая валюта, ресурсы, здоровье и т.д.). Средствами google-sheets визуализируйте данные в google-таблице (постройте график, диаграмму и пр.) для наглядного представления выбранной игровой величины.

- Написать следующий код на Pythonи, заполняющий google-таблицу, связ с которой ранее настроили при помощи GoogleCloud.
  
```py

import gspread
import numpy as np
gc = gspread.service_account(filename = 'unitydatascience-402805-5bac807ce896.json')
sh = gc.open("UnityWorkshop2")
price = np.random.randint(0, 20, 11)
mon = list(range(1, 11))
i = 0
while i <= len(mon):
    i += 1
    if i == 0:
        continue
    else:
        tempInf = ((price[i - 1] - price[i - 2]) / price[i - 2]) * 100
        tempInf = str(tempInf)
        tempInf = tempInf.replace('.', ',')
        sh.sheet1.update(('A' + str(i)), str(i))
        sh.sheet1.update(('B' + str(i)), str(price[i - 1]))
        sh.sheet1.update(('C' + str(i)), str(tempInf))
        print(tempInf)

```
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/eb57a5ca-4248-42c2-b8ac-03d0f7631523)
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/11aa303a-6baf-4c1e-8225-340bae1e9721)

- В первом столбце таблице указывается номер итерации, во втором сгенерированное число, а в третьем процентное соотношение разницы сгенерированного числа и предыдущего в сравнении с минимальным значением, необходимым для получения награды.
- Визуализация данных при помощи средств GoogleSheets (красная линия - значения второго стлобца, синия - третьего):

  ![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/9cdb711f-529f-4ff5-9184-1c0f6b6d389e)




## Задание 3
### Заполнить google-таблицу данными из Python.

![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/e20bafbf-cbdf-461e-a3b2-5e6d36f61736)


```py

import gspread
import numpy as np
import matplotlib.pyplot as plt
import time

gc = gspread.service_account(filename = 'worshop-3-19e26d47d10f.json')
sh = gc.open("difficulty factor")
speed = 1.00
distance = 10.00
timeBeet = 2.00
chance = 0.02
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


## Выводы

Я познакомилась с визуализацией данных из GoogleSheets в Unity и работой со звуковыми эффектами в Unity с помощью скриптов на Python и C#.

Анектод про Штирлица для поднятия настроения:
```
Штирлиц толкнул дверь. Дверь не открылась. Штирлиц толкнул сильнее. Дверь даже не шелохнулась. Штирлиц ударил ногой. С тем же успехом. Штирлиц разбежался и бросился на дверь всем телом.
Дверь не поддавалась.
"Закрыто", - догадался Штирлиц.
```
## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**

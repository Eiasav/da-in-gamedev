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
- Заполнить google-таблицу данными из Python. В Python данные также должны быть визуализированы.
- Выводы.

## Цель работы
Разработать оптимальный баланс для десяти уровней игры Dragon Picker

## Задание 1
### Предложите вариант изменения найденных переменных для 10 уровней в игре. Визуализируйте изменение уровня сложности в таблице. 

Ход работы:
- Выбрать игру. Я остановилась на игре Divinity: Original Sin 2. Divinity: Original Sin 2 - это пошаговая партийная ролевая видеоигра.
- Концепт игры: это ролевая партийная игра с пошаговой боевкой и открытым миром. Помимо одиночной кампании есть и совместная до 4 игроков - по сети или в режиме разделенного экрана, а также режим гейм-мастера. Игроку доступны более 200 навыков и 12 разных школ.
- Сюжет. Божественный мертв. Пустота надвигается со всех сторон. И виноваты в этом колдуны Истока. Магистры Божественного Ордена стремятся избавить Ривеллон от угрозы со стороны колдунов... подобных вам. Вы схвачены и отправлены в форт "Радость", где вам предстоит "излечиться" от своего "недуга". Это "лечение" может дорого вам обойтись.
- Скриншот геймплея игры:
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/163495b9-7303-445e-aa04-03761e0f29e7)
- Для описания ресурса я выбрала щепки тронутого Пустотой живодера
- Описание: данный ресурс можно добыть в двух локациях в игре - Лесопилка в Трухлявом лесу Побережья Жнеца и область в Арксе, покрытая туманом смерти. Можно продать или использовать для создания Усиленного Пустотой яда.
- Экономическая модель ресурса:
![воркшоп 2](https://github.com/Eiasav/da-in-gamedev/assets/130223999/69d2baa2-6c4c-4bea-8590-0b7991b72804)

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
### Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.

- Создаем пустой GameObject и привязываем к нему скрипт, куда добавляем код, написанный ниже. Подключаем скрипт и звуковые дорожки в инспекторе.

![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/aa29ed8f-7c77-4436-9729-44d312e417ee)
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/d04fd54d-da28-4f78-8ccf-a1e071819c01)

```py

using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class gameobj : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string, float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;

    void Start()
    {
        StartCoroutine(GoogleSheets());
    }

    // Update is called once per frame
    void Update()
    {
        if (i > dataSet.Count) return;

        if (dataSet["Mon_" + i.ToString()] <= 10 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] > 10 & dataSet["Mon_" + i.ToString()] < 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }

        if (dataSet["Mon_" + i.ToString()] >= 100 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curenResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1WDVGYHi-jJTAS3BrRTzB0QS4D2kkjNlzkbwQUWTQOuc/values/A1%3AZ100?key=AIzaSyCEP86S7nN6iHS0E7AI-aBcJO8woaaV7ro");
        yield return curenResp.SendWebRequest();
        string rawResp = curenResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"]) 
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[2]));
        }
    }

    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}


```

- Несложно заметить, что значения, выводимые в консоли Unity, полностью солвпадают со значениями из таблицы:
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/1109797c-8516-419f-8a70-918754bb21c2)
![image](https://github.com/Eiasav/da-in-gamedev/assets/130223999/34b79c53-54b6-4e07-8d47-ccb8af020f93)


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
